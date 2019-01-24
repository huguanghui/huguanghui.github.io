[TOC]

---
# gSoap源码中Alist的使用

```cpp
typedef void* ALIST_T

#define SOAP_MAXALLOCSIZE (0)   // 无限制

#define SOAP_CANARY  (0xC0DE)

void *soap_malloc(ALIST_T *list, size_t n);
void *soap_calloc(ALIST_T *list, size_t n);
char *soap_strdup(ALIST_T *list, const char *s);

void soap_echo_alist(ALIST_T *list);

void soap_dealloc(ALIST_T *list, void *p);

源码
void* soap_malloc(ALIST_T *list, size_t n)
{ 
    char *p;

    if (SOAP_MAXALLOCSIZE > 0 && n > SOAP_MAXALLOCSIZE)
        return NULL;
    if (n + sizeof(short) < n)
        return NULL;

    n += sizeof(short);
    if (n + ((-(long)n) & (sizeof(void*)-1)) + sizeof(void*) + sizeof(size_t) < n)
        return NULL;
    n += (-(long)n) & (sizeof(void*)-1); /* align at 4-, 8- or 16-byte boundary by rounding up */   
    p = (char*)SOAP_MALLOC(n + sizeof(void*) + sizeof(size_t));
    if (!p)
    { 
        return NULL;
    }
    /* set a canary word to detect memory overruns and data corruption */
    *(unsigned short*)(p + n - sizeof(unsigned short)) = (unsigned short)SOAP_CANARY;
    /* keep chain of alloced cells for destruction */
    *(void**)(p + n) = *list;
    *(size_t*)(p + n + sizeof(void*)) = n;
    *list = p + n;
    PRINT_Y("[%d]List:%x", n, *list);
    
    return p;
}
void* soap_calloc(ALIST_T *list, size_t n)
{
    char *p;

    p = soap_malloc(list, n);
    if (p)
    {
        memset(p, 0, n);
    }

    return p;    
}

char *soap_strdup(ALIST_T *list, const char *s)
{ 
  char *t = NULL;
  if (s)
  { 
    size_t n = strlen(s) + 1;
    if (n > 0)
    { t = (char*)soap_malloc(list, n);
      if (t)
      { memcpy((void*)t, (const void*)s, n);
        t[n - 1] = '\0';
      }
    }
  }
  return t;
}

void soap_dealloc(ALIST_T *list, void *p)
{
    if (p)
    {
        char **q;
        for (q = (char **)(void *)list; *q; q = *(char***)q)
        {
            if (*(unsigned short*)(char*)(*q - sizeof(unsigned short)) != (unsigned short)SOAP_CANARY)
            {
                return;
            }
            if (p == (void*)(*q - *(size_t*)(*q + sizeof(void*))))
            {
                *q = **(char***)q;
                SOAP_FREE(p);
                return;
            }
        }
    }
    else
    {
        char *q;
        while (*list)
        {
            q = (char*)*list;
            if (*(unsigned short*)(char*)(q - sizeof(unsigned short)) != (unsigned short)SOAP_CANARY)
            {
                return;
            }
            *list = *(void**)q;
            q -= *(size_t*)(q + sizeof(void*));
            SOAP_FREE(p);
        }
    }

    return;
}
```

# 特点
1.代码结构简洁
2.可以对多指针的结构体进行统一分配和释放