# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:06-11-2026
# Register Number :212225240046
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
## exp3_0046.l file
```


%{
#include "y.tab.h"
#include <stdio.h>
%}

%%

[0-9]+                  { return NUMBER; }
[a-zA-Z][a-zA-Z0-9]*    { return ID; }

"+"                     { return '+'; }
"-"                     { return '-'; }
"*"                     { return '*'; }
"/"                     { return '/'; }
"("                     { return '('; }
")"                     { return ')'; }
"="                     { return '='; }

[ \t]+                  ;

\n                      { return 0; }

.                       { return yytext[0]; }

%%

int yywrap()
{
    return 1;
}


```
## exp3_0046.y file
```

%{
#include <stdio.h>
#include <stdlib.h>

int yylex(void);
void yyerror(const char *s);
%}

%token NUMBER ID

%%

statement:
        expr '=' expr
      | expr
        ;

expr:
        expr '+' term
      | expr '-' term
      | term
      ;

term:
        term '*' factor
      | term '/' factor
      | factor
      ;

factor:
        '(' expr ')'
      | NUMBER
      | ID
      ;

%%

int main()
{
    printf("Enter Expression:\n");

    if (yyparse() == 0)
        printf("\nValid Arithmetic Expression\n");
    else
        printf("\nInvalid Arithmetic Expression\n");

    return 0;
}

void yyerror(const char *s)
{
}



```
# OUTPUT
<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/b1cc0c59-355a-4c6e-ab3b-20fa297d5195" />

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
