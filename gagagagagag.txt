1  #include <iostream> // Input/output operations 
2  #include <string> // String manipulation 
3  #include <cctype> // Character handling (isalpha, isdigit, isspace) 
4  
5  using namespace std; // Use standard namespace 
6  
7  string expr = "num1 * (temp + 42) - result2"; // Expression to analyze 
8  string token; // Current token 
9  char currentChar; // Current character 
10 int currentClass; // Current character type 
11 int currentPos = 0; // Current position in 'expr' 
12 
13 #define ID 1 // Identifier token type 
14 #define NUM 2 // Number token type 
15 #define OP 3 // Operator token type 
16 #define PAREN 4 // Parenthesis token type 
17 #define DONE -1 // End of input 
18 
19 void readChar() { // Read next character 
20     if (currentPos < expr.length()) { 
21         currentChar = expr[currentPos++]; 
22         if (isalpha(currentChar)) 
23             currentClass = ID; 
24         else if (isdigit(currentChar)) 
25             currentClass = NUM; 
26         else if (currentChar == '(' || currentChar == ')') 
27             currentClass = PAREN; 
28         else if (currentChar == '+' || currentChar == '-' || currentChar == '*' || currentChar == '/') 
29             currentClass = OP; 
30         else 
31             currentClass = -2; // Unknown 
32     } else { 
33         currentClass = DONE; 
34     } 
35 } 
36 
37 void skipSpaces() { // Skip whitespace 
38     while (isspace(currentChar)) 
39         readChar(); 
40 } 
41 
42 int scan() { // Identify and process next token 
43     token.clear(); 
44     skipSpaces(); 
45 
46     switch (currentClass) { 
47         case ID: // Identifier 
48             while (isalnum(currentChar)) { 
49                 token += currentChar; 
50                 readChar(); 
51             } 
52             cout << "Token: IDENTIFIER, Lexeme: " << token << endl; 
53             return ID; 
54 
55         case NUM: // Number 
56             while (isdigit(currentChar)) { 
57                 token += currentChar; 
58                 readChar(); 
59             } 
60             cout << "Token: INTEGER, Lexeme: " << token << endl; 
61             return NUM; 
62 
63         case OP: // Operator 
64             token += currentChar; 
65             cout << "Token: OPERATOR, Lexeme: " << token << endl; 
66             readChar(); 
67             return OP; 
68 
69         case PAREN: // Parenthesis 
70             token += currentChar; 
71             cout << "Token: PARENTHESIS, Lexeme: " << token << endl; 
72             readChar(); 
73             return PAREN; 
74 
75         case DONE: // End of input 
76             cout << "End of expression." << endl; 
77             return DONE; 
78 
79         default: // Unknown character 
80             cout << "Unknown character: " << currentChar << endl; 
81             readChar(); 
82             return -1; 
83     } 
84 } 
85 
86 int main() { // Main function 
87     readChar(); 
88     while (scan() != DONE); 
89     return 0; 
90 }



        case EOF_TOKEN:
            nextToken = EOF_TOKEN;
            strcpy(lexeme, "EOF");
            break;
    }

    cout << "Next token is: " << nextToken << ", Next lexeme is " << lexeme << endl;
    return nextToken;
}

int main() {
    cout << "Processing the expression: " << input << endl;
    currentIndex = 0;
    getChar();

    do {
        lex();
    } while (nextToken != EOF_TOKEN);

    return 0;
}



















