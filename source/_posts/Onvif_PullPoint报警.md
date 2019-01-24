 [TOC]

---

# Onvif的报警结构整理

## 1.PullPoint方式
### 1.1 创建PullPointSubscription
    {
        char *to;
        char *from;
        char *token;
        time_t termTime;
        int bDestroy;
        int bFirst;
    }
### 1.2 PullMessage
    查找，{检查销毁条件}，超时时间获取报警, 销毁报警
### 1.3 销毁
    bDestroy = 1

## 2.Subscript方式
### 2.1 创建
    {
        char *to;
        char *from;
        char *token;
        time_t termTime;
        int bDestroy;
        int bFirst;
    }    
### 2.2 有报警，向订阅地址发送消息 
### 2.3 销毁

## 3.测试步骤(时间同步问题)
### 3.1 UTC时间同步情况下
### 3.2 UTC时间不同步情况下