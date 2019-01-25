---
title: Lex和Yacc的入门
categories:
  - 开源代码
tags:
  - 软件
reward: true
originContent: "@[toc]\n\n---\n\n# lex和yacc简介\n\nlex和yacc是自动编译C代码的工具,适合于解析简单语言.这些工具常用于编译器或者解释器的组成部分，或者用于读取配置文件.“lex”和“yacc”这两个名字所代表的也包括这些工具的 GNU 版本 flex 和 bison. lex 和 yacc 是一对配对工具。lex 将文件分解为成组的“记号（tokens）”，大体上类似于单词。yacc 接受 成组的记号，并将它们装配为高层次的结构，类似于句子。yacc 设计用来处理 lex 的输出，不过您也可以 编写自己的代码来完成此任务。同样，lex 的输出很大程度上设计用于为某类解析器提供数据。\n\n# lex使用\n[Lex语法分析](http://www.kuqin.com/shuoit/20160526/352209.html)\n# yacc使用\n\n# 实例应用\n使用的是linux系统下的flex和bison,它们是lex和yacc的加强版.\ncalculator.l的源码\n\n```cpp\n%{  \n#include <stdio.h>  \n#include \"y.tab.h\"  \n  \nint  \nyywrap(void)  \n{  \n    return 1;  \n}  \n%}  \n%%  \n\"+\"             return ADD;  \n\"-\"             return SUB;  \n\"*\"             return MUL;  \n\"/\"             return DIV;  \n\"\\n\"            return CR;  \n([1-9][0-9]*)|0|([0-9]+\\.[0-9]*) {  \n    double temp;  \n    sscanf(yytext, \"%lf\", &temp);  \n    yylval.double_value = temp;  \n    return DOUBLE_LITERAL;  \n}  \n[ \\t] ;  \n. {  \n    fprintf(stderr, \"lexical error.\\n\");  \n    exit(1);  \n}  \n%%\n```\ncalculator.y源码\n```cpp\n%{  \n#include<stdio.h>  \n#include<stdlib.h>  \n#define YYDEBUG 1  \n%}  \n%union {  \nint int_value;  \ndouble double_value;  \n}  \n%token <double_value> DOUBLE_LITERAL  \n%token ADD SUB MUL DIV CR  \n%type <double_value> expression term primary_expression  \n%%  \nline_list  \n    : line  \n    | line_list line  \n    ;  \nline  \n    : expression CR  \n    {  \n        printf(\">>%lf\\n\",$1);  \n    }  \nexpression  \n    : term  \n    | expression ADD term  \n    {  \n        $$=$1+$3;  \n    }  \n    | expression SUB term  \n    {  \n        $$=$1-$3;  \n    }  \n    ;  \nterm  \n    : primary_expression  \n    | term MUL primary_expression  \n    {  \n        $$=$1*$3;  \n    }  \n    | term DIV primary_expression  \n    {  \n        $$=$1/$3;  \n    }  \n    ;  \nprimary_expression  \n    : DOUBLE_LITERAL  \n    ;  \n%%  \nint  \nyyerror(char const *str)  \n{  \n    extern char *yytext;  \n    fprintf(stderr,\"parser error near %s\\n\",yytext);  \n    return 0;  \n}  \nint main(void)  \n{  \n    extern int yyparse(void);  \n    extern FILE *yyin;  \n      \n    yyin=stdin;  \n    if(yyparse()){  \n        fprintf(stderr,\"Error! Error! Error!\\n\");  \n        exit(1);  \n    }  \n}\n```\n\n\t操作命令\n\t$bison -ydv calculator.y\n\t$flex calculator.l\n\t$gcc -o calc y.tab.c lex.yy.c"
toc: false
date: 2019-01-25 08:04:17
description:
---

@[toc]

---

# lex和yacc简介

lex和yacc是自动编译C代码的工具,适合于解析简单语言.这些工具常用于编译器或者解释器的组成部分，或者用于读取配置文件.“lex”和“yacc”这两个名字所代表的也包括这些工具的 GNU 版本 flex 和 bison. lex 和 yacc 是一对配对工具。lex 将文件分解为成组的“记号（tokens）”，大体上类似于单词。yacc 接受 成组的记号，并将它们装配为高层次的结构，类似于句子。yacc 设计用来处理 lex 的输出，不过您也可以 编写自己的代码来完成此任务。同样，lex 的输出很大程度上设计用于为某类解析器提供数据。

# lex使用
[Lex语法分析](http://www.kuqin.com/shuoit/20160526/352209.html)
# yacc使用

# 实例应用
使用的是linux系统下的flex和bison,它们是lex和yacc的加强版.
calculator.l的源码

```cpp
%{  
#include <stdio.h>  
#include "y.tab.h"  
  
int  
yywrap(void)  
{  
    return 1;  
}  
%}  
%%  
"+"             return ADD;  
"-"             return SUB;  
"*"             return MUL;  
"/"             return DIV;  
"\n"            return CR;  
([1-9][0-9]*)|0|([0-9]+\.[0-9]*) {  
    double temp;  
    sscanf(yytext, "%lf", &temp);  
    yylval.double_value = temp;  
    return DOUBLE_LITERAL;  
}  
[ \t] ;  
. {  
    fprintf(stderr, "lexical error.\n");  
    exit(1);  
}  
%%
```
calculator.y源码
```cpp
%{  
#include<stdio.h>  
#include<stdlib.h>  
#define YYDEBUG 1  
%}  
%union {  
int int_value;  
double double_value;  
}  
%token <double_value> DOUBLE_LITERAL  
%token ADD SUB MUL DIV CR  
%type <double_value> expression term primary_expression  
%%  
line_list  
    : line  
    | line_list line  
    ;  
line  
    : expression CR  
    {  
        printf(">>%lf\n",$1);  
    }  
expression  
    : term  
    | expression ADD term  
    {  
        $$=$1+$3;  
    }  
    | expression SUB term  
    {  
        $$=$1-$3;  
    }  
    ;  
term  
    : primary_expression  
    | term MUL primary_expression  
    {  
        $$=$1*$3;  
    }  
    | term DIV primary_expression  
    {  
        $$=$1/$3;  
    }  
    ;  
primary_expression  
    : DOUBLE_LITERAL  
    ;  
%%  
int  
yyerror(char const *str)  
{  
    extern char *yytext;  
    fprintf(stderr,"parser error near %s\n",yytext);  
    return 0;  
}  
int main(void)  
{  
    extern int yyparse(void);  
    extern FILE *yyin;  
      
    yyin=stdin;  
    if(yyparse()){  
        fprintf(stderr,"Error! Error! Error!\n");  
        exit(1);  
    }  
}
```

	操作命令
	$bison -ydv calculator.y
	$flex calculator.l
	$gcc -o calc y.tab.c lex.yy.c