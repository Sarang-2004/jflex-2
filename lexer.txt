/* User code section: imports, class definitions, etc. */
import java.io.*;

%% 

/* Options and Declarations Section */
%class Lexer
%unicode
%public
%standalone

/* Regular Definitions (macros) */
DIGIT         = [0-9]
LETTER        = [a-zA-Z]
ID            = {LETTER}({LETTER}|{DIGIT})*
CHAR          = \'([^'\\\\]|\\\\.)*\'    /* Single-quoted characters */
COMMENT       = "//".*("\n"|"$")          /* Single-line comments */
MULTI_COMMENT = "/*".* "*/"                /* Multi-line comments */
ASSIGNMENT    = =
SEMICOLON     = ;
PLUS          = \+
MINUS         = -
MULTIPLY      = \*
DIVIDE        = \/
MODULO        = %
LPAREN        = \(
RPAREN        = \)
WHITESPACE    = [ \t]+ 


%% 

/* Rules Section */
<YYINITIAL> {
  {MULTI_COMMENT}    { /* Ignore multi-line comments */ }
  {COMMENT}          { /* Ignore single-line comments */ }
  {DIGIT}+           { System.out.println("DIGIT: " + yytext()); }
  {LETTER}+          { System.out.println("IDENTIFIER: " + yytext()); }
  {ID}               { System.out.println("IDENTIFIER: " + yytext()); }
  {CHAR}             { System.out.println("CHARACTER: " + yytext()); }
  {ASSIGNMENT}       { System.out.println("ASSIGNMENT: " + yytext()); }
  {SEMICOLON}        { System.out.println("SEMICOLON: " + yytext()); }
  {PLUS}             { System.out.println("PLUS: " + yytext()); }
  {MINUS}            { System.out.println("MINUS: " + yytext()); }
  {MULTIPLY}         { System.out.println("MULTIPLY: " + yytext()); }
  {DIVIDE}           { System.out.println("DIVIDE: " + yytext()); }
  {MODULO}           { System.out.println("MODULO: " + yytext()); }
  {LPAREN}           { System.out.println("LEFT PARENTHESIS: " + yytext()); }
  {RPAREN}           { System.out.println("RIGHT PARENTHESIS: " + yytext()); }
  {WHITESPACE}       { /* Ignore whitespace */ }
  .                  { System.out.println("Unknown character: " + yytext()); }
}
