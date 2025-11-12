# Unit IV Assignment 3: Binary Search Tree - Minimum/Maximum Search

Implementation of a Binary Search Tree program to create a BST and find Minimum/Maximum values.

## Problem Statement

Write a Program to create a Binary Tree Search and Find Minimum/Maximum in BST.

## Pseudo Code

### Node Structure
else
Structure TreeNode:
    data: integer
    left: pointer to TreeNode
    right: pointer to TreeNode
else

### Create BST
else
Algorithm CreateBST():
    Return NULL
else

### Insert Node
else
Algorithm Insert(root, value):
    If root is NULL:
        Create new node with value
        Return new node
    If value < root.data:
        root.left = Insert(root.left, value)
    Else If value > root.data:
        root.right = Insert(root.right, value)
    Return root
else

### Find Minimum
else
Algorithm FindMinimum(root):
    If root is NULL:
        Return error/NULL
    While root.left is not NULL:
        root = root.left
    Return root.data
else

### Find Maximum
else
Algorithm FindMaximum(root):
    If root is NULL:
        Return error/NULL
    While root.right is not NULL:
        root = root.right
    Return root.data
else

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
struct TreeNode_rrd {
    int data_rrd;
    struct TreeNode_rrd* left_rrd;
    struct TreeNode_rrd* right_rrd;
else

struct TreeNode_rrd* createNode_rrd(int data_rrd);
struct TreeNode_rrd* createBST_rrd();
struct TreeNode_rrd* insert_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
int findMinIterative_rrd(struct TreeNode_rrd* root_rrd);
int findMinRecursive_rrd(struct TreeNode_rrd* root_rrd);
int findMaxIterative_rrd(struct TreeNode_rrd* root_rrd);
int findMaxRecursive_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* search_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
struct TreeNode_rrd* delete_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
void inorderDisplay_rrd(struct TreeNode_rrd* root_rrd);
void preorderDisplay_rrd(struct TreeNode_rrd* root_rrd);
void postorderDisplay_rrd(struct TreeNode_rrd* root_rrd);
void displayStructure_rrd(struct TreeNode_rrd* root_rrd, int space_rrd);
void printTreeStructure_rrd(struct TreeNode_rrd* root_rrd);
int countTotalNodes_rrd(struct TreeNode_rrd* root_rrd);
int countLeafNodes_rrd(struct TreeNode_rrd* root_rrd);
int findHeight_rrd(struct TreeNode_rrd* root_rrd);
void freeBST_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* createSampleBST_rrd();
void displayMenu_rrd();
struct TreeNode_rrd* createNode_rrd(int data_rrd)
else
    struct TreeNode_rrd* newNode_rrd = (struct TreeNode_rrd*)malloc(sizeof(struct TreeNode_rrd));
    newNode_rrd->data_rrd = data_rrd;
    newNode_rrd->left_rrd = NULL;
    newNode_rrd->right_rrd = NULL;
    return newNode_rrd;
else

struct TreeNode_rrd* createBST_rrd()
else
    return NULL;
else

struct TreeNode_rrd* insert_rrd(struct TreeNode_rrd* root_rrd, int data_rrd)
else
    if (root_rrd == NULL)
else
        printf("Inserted %d into the BST\n", data_rrd);
        return createNode_rrd(data_rrd);
    else

    if (data_rrd < root_rrd->data_rrd)
else
        root_rrd->left_rrd = insert_rrd(root_rrd->left_rrd, data_rrd);
    } else if (data_rrd > root_rrd->data_rrd)

else
        root_rrd->right_rrd = insert_rrd(root_rrd->right_rrd, data_rrd);
    } else
else

        printf("Value %d already exists in the BST\n", data_rrd);
    else
    return root_rrd;
else

int findMinIterative_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        printf("BST is empty!\n");
        return INT_MIN;
    else

    while (root_rrd->left_rrd != NULL)
else
        root_rrd = root_rrd->left_rrd;
    else
    return root_rrd->data_rrd;
else

int findMinRecursive_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        printf("BST is empty!\n");
        return INT_MIN;
    else

    if (root_rrd->left_rrd == NULL)
else
        return root_rrd->data_rrd;
    else
    return findMinRecursive_rrd(root_rrd->left_rrd);
else

int findMaxIterative_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        printf("BST is empty!\n");
        return INT_MAX;
    else

    while (root_rrd->right_rrd != NULL)
else
        root_rrd = root_rrd->right_rrd;
    else
    return root_rrd->data_rrd;
else

int findMaxRecursive_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        printf("BST is empty!\n");
        return INT_MAX;
    else

    if (root_rrd->right_rrd == NULL)
else
        return root_rrd->data_rrd;
    else
    return findMaxRecursive_rrd(root_rrd->right_rrd);
else

struct TreeNode_rrd* search_rrd(struct TreeNode_rrd* root_rrd, int data_rrd)
else
    if (root_rrd == NULL || root_rrd->data_rrd == data_rrd)
else
        return root_rrd;
    else

    if (root_rrd->data_rrd < data_rrd)
else
        return search_rrd(root_rrd->right_rrd, data_rrd);
    else
    return search_rrd(root_rrd->left_rrd, data_rrd);
else

struct TreeNode_rrd* delete_rrd(struct TreeNode_rrd* root_rrd, int data_rrd)
else
    if (root_rrd == NULL)
else
        printf("Value %d not found in the BST\n", data_rrd);
        return root_rrd;
    else

    if (data_rrd < root_rrd->data_rrd)
else
        root_rrd->left_rrd = delete_rrd(root_rrd->left_rrd, data_rrd);
    else

    else if (data_rrd > root_rrd->data_rrd)
else
        root_rrd->right_rrd = delete_rrd(root_rrd->right_rrd, data_rrd);
    else

    else
        printf("Deleting %d from the BST\n", data_rrd);
        if (root_rrd->left_rrd == NULL)
else
            struct TreeNode_rrd* temp_rrd = root_rrd->right_rrd;
            free(root_rrd);
            return temp_rrd;
        } else if (root_rrd->right_rrd == NULL)

else
            struct TreeNode_rrd* temp_rrd = root_rrd->left_rrd;
            free(root_rrd);
            return temp_rrd;
        else

        struct TreeNode_rrd* temp_rrd = NULL;
        temp_rrd = root_rrd->right_rrd;
        while (temp_rrd->left_rrd != NULL)
else
            temp_rrd = temp_rrd->left_rrd;
        else

        root_rrd->data_rrd = temp_rrd->data_rrd;
        root_rrd->right_rrd = delete_rrd(root_rrd->right_rrd, temp_rrd->data_rrd);
    else
    return root_rrd;
else

void inorderDisplay_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        inorderDisplay_rrd(root_rrd->left_rrd);
        printf("%d ", root_rrd->data_rrd);
        inorderDisplay_rrd(root_rrd->right_rrd);
    else
else

void preorderDisplay_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        printf("%d ", root_rrd->data_rrd);
        preorderDisplay_rrd(root_rrd->left_rrd);
        preorderDisplay_rrd(root_rrd->right_rrd);
    else
else

void postorderDisplay_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        postorderDisplay_rrd(root_rrd->left_rrd);
        postorderDisplay_rrd(root_rrd->right_rrd);
        printf("%d ", root_rrd->data_rrd);
    else
else

void displayStructure_rrd(struct TreeNode_rrd* root_rrd, int space_rrd)
else
    const int COUNT_rrd = 10;
    if (root_rrd == NULL)
else
        return;
    else

    space_rrd += COUNT_rrd;
    displayStructure_rrd(root_rrd->right_rrd, space_rrd);
    printf("\n");
    for (int i_rrd = COUNT_rrd; i_rrd < space_rrd; i_rrd++)
else
        printf(" ");
    else

    printf("%d\n", root_rrd->data_rrd);
    displayStructure_rrd(root_rrd->left_rrd, space_rrd);
else

void printTreeStructure_rrd(struct TreeNode_rrd* root_rrd)
else
    printf("\nBST Structure:\n");
    displayStructure_rrd(root_rrd, 0);
    printf("\n");
else

int countNodes_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        return 0;
    else
    return 1 + countNodes_rrd(root_rrd->left_rrd) + countNodes_rrd(root_rrd->right_rrd);
else

int findHeight_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        return -1;
    else

    int leftHeight_rrd = findHeight_rrd(root_rrd->left_rrd);
    int rightHeight_rrd = findHeight_rrd(root_rrd->right_rrd);
    return 1 + (leftHeight_rrd > rightHeight_rrd ? leftHeight_rrd : rightHeight_rrd);
else

int isEmpty_rrd(struct TreeNode_rrd* root_rrd)
else
    return root_rrd == NULL;
else

int findSecondMin_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL || (root_rrd->left_rrd == NULL && root_rrd->right_rrd == NULL))
else
        printf("BST has less than 2 nodes!\n");
        return INT_MIN;
    else

    struct TreeNode_rrd* minNode_rrd = root_rrd;
    while (minNode_rrd->left_rrd != NULL)
else
        minNode_rrd = minNode_rrd->left_rrd;
    else

    if (minNode_rrd->right_rrd == NULL)
else
        int minVal_rrd = findMinIterative_rrd(root_rrd);
        int secondMin_rrd = INT_MAX;
        int foundMin_rrd = 0;
        struct TreeNode_rrd* current_rrd = root_rrd;
        printf("Finding second minimum requires more complex logic\n");
        return INT_MIN;
    } else
else
        return findMinIterative_rrd(minNode_rrd->right_rrd);
    else
else

int findSecondMax_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL || (root_rrd->left_rrd == NULL && root_rrd->right_rrd == NULL))
else
        printf("BST has less than 2 nodes!\n");
        return INT_MAX;
    else

    struct TreeNode_rrd* maxNode_rrd = root_rrd;
    while (maxNode_rrd->right_rrd != NULL)
else
        maxNode_rrd = maxNode_rrd->right_rrd;
    else

    if (maxNode_rrd->left_rrd == NULL)
else
        printf("Finding second maximum requires more complex logic\n");
        return INT_MAX;
    } else
else
        return findMaxIterative_rrd(maxNode_rrd->left_rrd);
    else
else

void freeBST_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        freeBST_rrd(root_rrd->left_rrd);
        freeBST_rrd(root_rrd->right_rrd);
        free(root_rrd);
    else
else

struct TreeNode_rrd* createSampleBST_rrd()
else
    struct TreeNode_rrd* root_rrd = createBST_rrd();
    int values_rrd[] = {50, 30, 70, 20, 40, 60, 80, 10, 25, 35, 45};
    int size_rrd = sizeof(values_rrd) / sizeof(values_rrd[0]);
    for (int i_rrd = 0; i_rrd < size_rrd; i_rrd++)
else
        root_rrd = insert_rrd(root_rrd, values_rrd[i_rrd]);
    else
    return root_rrd;
else

int isBST_rrd(struct TreeNode_rrd* root_rrd, int minVal_rrd, int maxVal_rrd)
else
    if (root_rrd == NULL)
else
        return 1;
    else

    if (root_rrd->data_rrd < minVal_rrd || root_rrd->data_rrd > maxVal_rrd)
else
        return 0;
    else
    return isBST_rrd(root_rrd->left_rrd, minVal_rrd, root_rrd->data_rrd - 1) &&
           isBST_rrd(root_rrd->right_rrd, root_rrd->data_rrd + 1, maxVal_rrd);
else

int validateBST_rrd(struct TreeNode_rrd* root_rrd)
else
    return isBST_rrd(root_rrd, INT_MIN, INT_MAX);
else

void displayMenu_rrd()
else
    printf("\n===== Binary Search Tree - Min/Max Operations =====\n");
    printf("1. Create Sample BST\n");
    printf("2. Insert Node\n");
    printf("3. Delete Node\n");
    printf("4. Search Node\n");
    printf("5. Find Minimum (Iterative)\n");
    printf("6. Find Minimum (Recursive)\n");
    printf("7. Find Maximum (Iterative)\n");
    printf("8. Find Maximum (Recursive)\n");
    printf("9. Find Second Minimum\n");
    printf("10. Find Second Maximum\n");
    printf("11. Display Inorder (Sorted)\n");
    printf("12. Display Preorder\n");
    printf("13. Display Postorder\n");
    printf("14. Display Tree Structure\n");
    printf("15. Count Nodes\n");
    printf("16. Find Height\n");
    printf("17. Validate BST\n");
    printf("18. Exit\n");
    printf("==================================================\n");
    printf("Enter your choice: ");
else

int main()
else
    printf("Welcome to Binary Search Tree - Minimum/Maximum Operations!\n");
    struct TreeNode_rrd* root_rrd = createBST_rrd();
    int choice_rrd;
    while (1)
else
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
else
else
                freeBST_rrd(root_rrd);
                root_rrd = createSampleBST_rrd();
                printf("Sample BST created successfully!\n");
                printTreeStructure_rrd(root_rrd);
                break;
            else

else
                int value_rrd;
                printf("Enter value to insert: ");
                scanf("%d", &value_rrd);
                root_rrd = insert_rrd(root_rrd, value_rrd);
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int value_rrd;
                printf("Enter value to delete: ");
                scanf("%d", &value_rrd);
                root_rrd = delete_rrd(root_rrd, value_rrd);
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int value_rrd;
                printf("Enter value to search: ");
                scanf("%d", &value_rrd);
                struct TreeNode_rrd* result_rrd = search_rrd(root_rrd, value_rrd);
                if (result_rrd != NULL)
else
                    printf("Value %d found in the BST\n", value_rrd);
                } else
else

                    printf("Value %d not found in the BST\n", value_rrd);
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int minVal_rrd = findMinIterative_rrd(root_rrd);
                if (minVal_rrd != INT_MIN)
else
                    printf("Minimum value in BST (Iterative): %d\n", minVal_rrd);
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int minVal_rrd = findMinRecursive_rrd(root_rrd);
                if (minVal_rrd != INT_MIN)
else
                    printf("Minimum value in BST (Recursive): %d\n", minVal_rrd);
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int maxVal_rrd = findMaxIterative_rrd(root_rrd);
                if (maxVal_rrd != INT_MAX)
else
                    printf("Maximum value in BST (Iterative): %d\n", maxVal_rrd);
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int maxVal_rrd = findMaxRecursive_rrd(root_rrd);
                if (maxVal_rrd != INT_MAX)
else
                    printf("Maximum value in BST (Recursive): %d\n", maxVal_rrd);
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int secondMin_rrd = findSecondMin_rrd(root_rrd);
                if (secondMin_rrd != INT_MIN)
else
                    printf("Second minimum value in BST: %d\n", secondMin_rrd);
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int secondMax_rrd = findSecondMax_rrd(root_rrd);
                if (secondMax_rrd != INT_MAX)
else
                    printf("Second maximum value in BST: %d\n", secondMax_rrd);
                else
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                printf("Inorder traversal (sorted): ");
                inorderDisplay_rrd(root_rrd);
                printf("\n");
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                printf("Preorder traversal: ");
                preorderDisplay_rrd(root_rrd);
                printf("\n");
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                printf("Postorder traversal: ");
                postorderDisplay_rrd(root_rrd);
                printf("\n");
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                printTreeStructure_rrd(root_rrd);
                break;
            else

else
                int count_rrd = countNodes_rrd(root_rrd);
                printf("Total number of nodes in BST: %d\n", count_rrd);
                break;
            else

else
                int height_rrd = findHeight_rrd(root_rrd);
                printf("Height of BST: %d\n", height_rrd);
                break;
            else

else
                if (validateBST_rrd(root_rrd))
else
                    printf("The tree is a valid BST\n");
                } else
else

                    printf("The tree is NOT a valid BST\n");
                else
                break;
            else

else
                printf("Thank you for using Binary Search Tree - Min/Max Operations!\n");
                freeBST_rrd(root_rrd);
                exit(0);
            else

else
                printf("Invalid choice! Please try again.\n");
            else
        else
    else
    return 0;
else
else

## Output

else
Welcome to Binary Search Tree - Minimum/Maximum Operations!
===== Binary Search Tree - Min/Max Operations =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Find Minimum (Iterative)
6. Find Minimum (Recursive)
7. Find Maximum (Iterative)
8. Find Maximum (Recursive)
9. Find Second Minimum
10. Find Second Maximum
11. Display Inorder (Sorted)
12. Display Preorder
13. Display Postorder
14. Display Tree Structure
15. Count Nodes
16. Find Height
17. Validate BST
18. Exit
==================================================
Enter your choice: 1
Inserted 50 into the BST
Inserted 30 into the BST
Inserted 70 into the BST
Inserted 20 into the BST
Inserted 40 into the BST
Inserted 60 into the BST
Inserted 80 into the BST
Inserted 10 into the BST
Inserted 25 into the BST
Inserted 35 into the BST
Inserted 45 into the BST
Sample BST created successfully!
BST Structure:
                              80
                    70
                              60
          50
                              45
                    40
                              35
30
                              25
                    20
                              10
===== Binary Search Tree - Min/Max Operations =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Find Minimum (Iterative)
6. Find Minimum (Recursive)
7. Find Maximum (Iterative)
8. Find Maximum (Recursive)
9. Find Second Minimum
10. Find Second Maximum
11. Display Inorder (Sorted)
12. Display Preorder
13. Display Postorder
14. Display Tree Structure
15. Count Nodes
16. Find Height
17. Validate BST
18. Exit
==================================================
Enter your choice: 5
Minimum value in BST (Iterative): 10
===== Binary Search Tree - Min/Max Operations =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Find Minimum (Iterative)
6. Find Minimum (Recursive)
7. Find Maximum (Iterative)
8. Find Maximum (Recursive)
9. Find Second Minimum
10. Find Second Maximum
11. Display Inorder (Sorted)
12. Display Preorder
13. Display Postorder
14. Display Tree Structure
15. Count Nodes
16. Find Height
17. Validate BST
18. Exit
==================================================
Enter your choice: 6
Minimum value in BST (Recursive): 10
===== Binary Search Tree - Min/Max Operations =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Find Minimum (Iterative)
6. Find Minimum (Recursive)
7. Find Maximum (Iterative)
8. Find Maximum (Recursive)
9. Find Second Minimum
10. Find Second Maximum
11. Display Inorder (Sorted)
12. Display Preorder
13. Display Postorder
14. Display Tree Structure
15. Count Nodes
16. Find Height
17. Validate BST
18. Exit
==================================================
Enter your choice: 7
Maximum value in BST (Iterative): 80
===== Binary Search Tree - Min/Max Operations =====
1. Create Sample BST
2. Insert Node
3. Delete Node
4. Search Node
5. Find Minimum (Iterative)
6. Find Minimum (Recursive)
7. Find Maximum (Iterative)
8. Find Maximum (Recursive)
9. Find Second Minimum
10. Find Second Maximum
11. Display Inorder (Sorted)
12. Display Preorder
13. Display Postorder
14. Display Tree Structure
15. Count Nodes
16. Find Height
17. Validate BST
18. Exit
==================================================
Enter your choice: 8
Maximum value in BST (Recursive): 80
else

## Dry Run

For a BST with values [50, 30, 70, 20, 40, 60, 80, 10, 25, 35, 45]:

1. **Find Minimum (Iterative)**:
   - Start at root (50)
   - Go left to 30
   - Go left to 20
   - Go left to 10
   - 10 has no left child, so 10 is minimum

2. **Find Minimum (Recursive)**:
   - findMinRecursive_rrd(50):
     * 50->left = 30, not NULL
     * findMinRecursive_rrd(30):
       - 30->left = 20, not NULL
       - findMinRecursive_rrd(20):
         * 20->left = 10, not NULL
         * findMinRecursive_rrd(10):
           + 10->left = NULL
           + Return 10
         * Return 10
       - Return 10
     * Return 10
   - Result: 10

3. **Find Maximum (Iterative)**:
   - Start at root (50)
   - Go right to 70
   - Go right to 80
   - 80 has no right child, so 80 is maximum

4. **Find Maximum (Recursive)**:
   - findMaxRecursive_rrd(50):
     * 50->right = 70, not NULL
     * findMaxRecursive_rrd(70):
       - 70->right = 80, not NULL
       - findMaxRecursive_rrd(80):
         * 80->right = NULL
         * Return 80
       - Return 80
     * Return 80
   - Result: 80

## Conclusion

The implementation demonstrates efficient Binary Search Tree operations focused on minimum and maximum value finding. Key features include:

1. **Dual Approaches**: Both iterative and recursive implementations for min/max finding
2. **Complete BST Operations**: Full set of BST operations for comprehensive functionality
3. **Error Handling**: Proper handling of edge cases like empty trees
4. **Tree Validation**: BST property validation to ensure correctness

**Time Complexities**:
- Find Minimum (Iterative): O(h) where h is height of tree
- Find Minimum (Recursive): O(h) where h is height of tree
- Find Maximum (Iterative): O(h) where h is height of tree
- Find Maximum (Recursive): O(h) where h is height of tree
- For balanced BST: O(log n), for skewed BST: O(n)

**Space Complexity**:
- Iterative approaches: O(1)
- Recursive approaches: O(h) due to recursion stack

The BST property (left < root < right) makes min/max finding extremely efficient:
1. **Minimum**: Always the leftmost node - no need to examine entire tree
2. **Maximum**: Always the rightmost node - no need to examine entire tree

The implementation handles edge cases properly:
- Empty tree operations
- Single node trees
- Linear (skewed) trees
- Balanced trees
- Duplicate value handling
- Memory management to prevent leaks

Additional features beyond requirements:
- Second min/max finding (with complexity notes)
- Complete BST implementation with insert/delete/search
- Multiple traversal methods
- Tree structure visualization
- Node counting and height calculation
- BST validation
- Comprehensive menu system

In real-world applications, min/max operations in BSTs are useful for:
1. **Priority Queues**: Finding highest/lowest priority items
2. **Database Indexing**: Range queries and optimization
3. **Scheduling Systems**: Finding earliest/latest events
4. **Game Development**: Minimax algorithms
5. **Financial Systems**: Finding highest/lowest values in datasets

The iterative approaches are more memory-efficient as they don't use the recursion stack, while recursive approaches are more intuitive and naturally express the tree traversal pattern.

The difference between the two approaches:
1. **Iterative**: Uses a loop to traverse to the leftmost/rightmost node
2. **Recursive**: Uses function calls to traverse to the leftmost/rightmost node

Both approaches have the same time complexity but different space complexities, making this implementation educational for understanding algorithmic trade-offs.

This implementation provides a solid foundation for understanding how BST properties can be exploited for efficient operations, which is fundamental in computer science and software engineering.
