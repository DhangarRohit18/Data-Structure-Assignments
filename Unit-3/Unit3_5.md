# Unit III Assignment 5: Postfix Expression Evaluator using Stack

Implementation to evaluate postfix expressions (Reverse Polish Notation) using stack data structure.

## Problem Statement

You are given a postfix expression (also known as Reverse Polish Notation) consisting of single-digit operands and binary operators (+, -, *, /). Your task is to evaluate the expression using stack and return its result.

## Pseudo Code

### Stack Structure
```
Structure IntStack:
    items: array of integers
    top: integer
    size: integer
```

### Is Operator
```
Algorithm IsOperator(symbol):
    Return symbol is one of '+', '-', '*', '/'
```

### Is Operand
```
Algorithm IsOperand(symbol):
    Return symbol is digit (0-9)
```

### Perform Operation
```
Algorithm PerformOperation(operator, operand1, operand2):
    Switch operator:
        Case '+': Return operand1 + operand2
        Case '-': Return operand1 - operand2
        Case '*': Return operand1 * operand2
        Case '/': 
            If operand2 is 0:
                Return error (division by zero)
            Return operand1 / operand2
```

### Evaluate Postfix
```
Algorithm EvaluatePostfix(expression):
    Initialize empty stack
    For each character in expression:
        If character is operand:
            Convert to integer and push to stack
        Else If character is operator:
            If stack has fewer than 2 elements:
                Return error (invalid expression)
            operand2 = Pop from stack
            operand1 = Pop from stack
            result = PerformOperation(character, operand1, operand2)
            Push result to stack
    If stack has exactly one element:
        Return that element
    Else:
        Return error (invalid expression)
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#define MAX_SIZE 100
struct IntStack_rrd {
    int items_rrd[MAX_SIZE];
    int top_rrd;
    int size_rrd;
};

struct IntStack_rrd* createStack_rrd();
int isEmpty_rrd(struct IntStack_rrd* stack_rrd);
int isFull_rrd(struct IntStack_rrd* stack_rrd);
int push_rrd(struct IntStack_rrd* stack_rrd, int item_rrd);
int pop_rrd(struct IntStack_rrd* stack_rrd, int* poppedValue_rrd);
int peek_rrd(struct IntStack_rrd* stack_rrd, int* peekedValue_rrd);
int isOperator_rrd(char ch_rrd);
int isOperand_rrd(char ch_rrd);
int isValidPostfix_rrd(char expression_rrd[]);
int performOperation_rrd(char operator_rrd, int operand1_rrd, int operand2_rrd, int* result_rrd);
int evaluatePostfix_rrd(char expression_rrd[], int* finalResult_rrd);
void displayMenu_rrd();
struct IntStack_rrd* createStack_rrd() {
    struct IntStack_rrd* stack_rrd = (struct IntStack_rrd*)malloc(sizeof(struct IntStack_rrd));
    stack_rrd->top_rrd = -1;
    stack_rrd->size_rrd = MAX_SIZE;
    return stack_rrd;
}

int isEmpty_rrd(struct IntStack_rrd* stack_rrd) {
    return stack_rrd->top_rrd == -1;
}

int isFull_rrd(struct IntStack_rrd* stack_rrd) {
    return stack_rrd->top_rrd == MAX_SIZE - 1;
}

int push_rrd(struct IntStack_rrd* stack_rrd, int item_rrd) {
    if (isFull_rrd(stack_rrd))
{
        printf("Stack Overflow! Cannot push %d\n", item_rrd);
        return 0;
    }

    stack_rrd->items_rrd[++stack_rrd->top_rrd] = item_rrd;
    return 1;
}

int pop_rrd(struct IntStack_rrd* stack_rrd, int* poppedValue_rrd) {
    if (isEmpty_rrd(stack_rrd))
{
        printf("Stack Underflow! Cannot pop from empty stack\n");
        return 0;
    }

    *poppedValue_rrd = stack_rrd->items_rrd[stack_rrd->top_rrd--];
    return 1;
}

int peek_rrd(struct IntStack_rrd* stack_rrd, int* peekedValue_rrd) {
    if (isEmpty_rrd(stack_rrd))
{
        return 0;
    }

    *peekedValue_rrd = stack_rrd->items_rrd[stack_rrd->top_rrd];
    return 1;
}

int isOperator_rrd(char ch_rrd) {
    return (ch_rrd == '+' || ch_rrd == '-' || ch_rrd == '*' || ch_rrd == '/');
}

int isOperand_rrd(char ch_rrd) {
    return (ch_rrd >= '0' && ch_rrd <= '9');
}

int isValidPostfix_rrd(char expression_rrd[]) {
    int len_rrd = strlen(expression_rrd);
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        char ch_rrd = expression_rrd[i_rrd];
        if (!isOperand_rrd(ch_rrd) && !isOperator_rrd(ch_rrd))
{
            return 0;
        }
    }

    int operandCount_rrd = 0;
    int operatorCount_rrd = 0;
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        if (isOperand_rrd(expression_rrd[i_rrd]))
{
            operandCount_rrd++;
        } else if (isOperator_rrd(expression_rrd[i_rrd]))

{
            operatorCount_rrd++;
        }
    }

    if (operandCount_rrd == 0 || operatorCount_rrd == 0)
{
        return 0;
    }
    return 1;
}

int performOperation_rrd(char operator_rrd, int operand1_rrd, int operand2_rrd, int* result_rrd) {
    switch (operator_rrd)
{
        case '+':
            *result_rrd = operand1_rrd + operand2_rrd;
            return 1;
        case '-':
            *result_rrd = operand1_rrd - operand2_rrd;
            return 1;
        case '*':
            *result_rrd = operand1_rrd * operand2_rrd;
            return 1;
        case '/':
            if (operand2_rrd == 0)
{
                printf("Error: Division by zero!\n");
                return 0;
            }

            *result_rrd = operand1_rrd / operand2_rrd;
            return 1;
        default:
            printf("Error: Invalid operator '%c'\n", operator_rrd);
            return 0;
    }
}

int evaluatePostfix_rrd(char expression_rrd[], int* finalResult_rrd) {
    struct IntStack_rrd* stack_rrd = createStack_rrd();
    int len_rrd = strlen(expression_rrd);
    printf("\nEvaluating postfix expression: %s\n", expression_rrd);
    printf("Step-by-step evaluation:\n");
    printf("Step\tCharacter\tStack\t\t\tOperation\n");
    printf("----\t---------\t-----\t\t\t---------\n");
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        char ch_rrd = expression_rrd[i_rrd];
        if (isOperand_rrd(ch_rrd))
{
            int operand_rrd = ch_rrd - '0';
            if (!push_rrd(stack_rrd, operand_rrd))
{
                free(stack_rrd);
                return 0;
            }

            printf("%d\t%c\t\t", i_rrd + 1, ch_rrd);
            if (isEmpty_rrd(stack_rrd))
{
                printf("(empty)\t\t\t");
            } else
{

                printf("[");
                for (int j_rrd = 0; j_rrd <= stack_rrd->top_rrd; j_rrd++)
{
                    printf("%d", stack_rrd->items_rrd[j_rrd]);
                    if (j_rrd < stack_rrd->top_rrd) printf(", ");
                    {
                }

                printf("]\t\t\t");
            }

            printf("Push %d\n", operand_rrd);
        } else if (isOperator_rrd(ch_rrd))

{
            if (stack_rrd->top_rrd < 1)
{
                printf("Error: Insufficient operands for operator '%c' at position %d\n", ch_rrd, i_rrd + 1);
                free(stack_rrd);
                return 0;
            }

            int operand2_rrd, operand1_rrd;
            if (!pop_rrd(stack_rrd, &operand2_rrd) || !pop_rrd(stack_rrd, &operand1_rrd))
{
                free(stack_rrd);
                return 0;
            }

            int result_rrd;
            if (!performOperation_rrd(ch_rrd, operand1_rrd, operand2_rrd, &result_rrd))
{
                free(stack_rrd);
                return 0;
            }

            if (!push_rrd(stack_rrd, result_rrd))
{
                free(stack_rrd);
                return 0;
            }

            printf("%d\t%c\t\t", i_rrd + 1, ch_rrd);
            if (isEmpty_rrd(stack_rrd))
{
                printf("(empty)\t\t\t");
            } else
{

                printf("[");
                for (int j_rrd = 0; j_rrd <= stack_rrd->top_rrd; j_rrd++)
{
                    printf("%d", stack_rrd->items_rrd[j_rrd]);
                    if (j_rrd < stack_rrd->top_rrd) printf(", ");
                    {
                }

                printf("]\t\t\t");
            }

            printf("%d %c %d = %d\n", operand1_rrd, ch_rrd, operand2_rrd, result_rrd);
        }
    }

    if (stack_rrd->top_rrd == 0)
{
        *finalResult_rrd = stack_rrd->items_rrd[0];
        printf("Final\t-\t\t[%d]\t\t\tResult: %d\n", *finalResult_rrd, *finalResult_rrd);
        free(stack_rrd);
        return 1;
    } else if (stack_rrd->top_rrd > 0)

{
        printf("Error: Invalid expression - %d operands remaining in stack\n", stack_rrd->top_rrd + 1);
        free(stack_rrd);
        return 0;
    } else
{

        printf("Error: Invalid expression - No result computed\n");
        free(stack_rrd);
        return 0;
    }
}

void infixToPostfix_rrd(char infix_rrd[], char postfix_rrd[]) {
    struct IntStack_rrd* stack_rrd = createStack_rrd();
    int i_rrd = 0, j_rrd = 0;
    while (infix_rrd[i_rrd] != '\0')
{
        char ch_rrd = infix_rrd[i_rrd];
        if (isOperand_rrd(ch_rrd))
{
            postfix_rrd[j_rrd++] = ch_rrd;
        } else if (ch_rrd == '(')

{
            push_rrd(stack_rrd, ch_rrd);
        } else if (ch_rrd == ')')

{
            int temp_rrd;
            while (!isEmpty_rrd(stack_rrd) && peek_rrd(stack_rrd, &temp_rrd) && temp_rrd != '(')
{
                pop_rrd(stack_rrd, &temp_rrd);
                postfix_rrd[j_rrd++] = temp_rrd;
            }

            int dummy_rrd;
            pop_rrd(stack_rrd, &dummy_rrd);
        } else if (isOperator_rrd(ch_rrd))

{
            int topOperator_rrd;
            while (!isEmpty_rrd(stack_rrd) && peek_rrd(stack_rrd, &topOperator_rrd) && 
            {
                   topOperator_rrd != '(' && 
                   ((ch_rrd == '+' || ch_rrd == '-') || (topOperator_rrd == '*' || topOperator_rrd == '/')))
{
                pop_rrd(stack_rrd, &topOperator_rrd);
                postfix_rrd[j_rrd++] = topOperator_rrd;
            }

            push_rrd(stack_rrd, ch_rrd);
        }

        i_rrd++;
    }

    int temp_rrd;
    while (!isEmpty_rrd(stack_rrd))
{
        pop_rrd(stack_rrd, &temp_rrd);
        postfix_rrd[j_rrd++] = temp_rrd;
    }

    postfix_rrd[j_rrd] = '\0';
    free(stack_rrd);
}

void generateSampleExpressions_rrd() {
    printf("\nSample Postfix Expressions:\n");
    printf("1. 23+     (Infix: 2+3)              = 5\n");
    printf("2. 234*+    (Infix: 2+(3*4))         = 14\n");
    printf("3. 23+4*    (Infix: (2+3)*4)         = 20\n");
    printf("4. 234*+5-  (Infix: (2+(3*4))-5)     = 9\n");
    printf("5. 23-45*+  (Infix: (2-3)+(4*5))     = 19\n");
    printf("6. 234+*5-  (Infix: (2*(3+4))-5)     = 9\n");
}

void analyzeExpression_rrd(char expression_rrd[]) {
    int operandCount_rrd = 0;
    int operatorCount_rrd = 0;
    int len_rrd = strlen(expression_rrd);
    for (int i_rrd = 0; i_rrd < len_rrd; i_rrd++)
{
        if (isOperand_rrd(expression_rrd[i_rrd]))
{
            operandCount_rrd++;
        } else if (isOperator_rrd(expression_rrd[i_rrd]))

{
            operatorCount_rrd++;
        }
    }

    printf("\nExpression Analysis:\n");
    printf("Length: %d characters\n", len_rrd);
    printf("Operands: %d\n", operandCount_rrd);
    printf("Operators: %d\n", operatorCount_rrd);
    printf("Complexity: %d operations\n", operatorCount_rrd);
    if (operandCount_rrd == operatorCount_rrd + 1)
{
        printf("Structure: Valid postfix expression\n");
    } else
{

        printf("Structure: Invalid postfix expression\n");
    }
}

void displayMenu_rrd() {
    printf("\n===== Postfix Expression Evaluator =====\n");
    printf("1. Evaluate Postfix Expression\n");
    printf("2. Analyze Expression\n");
    printf("3. Generate Sample Expressions\n");
    printf("4. Convert Infix to Postfix (Bonus)\n");
    printf("5. Exit\n");
    printf("=======================================\n");
    printf("Enter your choice: ");
}

int main() {
    printf("Welcome to Postfix Expression Evaluator!\n");
    printf("Note: This evaluator works with single-digit operands (0-9) and binary operators (+, -, *, /)\n");
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
{
{
                char expression_rrd[MAX_SIZE];
                printf("Enter postfix expression: ");
                scanf("%s", expression_rrd);
                if (!isValidPostfix_rrd(expression_rrd))
{
                    printf("Error: Invalid postfix expression!\n");
                    printf("Make sure expression contains only digits (0-9) and operators (+, -, *, /)\n");
                    break;
                }

                int result_rrd;
                if (evaluatePostfix_rrd(expression_rrd, &result_rrd))
{
                    printf("\nFinal Result: %d\n", result_rrd);
                } else
{

                    printf("\nEvaluation failed!\n");
                }
                break;
            }

{
                char expression_rrd[MAX_SIZE];
                printf("Enter postfix expression: ");
                scanf("%s", expression_rrd);
                if (!isValidPostfix_rrd(expression_rrd))
{
                    printf("Error: Invalid postfix expression!\n");
                    break;
                }

                analyzeExpression_rrd(expression_rrd);
                break;
            }

{
                generateSampleExpressions_rrd();
                break;
            }

{
                char infix_rrd[MAX_SIZE];
                char postfix_rrd[MAX_SIZE];
                printf("Enter infix expression: ");
                scanf("%s", infix_rrd);
                infixToPostfix_rrd(infix_rrd, postfix_rrd);
                printf("Postfix expression: %s\n", postfix_rrd);
                break;
            }

{
                printf("Thank you for using Postfix Expression Evaluator!\n");
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
Welcome to Postfix Expression Evaluator!
Note: This evaluator works with single-digit operands (0-9) and binary operators (+, -, *, /)
===== Postfix Expression Evaluator =====
1. Evaluate Postfix Expression
2. Analyze Expression
3. Generate Sample Expressions
4. Convert Infix to Postfix (Bonus)
5. Exit
=======================================
Enter your choice: 1
Enter postfix expression: 234*+
Evaluating postfix expression: 234*+
Step-by-step evaluation:
Step	Character	Stack			Operation
----	---------	-----			---------
1	2		[2]			Push 2
2	3		[2, 3]			Push 3
3	4		[2, 3, 4]		Push 4
4	*		[2, 12]			3 * 4 = 12
5	+		[14]			2 + 12 = 14
Final	-		[14]			Result: 14
Final Result: 14
```

## Dry Run

For postfix expression: 234*+

1. **Process '2'**:
   - Operand, convert to integer (2) and push to stack
   - Stack: [2]

2. **Process '3'**:
   - Operand, convert to integer (3) and push to stack
   - Stack: [2, 3]

3. **Process '4'**:
   - Operand, convert to integer (4) and push to stack
   - Stack: [2, 3, 4]

4. **Process '*'**:
   - Operator, pop two operands:
     * operand2 = 4 (top of stack)
     * operand1 = 3 (next in stack)
   - Perform operation: 3 * 4 = 12
   - Push result (12) to stack
   - Stack: [2, 12]

5. **Process '+'**:
   - Operator, pop two operands:
     * operand2 = 12 (top of stack)
     * operand1 = 2 (next in stack)
   - Perform operation: 2 + 12 = 14
   - Push result (14) to stack
   - Stack: [14]

6. **Final Check**:
   - Stack has exactly one element (14)
   - Return 14 as final result

## Conclusion

The implementation demonstrates postfix expression evaluation using stack data structure. Key features include:

1. **Proper Evaluation**: Correctly evaluates postfix expressions using stack operations
2. **Step-by-step Visualization**: Shows the evaluation process in detail
3. **Error Handling**: Comprehensive error checking for invalid expressions
4. **Division by Zero Protection**: Prevents arithmetic errors

**Time Complexity**: O(n) where n is the length of the postfix expression
- Each character is processed exactly once
- Stack operations (push/pop) are O(1)

**Space Complexity**: O(n) in worst case when all characters are operands

The stack-based approach is ideal for postfix evaluation because:
1. **Natural Fit**: Postfix evaluation is a classic stack application
2. **LIFO Nature**: Perfect for managing operand order
3. **Efficient Operations**: Push and pop are constant time operations
4. **Simple Logic**: Clear rules for when to push/pop

The implementation handles edge cases properly:
- Invalid characters in expressions
- Stack overflow and underflow conditions
- Insufficient operands for operators
- Division by zero errors
- Invalid expression structures

Additional features beyond requirements:
- Expression analysis
- Sample expression generation
- Infix to postfix conversion (bonus)
- Detailed step-by-step evaluation
- Comprehensive error handling

In real-world applications, this system could be extended to:
1. Support multi-digit operands
2. Handle more operators (power, modulo, etc.)
3. Add floating-point arithmetic
4. Implement expression optimization
5. Add graphical visualization of the process

Postfix notation (Reverse Polish Notation) is used in:
1. **Calculator Applications**: HP calculators famously used RPN
2. **Programming Languages**: Some functional languages use postfix
3. **Compiler Design**: Intermediate code generation
4. **Stack-based Virtual Machines**: Java bytecode, Python bytecode
5. **Mathematical Software**: For unambiguous expression evaluation

This implementation provides a solid foundation for understanding how stacks can be used to evaluate mathematical expressions, which is fundamental in compiler design and calculator applications.
