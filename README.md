# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# REG NO: 212224040155
# Date: 19-09-2025
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
```
cdex3.l

%{
#include "y.tab.h"
%}

digit   [0-9]
%%
[ \t\n]+        ; // Ignore whitespace
{digit}+        { yylval = atoi(yytext); return NUMBER; }
[\+\-\*/]       { return *yytext; }
\(              { return '('; }
\)              { return ')'; }
.               { return 0; }
%%
int yywrap() { return 1; }
```
```
cdex3.y
%{
#include <stdio.h>
#include <stdlib.h>
void yyerror(const char *s);
int yylex(void);
%}

%token NUMBER

%%
expr:   expr '+' term
        | expr '-' term
        | term
        ;

term:   term '*' factor
        | term '/' factor
        | factor
        ;

factor: '(' expr ')'
        | NUMBER
        ;

%%

void yyerror(const char *s) {
    printf("Invalid arithmetic expression.\n");
}

int main() {
    printf("Enter an arithmetic expression: ");
    if (yyparse() == 0)
        printf("Valid arithmetic expression.\n");
    return 0;
}
```
# OUTPUT
<img width="1920" height="1080" alt="Screenshot (123)" src="https://github.com/user-attachments/assets/a4547fc0-9f16-4221-bb01-d231c9d831f1" />

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
