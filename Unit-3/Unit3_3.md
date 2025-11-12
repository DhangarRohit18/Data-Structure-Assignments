# Unit III Assignment 3: Multiple Stack Implementation using Array

Implementation of multiple stacks (more than two) using a single array.

## Problem Statement

Write a program to implement multiple stack i.e more than two stack using array and perform following operations on it:
A. Push
B. Pop
C. Stack Overflow
D. Stack Underflow
E. Display

## Pseudo Code

### Multiple Stack Structure
```
Structure MultipleStack:
    array: fixed size array
    tops: array to store top indices for each stack
    size: total size of array
    numStacks: number of stacks
    stackSize: size allocated to each stack
```

### Push Operation
```
Algorithm Push(stackNum, value):
    If stackNum is invalid:
        Return error
    If tops[stackNum] >= (stackNum+1) * stackSize - 1:
        Return "Stack Overflow"
    tops[stackNum]++
    array[tops[stackNum]] = value
```

### Pop Operation
```
Algorithm Pop(stackNum):
    If stackNum is invalid:
        Return error
    If tops[stackNum] < stackNum * stackSize:
        Return "Stack Underflow"
    value = array[tops[stackNum]]
    tops[stackNum]--
    Return value
```

### Display Stack
```
Algorithm DisplayStack(stackNum):
    If stackNum is invalid:
        Return error
    For i from tops[stackNum] down to stackNum * stackSize:
        Print array[i]
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_SIZE 100
#define MAX_STACKS 5
struct MultipleStack_rrd {
    int array_rrd[MAX_SIZE];
    int tops_rrd[MAX_STACKS];
    int size_rrd;
    int numStacks_rrd;
    int stackSize_rrd;
};

struct MultipleStack_rrd* createMultipleStack_rrd(int numStacks_rrd);
int isEmpty_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
int isFull_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
int push_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int value_rrd);
int pop_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* poppedValue_rrd);
int peek_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* peekedValue_rrd);
void displayStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
void displayAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd);
int getStackSize_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
int areAllStacksEmpty_rrd(struct MultipleStack_rrd* mStack_rrd);
void clearStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd);
void clearAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd);
void freeMultipleStack_rrd(struct MultipleStack_rrd* mStack_rrd);
void demonstrateOperations_rrd(struct MultipleStack_rrd* mStack_rrd);
void displayMenu_rrd();
struct MultipleStack_rrd* createMultipleStack_rrd(int numStacks_rrd) {
    if (numStacks_rrd <= 0 || numStacks_rrd > MAX_STACKS)
{
        printf("Invalid number of stacks! Must be between 1 and %d.\n", MAX_STACKS);
        return NULL;
    }

    struct MultipleStack_rrd* mStack_rrd = (struct MultipleStack_rrd*)malloc(sizeof(struct MultipleStack_rrd));
    mStack_rrd->numStacks_rrd = numStacks_rrd;
    mStack_rrd->size_rrd = MAX_SIZE;
    mStack_rrd->stackSize_rrd = MAX_SIZE / numStacks_rrd;
    for (int i_rrd = 0; i_rrd < numStacks_rrd; i_rrd++)
{
        mStack_rrd->tops_rrd[i_rrd] = (i_rrd * mStack_rrd->stackSize_rrd) - 1;
    }

    printf("Multiple stack created with %d stacks, each of size %d\n", numStacks_rrd, mStack_rrd->stackSize_rrd);
    return mStack_rrd;
}

int isEmpty_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number!\n");
        return -1;
    }
    return mStack_rrd->tops_rrd[stackNum_rrd] < (stackNum_rrd * mStack_rrd->stackSize_rrd);
}

int isFull_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number!\n");
        return -1;
    }
    return mStack_rrd->tops_rrd[stackNum_rrd] >= ((stackNum_rrd + 1) * mStack_rrd->stackSize_rrd) - 1;
}

int push_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int value_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number! Please use stack number between 0 and %d.\n", mStack_rrd->numStacks_rrd - 1);
        return 0;
    }

    if (isFull_rrd(mStack_rrd, stackNum_rrd))
{
        printf("Stack Overflow! Stack %d is full.\n", stackNum_rrd);
        return 0;
    }

    mStack_rrd->tops_rrd[stackNum_rrd]++;
    mStack_rrd->array_rrd[mStack_rrd->tops_rrd[stackNum_rrd]] = value_rrd;
    printf("Value %d pushed to stack %d successfully!\n", value_rrd, stackNum_rrd);
    return 1;
}

int pop_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* poppedValue_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number! Please use stack number between 0 and %d.\n", mStack_rrd->numStacks_rrd - 1);
        return 0;
    }

    if (isEmpty_rrd(mStack_rrd, stackNum_rrd))
{
        printf("Stack Underflow! Stack %d is empty.\n", stackNum_rrd);
        return 0;
    }

    *poppedValue_rrd = mStack_rrd->array_rrd[mStack_rrd->tops_rrd[stackNum_rrd]];
    mStack_rrd->tops_rrd[stackNum_rrd]--;
    printf("Value %d popped from stack %d successfully!\n", *poppedValue_rrd, stackNum_rrd);
    return 1;
}

int peek_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd, int* peekedValue_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number! Please use stack number between 0 and %d.\n", mStack_rrd->numStacks_rrd - 1);
        return 0;
    }

    if (isEmpty_rrd(mStack_rrd, stackNum_rrd))
{
        printf("Stack %d is empty!\n", stackNum_rrd);
        return 0;
    }

    *peekedValue_rrd = mStack_rrd->array_rrd[mStack_rrd->tops_rrd[stackNum_rrd]];
    return 1;
}

void displayStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number! Please use stack number between 0 and %d.\n", mStack_rrd->numStacks_rrd - 1);
        return;
    }

    if (isEmpty_rrd(mStack_rrd, stackNum_rrd))
{
        printf("Stack %d is empty!\n", stackNum_rrd);
        return;
    }

    printf("Stack %d contents (top to bottom): ", stackNum_rrd);
    for (int i_rrd = mStack_rrd->tops_rrd[stackNum_rrd]; i_rrd >= (stackNum_rrd * mStack_rrd->stackSize_rrd); i_rrd--)
{
        printf("%d ", mStack_rrd->array_rrd[i_rrd]);
    }

    printf("\n");
}

void displayAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd) {
    printf("\n===== All Stacks =====\n");
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        printf("Stack %d: ", i_rrd);
        if (isEmpty_rrd(mStack_rrd, i_rrd))
{
            printf("Empty\n");
        } else
{

            for (int j_rrd = mStack_rrd->tops_rrd[i_rrd]; j_rrd >= (i_rrd * mStack_rrd->stackSize_rrd); j_rrd--)
{
                printf("%d ", mStack_rrd->array_rrd[j_rrd]);
            }

            printf("\n");
        }
    }

    printf("=====================\n");
}

int getStackSize_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number!\n");
        return -1;
    }
    return mStack_rrd->tops_rrd[stackNum_rrd] - (stackNum_rrd * mStack_rrd->stackSize_rrd) + 1;
}

int areAllStacksEmpty_rrd(struct MultipleStack_rrd* mStack_rrd) {
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        if (!isEmpty_rrd(mStack_rrd, i_rrd))
{
            return 0;
        }
    }
    return 1;
}

void clearStack_rrd(struct MultipleStack_rrd* mStack_rrd, int stackNum_rrd) {
    if (stackNum_rrd < 0 || stackNum_rrd >= mStack_rrd->numStacks_rrd)
{
        printf("Invalid stack number!\n");
        return;
    }

    mStack_rrd->tops_rrd[stackNum_rrd] = (stackNum_rrd * mStack_rrd->stackSize_rrd) - 1;
    printf("Stack %d cleared successfully!\n", stackNum_rrd);
}

void clearAllStacks_rrd(struct MultipleStack_rrd* mStack_rrd) {
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        clearStack_rrd(mStack_rrd, i_rrd);
    }

    printf("All stacks cleared successfully!\n");
}

void freeMultipleStack_rrd(struct MultipleStack_rrd* mStack_rrd) {
    free(mStack_rrd);
}

void demonstrateOperations_rrd(struct MultipleStack_rrd* mStack_rrd) {
    printf("\n===== Demonstration of Stack Operations =====\n");
    printf("\n1. Push Operations:\n");
    push_rrd(mStack_rrd, 0, 10);
    push_rrd(mStack_rrd, 0, 20);
    push_rrd(mStack_rrd, 1, 30);
    push_rrd(mStack_rrd, 1, 40);
    push_rrd(mStack_rrd, 2, 50);
    printf("\n2. Display Individual Stacks:\n");
    displayStack_rrd(mStack_rrd, 0);
    displayStack_rrd(mStack_rrd, 1);
    displayStack_rrd(mStack_rrd, 2);
    printf("\n3. Display All Stacks:\n");
    displayAllStacks_rrd(mStack_rrd);
    printf("\n4. Peek Operations:\n");
    int peekedValue_rrd;
    if (peek_rrd(mStack_rrd, 0, &peekedValue_rrd))
{
        printf("Top of stack 0: %d\n", peekedValue_rrd);
    }

    if (peek_rrd(mStack_rrd, 1, &peekedValue_rrd))
{
        printf("Top of stack 1: %d\n", peekedValue_rrd);
    }

    printf("\n5. Pop Operations:\n");
    int poppedValue_rrd;
    pop_rrd(mStack_rrd, 0, &poppedValue_rrd);
    pop_rrd(mStack_rrd, 1, &poppedValue_rrd);
    printf("\n6. Display After Pop Operations:\n");
    displayAllStacks_rrd(mStack_rrd);
    printf("\n7. Stack Size Information:\n");
    for (int i_rrd = 0; i_rrd < mStack_rrd->numStacks_rrd; i_rrd++)
{
        int size_rrd = getStackSize_rrd(mStack_rrd, i_rrd);
        if (size_rrd >= 0)
{
            printf("Size of stack %d: %d\n", i_rrd, size_rrd);
        }
    }
}

void displayMenu_rrd() {
    printf("\n===== Multiple Stack Operations =====\n");
    printf("1. Push to Stack\n");
    printf("2. Pop from Stack\n");
    printf("3. Peek at Stack\n");
    printf("4. Display Stack\n");
    printf("5. Display All Stacks\n");
    printf("6. Check if Stack is Empty\n");
    printf("7. Check if Stack is Full\n");
    printf("8. Get Stack Size\n");
    printf("9. Clear Stack\n");
    printf("10. Clear All Stacks\n");
    printf("11. Demonstrate Operations\n");
    printf("12. Exit\n");
    printf("====================================\n");
    printf("Enter your choice: ");
}

int main() {
    printf("Welcome to Multiple Stack Implementation!\n");
    int numStacks_rrd;
    printf("Enter the number of stacks to create (1-%d): ", MAX_STACKS);
    scanf("%d", &numStacks_rrd);
    struct MultipleStack_rrd* mStack_rrd = createMultipleStack_rrd(numStacks_rrd);
    if (mStack_rrd == NULL)
{
        return 1;
    }

    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
{
{
                int stackNum_rrd, value_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                printf("Enter value to push: ");
                scanf("%d", &value_rrd);
                push_rrd(mStack_rrd, stackNum_rrd, value_rrd);
                break;
            }

{
                int stackNum_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                int poppedValue_rrd;
                if (pop_rrd(mStack_rrd, stackNum_rrd, &poppedValue_rrd))
{
                    printf("Popped value: %d\n", poppedValue_rrd);
                }
                break;
            }

{
                int stackNum_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                int peekedValue_rrd;
                if (peek_rrd(mStack_rrd, stackNum_rrd, &peekedValue_rrd))
{
                    printf("Top value of stack %d: %d\n", stackNum_rrd, peekedValue_rrd);
                }
                break;
            }

{
                int stackNum_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                displayStack_rrd(mStack_rrd, stackNum_rrd);
                break;
            }

{
                displayAllStacks_rrd(mStack_rrd);
                break;
            }

{
                int stackNum_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                if (isEmpty_rrd(mStack_rrd, stackNum_rrd) == 1)
{
                    printf("Stack %d is empty.\n", stackNum_rrd);
                } else if (isEmpty_rrd(mStack_rrd, stackNum_rrd) == 0)

{
                    printf("Stack %d is not empty.\n", stackNum_rrd);
                }
                break;
            }

{
                int stackNum_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                if (isFull_rrd(mStack_rrd, stackNum_rrd) == 1)
{
                    printf("Stack %d is full.\n", stackNum_rrd);
                } else if (isFull_rrd(mStack_rrd, stackNum_rrd) == 0)

{
                    printf("Stack %d is not full.\n", stackNum_rrd);
                }
                break;
            }

{
                int stackNum_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                int size_rrd = getStackSize_rrd(mStack_rrd, stackNum_rrd);
                if (size_rrd >= 0)
{
                    printf("Size of stack %d: %d\n", stackNum_rrd, size_rrd);
                }
                break;
            }

{
                int stackNum_rrd;
                printf("Enter stack number (0-%d): ", mStack_rrd->numStacks_rrd - 1);
                scanf("%d", &stackNum_rrd);
                clearStack_rrd(mStack_rrd, stackNum_rrd);
                break;
            }

{
                clearAllStacks_rrd(mStack_rrd);
                break;
            }

{
                demonstrateOperations_rrd(mStack_rrd);
                break;
            }

{
                printf("Thank you for using Multiple Stack Implementation!\n");
                freeMultipleStack_rrd(mStack_rrd);
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
Welcome to Multiple Stack Implementation!
Enter the number of stacks to create (1-5): 3
Multiple stack created with 3 stacks, each of size 33
===== Multiple Stack Operations =====
1. Push to Stack
2. Pop from Stack
3. Peek at Stack
4. Display Stack
5. Display All Stacks
6. Check if Stack is Empty
7. Check if Stack is Full
8. Get Stack Size
9. Clear Stack
10. Clear All Stacks
11. Demonstrate Operations
12. Exit
====================================
Enter your choice: 11
===== Demonstration of Stack Operations =====
1. Push Operations:
Value 10 pushed to stack 0 successfully!
Value 20 pushed to stack 0 successfully!
Value 30 pushed to stack 1 successfully!
Value 40 pushed to stack 1 successfully!
Value 50 pushed to stack 2 successfully!
2. Display Individual Stacks:
Stack 0 contents (top to bottom): 20 10 
Stack 1 contents (top to bottom): 40 30 
Stack 2 contents (top to bottom): 50 
3. Display All Stacks:
===== All Stacks =====
Stack 0: 20 10 
Stack 1: 40 30 
Stack 2: 50 
=====================
4. Peek Operations:
Top of stack 0: 20
Top of stack 1: 40
5. Pop Operations:
Value 20 popped from stack 0 successfully!
Value 40 popped from stack 1 successfully!
6. Display After Pop Operations:
===== All Stacks =====
Stack 0: 10 
Stack 1: 30 
Stack 2: 50 
=====================
7. Stack Size Information:
Size of stack 0: 1
Size of stack 1: 1
Size of stack 2: 1
```

## Dry Run

For 3 stacks with array size 100:
- Stack 0: indices 0-32
- Stack 1: indices 33-65
- Stack 2: indices 66-98

1. **Push Operations**:
   - Push 10 to stack 0: tops[0] = -1 → 0, array[0] = 10
   - Push 20 to stack 0: tops[0] = 0 → 1, array[1] = 20
   - Push 30 to stack 1: tops[1] = 32 → 33, array[33] = 30
   - Push 40 to stack 1: tops[1] = 33 → 34, array[34] = 40
   - Push 50 to stack 2: tops[2] = 65 → 66, array[66] = 50

2. **Display Stack 0**:
   - Traverse from tops[0] (1) down to 0
   - Print array[1] (20), then array[0] (10)
   - Output: "20 10"

3. **Pop from Stack 1**:
   - Store array[tops[1]] = array[34] = 40
   - tops[1] = 34 → 33
   - Return 40

4. **Check if Stack 2 is Empty**:
   - tops[2] = 66, base index = 66
   - tops[2] >= base index, so not empty

5. **Check if Stack 0 is Full**:
   - tops[0] = 1, max index = 32
   - tops[0] < max index, so not full

## Conclusion

The implementation demonstrates multiple stack management using a single array. Key features include:

1. **Fixed Partitioning**: Each stack gets an equal portion of the array
2. **Independent Operations**: Each stack operates independently
3. **Complete Functionality**: All required stack operations plus additional utilities

**Time Complexities**:
- Push: O(1) - constant time operation
- Pop: O(1) - constant time operation
- Peek: O(1) - constant time operation
- Display: O(n) where n is the number of elements in the stack
- isEmpty/isFull: O(1) - simple index comparisons

**Space Complexity**: O(MAX_SIZE) for the array, O(numStacks) for the tops array

The fixed partitioning approach has advantages and disadvantages:

**Advantages**:
1. **Simple Implementation**: Easy to understand and implement
2. **No Memory Wastage**: Each stack gets exactly its allocated space
3. **Predictable Performance**: No interference between stacks
4. **Memory Efficient**: No extra pointers needed

**Disadvantages**:
1. **Rigid Allocation**: Space cannot be shared between stacks
2. **Potential Wastage**: If one stack grows large while others are small, space is wasted
3. **Limited Flexibility**: Cannot accommodate varying stack sizes dynamically

The implementation handles edge cases properly:
- Invalid stack numbers
- Stack overflow and underflow conditions
- Empty stack operations
- Memory management

Additional features beyond requirements:
- Stack size tracking
- Peek operation
- Clear individual/all stacks
- Comprehensive demonstration
- Detailed error handling

In real-world applications, this system could be extended to:
1. Implement flexible partitioning (variable size stacks)
2. Add dynamic resizing capabilities
3. Support different data types
4. Implement priority-based stack allocation
5. Add thread safety for concurrent access

The multiple stack implementation is useful in scenarios where:
1. Multiple independent data streams need to be managed
2. Memory needs to be partitioned for different purposes
3. Recursive algorithms with multiple state tracking are implemented
4. Compiler design for managing different symbol tables

This implementation provides a solid foundation for understanding how multiple data structures can coexist in a single memory space while maintaining their individual integrity and functionality.
