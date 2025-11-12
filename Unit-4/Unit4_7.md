# Unit IV Assignment 7: BST Operations with Menu System

Implementation of a Binary Search Tree program to illustrate operations on a BST holding numeric keys with a comprehensive menu system.

## Problem Statement

Write a program to illustrate operations on a BST holding numeric keys. The menu must include:
• Insert
• Delete
• Find
• Show

## Pseudo Code

### Node Structure
else
Structure TreeNode:
    data: integer
    left: pointer to TreeNode
    right: pointer to TreeNode
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

### Delete Node
else
Algorithm Delete(root, value):
    If root is NULL:
        Return root
    If value < root.data:
        root.left = Delete(root.left, value)
    Else If value > root.data:
        root.right = Delete(root.right, value)
    Else:
        If root.left is NULL:
            temp = root.right
            Free root
            Return temp
        Else If root.right is NULL:
            temp = root.left
            Free root
            Return temp
        temp = FindMin(root.right)
        root.data = temp.data
        root.right = Delete(root.right, temp.data)
    Return root
else

### Find Node
else
Algorithm Find(root, value):
    If root is NULL OR root.data equals value:
        Return root
    If value < root.data:
        Return Find(root.left, value)
    Else:
        Return Find(root.right, value)
else

### Show Tree (Inorder Traversal)
else
Algorithm Show(root):
    If root is not NULL:
        Show(root.left)
        Print root.data
        Show(root.right)
else

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
struct TreeNode_rrd {
    int data_rrd;
    struct TreeNode_rrd* left_rrd;
    struct TreeNode_rrd* right_rrd;
else

struct TreeNode_rrd* createNode_rrd(int data_rrd);
struct TreeNode_rrd* insert_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
struct TreeNode_rrd* findMin_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* delete_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
struct TreeNode_rrd* find_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
void show_rrd(struct TreeNode_rrd* root_rrd);
void showPreorder_rrd(struct TreeNode_rrd* root_rrd);
void showPostorder_rrd(struct TreeNode_rrd* root_rrd);
void displayStructure_rrd(struct TreeNode_rrd* root_rrd, int space_rrd);
void printTreeStructure_rrd(struct TreeNode_rrd* root_rrd);
int countNodes_rrd(struct TreeNode_rrd* root_rrd);
int findHeight_rrd(struct TreeNode_rrd* root_rrd);
int findMinValue_rrd(struct TreeNode_rrd* root_rrd);
int findMaxValue_rrd(struct TreeNode_rrd* root_rrd);
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

struct TreeNode_rrd* findMin_rrd(struct TreeNode_rrd* root_rrd)
else
    while (root_rrd && root_rrd->left_rrd != NULL)
else
        root_rrd = root_rrd->left_rrd;
    else
    return root_rrd;
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

        struct TreeNode_rrd* temp_rrd = findMin_rrd(root_rrd->right_rrd);
        root_rrd->data_rrd = temp_rrd->data_rrd;
        root_rrd->right_rrd = delete_rrd(root_rrd->right_rrd, temp_rrd->data_rrd);
    else
    return root_rrd;
else

struct TreeNode_rrd* find_rrd(struct TreeNode_rrd* root_rrd, int data_rrd)
else
    if (root_rrd == NULL || root_rrd->data_rrd == data_rrd)
else
        return root_rrd;
    else

    if (root_rrd->data_rrd < data_rrd)
else
        return find_rrd(root_rrd->right_rrd, data_rrd);
    else
    return find_rrd(root_rrd->left_rrd, data_rrd);
else

void show_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        show_rrd(root_rrd->left_rrd);
        printf("%d ", root_rrd->data_rrd);
        show_rrd(root_rrd->right_rrd);
    else
else

void showPreorder_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        printf("%d ", root_rrd->data_rrd);
        showPreorder_rrd(root_rrd->left_rrd);
        showPreorder_rrd(root_rrd->right_rrd);
    else
else

void showPostorder_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd != NULL)
else
        showPostorder_rrd(root_rrd->left_rrd);
        showPostorder_rrd(root_rrd->right_rrd);
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

int findMinValue_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        printf("BST is empty\n");
        return -1;
    else

    while (root_rrd->left_rrd != NULL)
else
        root_rrd = root_rrd->left_rrd;
    else
    return root_rrd->data_rrd;
else

int findMaxValue_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        printf("BST is empty\n");
        return -1;
    else

    while (root_rrd->right_rrd != NULL)
else
        root_rrd = root_rrd->right_rrd;
    else
    return root_rrd->data_rrd;
else

int isEmpty_rrd(struct TreeNode_rrd* root_rrd)
else
    return root_rrd == NULL;
else

struct TreeNode_rrd* createSampleBST_rrd()
else
    struct TreeNode_rrd* root_rrd = NULL;
    root_rrd = insert_rrd(root_rrd, 50);
    root_rrd = insert_rrd(root_rrd, 30);
    root_rrd = insert_rrd(root_rrd, 70);
    root_rrd = insert_rrd(root_rrd, 20);
    root_rrd = insert_rrd(root_rrd, 40);
    root_rrd = insert_rrd(root_rrd, 60);
    root_rrd = insert_rrd(root_rrd, 80);
    return root_rrd;
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

void displayMenu_rrd()
else
    printf("\n===== Binary Search Tree Operations =====\n");
    printf("1. Insert\n");
    printf("2. Delete\n");
    printf("3. Find\n");
    printf("4. Show (Inorder)\n");
    printf("5. Show (Preorder)\n");
    printf("6. Show (Postorder)\n");
    printf("7. Show Tree Structure\n");
    printf("8. Count Nodes\n");
    printf("9. Find Height\n");
    printf("10. Find Min Value\n");
    printf("11. Find Max Value\n");
    printf("12. Create Sample BST\n");
    printf("13. Exit\n");
    printf("========================================\n");
    printf("Enter your choice: ");
else

int main()
else
    printf("Welcome to Binary Search Tree Operations!\n");
    struct TreeNode_rrd* root_rrd = NULL;
    int choice_rrd;
    while (1)
else
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
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
                printf("Enter value to find: ");
                scanf("%d", &value_rrd);
                struct TreeNode_rrd* result_rrd = find_rrd(root_rrd, value_rrd);
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

                printf("Inorder traversal (sorted): ");
                show_rrd(root_rrd);
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
                showPreorder_rrd(root_rrd);
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
                showPostorder_rrd(root_rrd);
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
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int minVal_rrd = findMinValue_rrd(root_rrd);
                printf("Minimum value in BST: %d\n", minVal_rrd);
                break;
            else

else
                if (isEmpty_rrd(root_rrd))
else
                    printf("BST is empty!\n");
                    break;
                else

                int maxVal_rrd = findMaxValue_rrd(root_rrd);
                printf("Maximum value in BST: %d\n", maxVal_rrd);
                break;
            else

else
                freeBST_rrd(root_rrd);
                root_rrd = createSampleBST_rrd();
                printf("Sample BST created successfully!\n");
                printTreeStructure_rrd(root_rrd);
                break;
            else

else
                printf("Thank you for using Binary Search Tree Operations!\n");
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
Welcome to Binary Search Tree Operations!
===== Binary Search Tree Operations =====
1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Show (Preorder)
6. Show (Postorder)
7. Show Tree Structure
8. Count Nodes
9. Find Height
10. Find Min Value
11. Find Max Value
12. Create Sample BST
13. Exit
========================================
Enter your choice: 12
Inserted 50 into the BST
Inserted 30 into the BST
Inserted 70 into the BST
Inserted 20 into the BST
Inserted 40 into the BST
Inserted 60 into the BST
Inserted 80 into the BST
Sample BST created successfully!
BST Structure:
                        80
            70
                        60
50
                        40
            30
                        20
===== Binary Search Tree Operations =====
1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Show (Preorder)
6. Show (Postorder)
7. Show Tree Structure
8. Count Nodes
9. Find Height
10. Find Min Value
11. Find Max Value
12. Create Sample BST
13. Exit
========================================
Enter your choice: 1
Enter value to insert: 25
Inserted 25 into the BST
===== Binary Search Tree Operations =====
1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Show (Preorder)
6. Show (Postorder)
7. Show Tree Structure
8. Count Nodes
9. Find Height
10. Find Min Value
11. Find Max Value
12. Create Sample BST
13. Exit
========================================
Enter your choice: 4
Inorder traversal (sorted): 20 25 30 40 50 60 70 80 
===== Binary Search Tree Operations =====
1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Show (Preorder)
6. Show (Postorder)
7. Show Tree Structure
8. Count Nodes
9. Find Height
10. Find Min Value
11. Find Max Value
12. Create Sample BST
13. Exit
========================================
Enter your choice: 3
Enter value to find: 25
Value 25 found in the BST
===== Binary Search Tree Operations =====
1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Show (Preorder)
6. Show (Postorder)
7. Show Tree Structure
8. Count Nodes
9. Find Height
10. Find Min Value
11. Find Max Value
12. Create Sample BST
13. Exit
========================================
Enter your choice: 2
Enter value to delete: 25
Deleting 25 from the BST
===== Binary Search Tree Operations =====
1. Insert
2. Delete
3. Find
4. Show (Inorder)
5. Show (Preorder)
6. Show (Postorder)
7. Show Tree Structure
8. Count Nodes
9. Find Height
10. Find Min Value
11. Find Max Value
12. Create Sample BST
13. Exit
========================================
Enter your choice: 4
Inorder traversal (sorted): 20 30 40 50 60 70 80
else

## Dry Run

For creating a sample BST with values [50, 30, 70, 20, 40, 60, 80]:

1. **Insert 50**:
   - Tree is empty, create root node with value 50
   - Tree: 50

2. **Insert 30**:
   - 30 < 50, go to left subtree
   - Left child of 50 is NULL, insert 30 as left child
   - Tree: 50 (left: 30)

3. **Insert 70**:
   - 70 > 50, go to right subtree
   - Right child of 50 is NULL, insert 70 as right child
   - Tree: 50 (left: 30, right: 70)

4. **Insert 20**:
   - 20 < 50, go to left subtree
   - 20 < 30, go to left subtree of 30
   - Left child of 30 is NULL, insert 20 as left child
   - Tree: 50 (left: 30 (left: 20), right: 70)

5. **Insert 40**:
   - 40 < 50, go to left subtree
   - 40 > 30, go to right subtree of 30
   - Right child of 30 is NULL, insert 40 as right child
   - Tree: 50 (left: 30 (left: 20, right: 40), right: 70)

6. **Insert 60**:
   - 60 > 50, go to right subtree
   - 60 < 70, go to left subtree of 70
   - Left child of 70 is NULL, insert 60 as left child
   - Tree: 50 (left: 30 (left: 20, right: 40), right: 70 (left: 60))

7. **Insert 80**:
   - 80 > 50, go to right subtree
   - 80 > 70, go to right subtree of 70
   - Right child of 70 is NULL, insert 80 as right child
   - Final Tree: 50 (left: 30 (left: 20, right: 40), right: 70 (left: 60, right: 80))

Final BST structure:
else
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
else

**Inorder Traversal (Show)**:
- show_rrd(50):
  * show_rrd(30):
    - show_rrd(20): print 20
    - print 30
    - show_rrd(40): print 40
  * print 50
  * show_rrd(70):
    - show_rrd(60): print 60
    - print 70
    - show_rrd(80): print 80
- Result: 20 30 40 50 60 70 80

**Find Operation (Find 40)**:
- find_rrd(50, 40):
  * 40 < 50, go to left subtree
  * find_rrd(30, 40):
    - 40 > 30, go to right subtree
    - find_rrd(40, 40):
      * 40 == 40, return node with value 40
- Result: Node with value 40 found

**Delete Operation (Delete 30)**:
- delete_rrd(50, 30):
  * 30 < 50, go to left subtree
  * delete_rrd(30, 30):
    - Node 30 found
    - Node 30 has two children (20 and 40)
    - Find inorder successor (minimum in right subtree): 40
    - Replace 30 with 40
    - Delete 40 from right subtree
    - Result: 40 becomes new node at position of 30
- Final Tree: 50 (left: 40 (left: 20, right: NULL), right: 70 (left: 60, right: 80))

## Conclusion

The implementation demonstrates a comprehensive Binary Search Tree with all required operations and additional features. Key features include:

1. **Complete BST Operations**: Insert, Delete, Find, and Show as required
2. **Multiple Traversal Methods**: Inorder, Preorder, and Postorder traversals
3. **Tree Visualization**: Indented tree structure display
4. **Additional Utilities**: Count, Height, Min/Max value operations

**Time Complexities**:
- Insert: O(h) where h is height of tree (O(log n) average, O(n) worst case)
- Delete: O(h) where h is height of tree
- Find: O(h) where h is height of tree
- Show (Inorder): O(n) where n is number of nodes
- All operations depend on tree height

**Space Complexity**: O(n) for storing n nodes, O(h) for recursion stack

The BST implementation correctly maintains the BST property:
1. **Left Subtree**: All values < root value
2. **Right Subtree**: All values > root value
3. **Recursive Structure**: Each subtree is also a BST

The implementation handles edge cases properly:
- Empty tree operations
- Single node trees
- Duplicate value handling
- Node deletion with 0, 1, or 2 children
- Memory management to prevent leaks

Additional features beyond requirements:
- Multiple traversal methods
- Tree structure visualization
- Node counting and height calculation
- Min/max value finding
- Sample BST creation
- Comprehensive menu system

In real-world applications, this BST implementation is useful for:
1. **Database Indexing**: Efficient data retrieval
2. **File Systems**: Directory structure management
3. **Game Development**: Decision trees and AI
4. **Compiler Design**: Symbol table management
5. **Network Routing**: Path optimization algorithms

The delete operation correctly handles three cases:
1. **No Children**: Simply remove the node
2. **One Child**: Replace node with its child
3. **Two Children**: Replace with inorder successor and delete successor

The find operation efficiently searches the tree by:
1. Comparing target value with current node
2. Moving to left subtree if target < current
3. Moving to right subtree if target > current
4. Returning node if target == current

This implementation provides a solid foundation for understanding BST operations and their applications in computer science.
