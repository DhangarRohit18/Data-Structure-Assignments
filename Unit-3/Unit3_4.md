# Unit III Assignment 4: Balanced Parentheses Checker using Stack

Implementation to check whether parentheses in a string are balanced using stack data structure.

## Problem Statement

You are given a string containing only parentheses characters: '(', ')', '{', '}', '[', and ']'. Your task is to check whether the parentheses are balanced or not.

A string is considered balanced if:
1. Every opening bracket has a corresponding closing bracket of the same type
2. Brackets are closed in the correct order

## Pseudo Code

### Stack Structure
```
Structure CharStack:
    items: array of characters
    top: integer
    size: integer
```

### Is Matching Pair
```
Algorithm IsMatchingPair(opening, closing):
    If opening == '(' AND closing == ')': Return true
    If opening == '{' AND closing == '}': Return true
    If opening == '[' AND closing == ']': Return true
    Return false
```

### Is Opening Bracket
```
Algorithm IsOpeningBracket(ch):
    Return ch is one of '(', '{', '['
```

### Is Closing Bracket
```
Algorithm IsClosingBracket(ch):
    Return ch is one of ')', '}', ']'
```

### Check Balanced Parentheses
```
Algorithm CheckBalancedParentheses(expression):
    Initialize empty stack
    For each character in expression:
        If character is opening bracket:
            Push to stack
        Else If character is closing bracket:
            If stack is empty:
                Return false
            opening = Pop from stack
            If NOT IsMatchingPair(opening, character):
                Return false
    Return isEmpty(stack)
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_SIZE 100
struct CharStack_rrd {
    char items_rrd[MAX_SIZE];
    int top_rrd;
    int size_rrd;
};

struct CharStack_rrd* createStack_rrd();
int isEmpty_rrd(struct CharStack_rrd* stack_rrd);
int isFull_rrd(struct CharStack_rrd* stack_rrd);
int push_rrd(struct CharStack_rrd* stack_rrd, char item_rrd);
char pop_rrd(struct CharStack_rrd* stack_rrd);
char peek_rrd(struct CharStack_rrd* stack_rrd);
int isOpeningBracket_rrd(char ch_rrd);
int isClosingBracket_rrd(char ch_rrd);
int isMatchingPair_rrd(char opening_rrd, char closing_rrd);
int isValidExpression_rrd(char expression_rrd[]);
int checkBalancedParentheses_rrd(char expression_rrd[]);
void countBrackets_rrd(char expression_rrd[]);
void findUnmatchedBrackets_rrd(char expression_rrd[]);
void displayMenu_rrd();
struct CharStack_rrd* createStack_rrd() {
    struct CharStack_rrd* stack_rrd = (struct CharStack_rrd*)malloc(sizeof(struct CharStack_rrd));
    stack_rrd->top_rrd = -1;
    stack_rrd->size_rrd = MAX_SIZE;
    return stack_rrd;
}

int isEmpty_rrd(struct CharStack_rrd* stack_rrd) {
    return stack_rrd->top_rrd == -1;
}

int isFull_rrd(struct CharStack_rrd* stack_rrd) {
    return stack_rrd->top_rrd == MAX_SIZE - 1;
}

int push_rrd(struct CharStack_rrd* stack_rrd, char item_rrd) {
    if (isFull_rrd(stack_rrd))
{
        printf("Stack Overflow!\n");
        return 0;
    }

    stack_rrd->items_rrd[++stack_rrd->top_rrd] = item_rrd;
    return 1;
}

char pop_rrd(struct CharStack_rrd* stack_rrd)
{
    if (isEmpty_rrd(stack_rrd))
{
        printf("Stack Underflow!\n");
        return '\0';
    }
    return stack_rrd->items_rrd[stack_rrd->top_rrd--];
}

char peek_rrd(struct CharStack_rrd* stack_rrd)
{
    if (isEmpty_rrd(stack_rrd))
{
        return '\0';
    }
    return stack_rrd->items_rrd[stack_rrd->top_rrd];
}

int isOpeningBracket_rrd(char ch_rrd) {
    return (ch_rrd == '(' || ch_rrd == '{' || ch_rrd == '[');
}

int isClosingBracket_rrd(char ch_rrd) {
    return (ch_rrd == ')' || ch_rrd == '}' || ch_rrd == ']');
}

int isMatchingPair_rrd(char opening_rrd, char closing_rrd) {
    if (opening_rrd == '(' && closing_rrd == ')') return 1;
    if (opening_rrd == '{' && closing_rrd == '}') return 1;
    if (opening_rrd == '[' && closing_rrd == ']') return 1;
    return 0;
}

int isValidExpression_rrd(char expression_rrd[]) {
    int len_rrd = strlen(expression_rrd);
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        char ch_rrd = expression_rrd[i_rrd];
        if (!isOpeningBracket_rrd(ch_rrd) && !isClosingBracket_rrd(ch_rrd))
{
            return 0;
        }
    }
    return 1;
}

int checkBalancedParentheses_rrd(char expression_rrd[]) {
    struct CharStack_rrd* stack_rrd = createStack_rrd();
    int len_rrd = strlen(expression_rrd);
    printf("\nChecking expression: %s\n", expression_rrd);
    printf("Step-by-step process:\n");
    printf("Step\tCharacter\tStack\t\tStatus\n");
    printf("----\t---------\t-----\t\t------\n");
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        char ch_rrd = expression_rrd[i_rrd];
        if (isOpeningBracket_rrd(ch_rrd))
{
            if (!push_rrd(stack_rrd, ch_rrd))
{
                free(stack_rrd);
                return 0;
            }
        } else if (isClosingBracket_rrd(ch_rrd))
{
            if (isEmpty_rrd(stack_rrd))
{
                printf("%d\t%c\t\t(empty)\t\tUnbalanced - No matching opening bracket\n", i_rrd + 1, ch_rrd);
                free(stack_rrd);
                return 0;
            }

            char opening_rrd = pop_rrd(stack_rrd);
            if (!isMatchingPair_rrd(opening_rrd, ch_rrd))
{
                printf("%d\t%c\t\t", i_rrd + 1, ch_rrd);
                if (isEmpty_rrd(stack_rrd))
{
                    printf("(empty)\t\t");
                } else {
                    for (int j_rrd = 0; j_rrd <= stack_rrd->top_rrd; j_rrd++)
{
                        printf("%c", stack_rrd->items_rrd[j_rrd]);
                    }

                    printf("\t\t");
                }

                printf("Unbalanced - Mismatched brackets (%c and %c)\n", opening_rrd, ch_rrd);
                free(stack_rrd);
                return 0;
            }
        }

        printf("%d\t%c\t\t", i_rrd + 1, ch_rrd);
        if (isEmpty_rrd(stack_rrd))
{
            printf("(empty)\t\t");
        } else {
            for (int j_rrd = 0; j_rrd <= stack_rrd->top_rrd; j_rrd++)
{
                printf("%c", stack_rrd->items_rrd[j_rrd]);
            }

            printf("\t\t");
        }

        printf("Processing\n");
    }

    int isBalanced_rrd = isEmpty_rrd(stack_rrd);
    if (isBalanced_rrd)
{
        printf("Final\t-\t\t(empty)\t\tBalanced - All brackets matched\n");
    } else {
        printf("Final\t-\t\t");
        for (int j_rrd = 0; j_rrd <= stack_rrd->top_rrd; j_rrd++)
{
            printf("%c", stack_rrd->items_rrd[j_rrd]);
        }

        printf("\t\tUnbalanced - Unclosed brackets remaining\n");
    }

    free(stack_rrd);
    return isBalanced_rrd;
}

void countBrackets_rrd(char expression_rrd[]) {
    int roundOpen_rrd = 0, roundClose_rrd = 0;
    int curlyOpen_rrd = 0, curlyClose_rrd = 0;
    int squareOpen_rrd = 0, squareClose_rrd = 0;
    int len_rrd = strlen(expression_rrd);
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        switch (expression_rrd[i_rrd])
{
            case '(': roundOpen_rrd++; break;
            case ')': roundClose_rrd++; break;
            case '{': curlyOpen_rrd++; break;
            case '}': curlyClose_rrd++; break;
            case '[': squareOpen_rrd++; break;
            case ']': squareClose_rrd++; break;
        }
    }

    printf("\nBracket Count:\n");
    printf("Round brackets:  (%d opening, %d closing)\n", roundOpen_rrd, roundClose_rrd);
    printf("Curly brackets:  (%d opening, %d closing)\n", curlyOpen_rrd, curlyClose_rrd);
    printf("Square brackets: (%d opening, %d closing)\n", squareOpen_rrd, squareClose_rrd);
}

void findUnmatchedBrackets_rrd(char expression_rrd[]) {
    struct CharStack_rrd* stack_rrd = createStack_rrd();
    int len_rrd = strlen(expression_rrd);
    printf("\nUnmatched Brackets Analysis:\n");
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        char ch_rrd = expression_rrd[i_rrd];
        if (isOpeningBracket_rrd(ch_rrd))
{
            push_rrd(stack_rrd, ch_rrd);
        } else if (isClosingBracket_rrd(ch_rrd))

{
            if (isEmpty_rrd(stack_rrd))
{
                printf("Unmatched closing bracket '%c' at position %d\n", ch_rrd, i_rrd + 1);
            } else {
                char opening_rrd = pop_rrd(stack_rrd);
                if (!isMatchingPair_rrd(opening_rrd, ch_rrd))
{
                    printf("Mismatched brackets: '%c' at position %d and '%c' at position %d\n", 
                           opening_rrd, i_rrd, ch_rrd, i_rrd + 1);
                }
            }
        }
    }

    while (!isEmpty_rrd(stack_rrd))
{
        char unmatched_rrd = pop_rrd(stack_rrd);
        printf("Unmatched opening bracket '%c'\n", unmatched_rrd);
    }

    free(stack_rrd);
}

void generateBalancedParentheses_rrd(int n_rrd) {
    if (n_rrd <= 0)
{
        printf("Invalid number of pairs!\n");
        return;
    }

    printf("\nExample of balanced parentheses with %d pairs:\n", n_rrd);
    for (int i_rrd = 0; i_rrd < n_rrd; i_rrd++)
{
        printf("(");
    }

    for (int i_rrd = 0; i_rrd < n_rrd; i_rrd++)
{
        printf(")");
    }

    printf("\n");
    printf("Another example:\n");
    for (int i_rrd = 0; i_rrd < n_rrd; i_rrd++)
{
        printf("()");
    }

    printf("\n");
}

void displayMenu_rrd() {
    printf("\n===== Balanced Parentheses Checker =====\n");
    printf("1. Check Balanced Parentheses\n");
    printf("2. Count Bracket Types\n");
    printf("3. Find Unmatched Brackets\n");
    printf("4. Generate Balanced Parentheses Example\n");
    printf("5. Exit\n");
    printf("=======================================\n");
    printf("Enter your choice: ");
}

int main() {
    printf("Welcome to Balanced Parentheses Checker!\n");
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
{
{
                char expression_rrd[MAX_SIZE];
                printf("Enter parentheses expression: ");
                scanf("%s", expression_rrd);
                if (!isValidExpression_rrd(expression_rrd))
{
                    printf("Error: Expression contains invalid characters! Only (), {}, [] are allowed.\n");
                    break;
                }

                int isBalanced_rrd = checkBalancedParentheses_rrd(expression_rrd);
                if (isBalanced_rrd)
{
                    printf("\nResult: The parentheses are BALANCED.\n");
                } else
{

                    printf("\nResult: The parentheses are NOT BALANCED.\n");
                }
                break;
            }

{
                char expression_rrd[MAX_SIZE];
                printf("Enter parentheses expression: ");
                scanf("%s", expression_rrd);
                if (!isValidExpression_rrd(expression_rrd))
{
                    printf("Error: Expression contains invalid characters! Only (), {}, [] are allowed.\n");
                    break;
                }

                countBrackets_rrd(expression_rrd);
                break;
            }

{
                char expression_rrd[MAX_SIZE];
                printf("Enter parentheses expression: ");
                scanf("%s", expression_rrd);
                if (!isValidExpression_rrd(expression_rrd))
{
                    printf("Error: Expression contains invalid characters! Only (), {}, [] are allowed.\n");
                    break;
                }

                findUnmatchedBrackets_rrd(expression_rrd);
                break;
            }

{
                int n_rrd;
                printf("Enter number of pairs: ");
                scanf("%d", &n_rrd);
                generateBalancedParentheses_rrd(n_rrd);
                break;
            }

{
                printf("Thank you for using Balanced Parentheses Checker!\n");
                exit(0);
            }

{
                printf("Invalid choice! Please try again.\n");
            }
        }
    }
    return 0;
}
```

## Output

```
Welcome to Balanced Parentheses Checker!
===== Balanced Parentheses Checker =====
1. Check Balanced Parentheses
2. Count Bracket Types
3. Find Unmatched Brackets
4. Generate Balanced Parentheses Example
5. Exit
=======================================
Enter your choice: 1
Enter parentheses expression: ({[()]})
Checking expression: ({[()]})
Step-by-step process:
Step	Character	Stack		Status
----	---------	-----		------
1	(		(		Processing
2	{		({		Processing
3	[		({[		Processing
4	(		({[(		Processing
5	)		({[		Processing
6	]		({		Processing
7	}		(		Processing
8	)		(empty)		Processing
Final	-		(empty)		Balanced - All brackets matched
Result: The parentheses are BALANCED.
```

## Dry Run

For expression: ({[()]})

1. **Process '('**:
   - Opening bracket, push to stack
   - Stack: ['(']

2. **Process '{'**:
   - Opening bracket, push to stack
   - Stack: ['(', '{']

3. **Process '['**:
   - Opening bracket, push to stack
   - Stack: ['(', '{', '[']

4. **Process '('**:
   - Opening bracket, push to stack
   - Stack: ['(', '{', '[', '(']

5. **Process ')'**:
   - Closing bracket, pop from stack: '('
   - Check if matching pair: '(' and ')' → Yes
   - Stack: ['(', '{', '[']

6. **Process ']'**:
   - Closing bracket, pop from stack: '['
   - Check if matching pair: '[' and ']' → Yes
   - Stack: ['(', '{']

7. **Process '}'**:
   - Closing bracket, pop from stack: '{'
   - Check if matching pair: '{' and '}' → Yes
   - Stack: ['(']

8. **Process ')'**:
   - Closing bracket, pop from stack: '('
   - Check if matching pair: '(' and ')' → Yes
   - Stack: []

9. **Final Check**:
   - Stack is empty → Balanced

## Conclusion

The implementation demonstrates balanced parentheses checking using stack data structure. Key features include:

1. **Proper Bracket Matching**: Correctly identifies matching pairs of parentheses
2. **Order Validation**: Ensures brackets are closed in the correct order
3. **Step-by-step Visualization**: Shows the checking process in detail
4. **Comprehensive Analysis**: Provides additional analysis features

**Time Complexity**: O(n) where n is the length of the expression
- Each character is processed exactly once
- Stack operations (push/pop) are O(1)

**Space Complexity**: O(n) in worst case when all characters are opening brackets

The stack-based approach is ideal for this problem because:
1. **LIFO Nature**: Perfect for matching opening and closing brackets
2. **Natural Fit**: Bracket matching is a classic stack application
3. **Efficient Operations**: Push and pop are constant time operations
4. **Simple Logic**: Clear rules for when to push/pop

The implementation handles edge cases properly:
- Invalid characters in expressions
- Stack overflow and underflow conditions
- Empty expressions
- Mismatched brackets
- Unclosed brackets

Additional features beyond requirements:
- Bracket counting
- Unmatched bracket identification
- Example generation
- Detailed step-by-step process
- Comprehensive error handling

In real-world applications, this system could be extended to:
1. Support more bracket types
2. Handle nested expressions with operators
3. Integrate with code editors for real-time validation
4. Add position tracking for error reporting
5. Support multi-line expressions

The balanced parentheses problem is fundamental in:
1. **Compiler Design**: Parsing programming language syntax
2. **Text Editors**: Validating code structure
3. **Mathematical Expression Evaluation**: Ensuring proper formatting
4. **Data Validation**: Checking structured data formats

This implementation provides a solid foundation for understanding how stacks can be used to solve problems involving nested structures and matching pairs, which is a common pattern in computer science and software development.
