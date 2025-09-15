# Ex-1 IMPLEMENTATION-OF-SYMBOL-TABLE
# Register Number :2305001023
# Date : 01/09/2025
# AIM :
## To write a C program to implement a symbol table.
# ALGORITHM
1.	Start the program.
2.	Get the input from the user with the terminating symbol ‘$’.
3.	Allocate memory for the variable by dynamic memory allocation function.
4.	If the next character of the symbol is an operator then only the memory is allocated.
5.	While reading, the input symbol and memory address are inserted into the symbol table.
6.	The steps are repeated till ‘$’ is reached.
7.	To reach a variable, enter the variable to be searched and the symbol table has been checked for the corresponding variable, the variable along with its address is displayed as a result.
8.	Stop the program. 
# PROGRAM

```
%{
    int COMMENT = 0;
%}

identifier [a-zA-Z][a-zA-Z0-9]*

%%

#.*                            { printf("\n%s is a PREPROCESSOR DIRECTIVE", yytext); }

int | float | char | double | while | for | do | if |
break | continue | void | switch | case | long | struct | const | typedef | return | else |
goto                            { printf("\n\t%s is a KEYWORD", yytext); }

"/*"                           { COMMENT = 1; }
"*/"                           { COMMENT = 0; }

{identifier}\(                  { if (!COMMENT) printf("\n\nFUNCTION\n\t%s", yytext); }

\{                              { if (!COMMENT) printf("\n BLOCK BEGINS"); }
\}                              { if (!COMMENT) printf("\n BLOCK ENDS"); }

{identifier}(\[[0-9]*\])?       { if (!COMMENT) printf("\n %s IDENTIFIER", yytext); }

\".*\"                          { if (!COMMENT) printf("\n\t%s is a STRING", yytext); }

[0-9]+                          { if (!COMMENT) printf("\n\t%s is a NUMBER", yytext); }

\)(\;)?                         { 
                                    if (!COMMENT) { 
                                        printf("\n\t"); 
                                        ECHO; 
                                        printf("\n"); 
                                    } 
                                }

\(                              { ECHO; }

=                               { if (!COMMENT) printf("\n\t%s is an ASSIGNMENT OPERATOR", yytext); }

\<= | \>= | \< | == | \>        { if (!COMMENT) printf("\n\t%s is a RELATIONAL OPERATOR", yytext); }

%%

int main(int argc, char **argv)
{
    if (argc > 1)
    {
        FILE *file;
        file = fopen(argv[1], "r");
        if (!file)
        {
            printf("could not open %s \n", argv[1]);
            exit(0);
        }
        yyin = file;
    }
    yylex();
    printf("\n\n");
    return 0;
}

int yywrap()
{
    return 0;
}

```
# OUTPUT
<img width="1459" height="893" alt="image" src="https://github.com/user-attachments/assets/0a603a5c-120a-4bc5-8182-f9f3153da870" />

# RESULT
### The program to implement a symbol table is executed and the output is verified.
