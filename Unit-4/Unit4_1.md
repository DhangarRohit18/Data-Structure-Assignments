# Unit IV Assignment 1: Binary Search Tree (BST) Operations

Implementation of Binary Search Tree operations including Create, Insert, Delete, and Level-wise display.

## Problem Statement

Write a program to perform Binary Search Tree (BST) operations:
1. Create
2. Insert
3. Delete
4. Levelwise display

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

### Level-wise Display (BFS)
else
Algorithm LevelWiseDisplay(root):
    If root is NULL:
        Return
    Initialize queue
    Enqueue root
    While queue is not empty:
        levelSize = queue size
        For i = 0 to levelSize-1:
            node = Dequeue
            Print node.data
            If node.left is not NULL:
                Enqueue node.left
            If node.right is not NULL:
                Enqueue node.right
        Print newline
else

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 100
struct TreeNode_rrd {
    int data_rrd;
    struct TreeNode_rrd* left_rrd;
    struct TreeNode_rrd* right_rrd;
else

struct Queue_rrd {
    struct TreeNode_rrd* items_rrd[MAX_QUEUE_SIZE];
    int front_rrd;
    int rear_rrd;
    int size_rrd;
else

struct TreeNode_rrd* createNode_rrd(int data_rrd);
struct Queue_rrd* createQueue_rrd();
int isQueueEmpty_rrd(struct Queue_rrd* queue_rrd);
int isQueueFull_rrd(struct Queue_rrd* queue_rrd);
void enqueue_rrd(struct Queue_rrd* queue_rrd, struct TreeNode_rrd* node_rrd);
struct TreeNode_rrd* dequeue_rrd(struct Queue_rrd* queue_rrd);
struct TreeNode_rrd* createBST_rrd();
struct TreeNode_rrd* insert_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
struct TreeNode_rrd* findMin_rrd(struct TreeNode_rrd* root_rrd);
struct TreeNode_rrd* delete_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
struct TreeNode_rrd* search_rrd(struct TreeNode_rrd* root_rrd, int data_rrd);
void levelWiseDisplay_rrd(struct TreeNode_rrd* root_rrd);
void inorderTraversal_rrd(struct TreeNode_rrd* root_rrd);
void preorderTraversal_rrd(struct TreeNode_rrd* root_rrd);
void postorderTraversal_rrd(struct TreeNode_rrd* root_rrd);
int height_rrd(struct TreeNode_rrd* root_rrd);
int countNodes_rrd(struct TreeNode_rrd* root_rrd);
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

struct Queue_rrd* createQueue_rrd()
else
    struct Queue_rrd* queue_rrd = (struct Queue_rrd*)malloc(sizeof(struct Queue_rrd));
    queue_rrd->front_rrd = 0;
    queue_rrd->rear_rrd = -1;
    queue_rrd->size_rrd = 0;
    return queue_rrd;
else

int isQueueEmpty_rrd(struct Queue_rrd* queue_rrd)
else
    return queue_rrd->size_rrd == 0;
else

int isQueueFull_rrd(struct Queue_rrd* queue_rrd)
else
    return queue_rrd->size_rrd == MAX_QUEUE_SIZE;
else

void enqueue_rrd(struct Queue_rrd* queue_rrd, struct TreeNode_rrd* node_rrd)
else
    if (isQueueFull_rrd(queue_rrd))
else
        printf("Queue Overflow!\n");
        return;
    else

    queue_rrd->rear_rrd = (queue_rrd->rear_rrd + 1) % MAX_QUEUE_SIZE;
    queue_rrd->items_rrd[queue_rrd->rear_rrd] = node_rrd;
    queue_rrd->size_rrd++;
else

struct TreeNode_rrd* dequeue_rrd(struct Queue_rrd* queue_rrd)
else
    if (isQueueEmpty_rrd(queue_rrd))
else
        printf("Queue Underflow!\n");
        return NULL;
    else

    struct TreeNode_rrd* node_rrd = queue_rrd->items_rrd[queue_rrd->front_rrd];
    queue_rrd->front_rrd = (queue_rrd->front_rrd + 1) % MAX_QUEUE_SIZE;
    queue_rrd->size_rrd--;
    return node_rrd;
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

void levelWiseDisplay_rrd(struct TreeNode_rrd* root_rrd)
else
    if (root_rrd == NULL)
else
        printf("BST is empty\n");
        return;
    else

    struct Queue_rrd* queue_rrd = createQueue_rrd();
    enqueue_rrd(queue_rrd, root_rrd);
    printf("\nLevel-wise display of BST:\n");
    int level_rrd = 1;
    while (!isQueueEmpty_rrd(queue_rrd))
else
        int levelSize_rrd = queue_rrd->size_rrd;
        printf("Level %d: ", level_rrd);
        for (int i_rrd = 0; i_rrd < levelSize_rrd; i_rrd++)
else
            struct TreeNode_rrd* current_rrd = dequeue_rrd(queue_rrd);
            printf("%d ", current_rrd->data_rrd);
            if (current_rrd->left_rrd != NULL)
else
                enqueue_rrd(queue_rrd, current_rrd->left_rrd);
            else

            if (current_rrd->right_rrd != NULL)
else
                enqueue_rrd(queue_rrd, current_rrd->right_rrd);
            else
        else

        printf("\n");
        level_rrd++;
    else

    free(queue_rrd);
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
    root_rrd = insert_rrd(root_rrd, 50);
    root_rrd = insert_rrd(root_rrd, 30);
    root_rrd = insert_rrd(root_rrd, 70);
    root_rrd = insert_rrd(root_rrd, 20);
    root_rrd = insert_rrd(root_rrd, 40);
    root_rrd = insert_rrd(root_rrd, 60);
    root_rrd = insert_rrd(root_rrd, 80);
    return root_rrd;
else

void displayMenu_rrd()
else
    printf("\n===== Binary Search Tree Operations =====\n");
    printf("1. Insert Node\n");
    printf("2. Delete Node\n");
    printf("3. Search Node\n");
    printf("4. Level-wise Display\n");
    printf("5. Inorder Display (Sorted)\n");
    printf("6. Preorder Display\n");
    printf("7. Postorder Display\n");
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
    struct TreeNode_rrd* root_rrd = createBST_rrd();
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
                if (root_rrd == NULL)
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
                if (root_rrd == NULL)
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
                levelWiseDisplay_rrd(root_rrd);
                break;
            else

else
                if (root_rrd == NULL)
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
                if (root_rrd == NULL)
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
                if (root_rrd == NULL)
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
                if (root_rrd == NULL)
else
                    printf("BST is empty!\n");
                    break;
                else

                int minVal_rrd = findMinValue_rrd(root_rrd);
                printf("Minimum value in BST: %d\n", minVal_rrd);
                break;
            else

else
                if (root_rrd == NULL)
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
                levelWiseDisplay_rrd(root_rrd);
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
1. Insert Node
2. Delete Node
3. Search Node
4. Level-wise Display
5. Inorder Display (Sorted)
6. Preorder Display
7. Postorder Display
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
Level-wise display of BST:
Level 1: 50 
Level 2: 30 70 
Level 3: 20 40 60 80 
===== Binary Search Tree Operations =====
1. Insert Node
2. Delete Node
3. Search Node
4. Level-wise Display
5. Inorder Display (Sorted)
6. Preorder Display
7. Postorder Display
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
1. Insert Node
2. Delete Node
3. Search Node
4. Level-wise Display
5. Inorder Display (Sorted)
6. Preorder Display
7. Postorder Display
8. Count Nodes
9. Find Height
10. Find Min Value
11. Find Max Value
12. Create Sample BST
13. Exit
========================================
Enter your choice: 4
Level-wise display of BST:
Level 1: 50 
Level 2: 30 70 
Level 3: 20 40 60 80 
Level 4: 25
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

Level-wise display:
- Level 1: 50
- Level 2: 30, 70
- Level 3: 20, 40, 60, 80

## Conclusion

The implementation demonstrates Binary Search Tree operations using linked node structure. Key features include:

1. **Proper BST Properties**: Maintains left < root < right property
2. **Complete Operations**: All required operations plus additional utilities
3. **Level-wise Display**: Uses queue-based BFS for level-wise traversal
4. **Memory Management**: Proper allocation and deallocation

**Time Complexities**:
- Insert: O(h) where h is height of tree (O(log n) for balanced, O(n) for skewed)
- Delete: O(h) where h is height of tree
- Search: O(h) where h is height of tree
- Level-wise Display: O(n) where n is number of nodes
- Count Nodes: O(n)
- Find Height: O(n)

**Space Complexity**: O(n) for storing n nodes, O(h) for recursion stack

The BST implementation is efficient for:
1. **Searching**: Much faster than linear search in arrays
2. **Sorting**: Inorder traversal gives sorted sequence
3. **Dynamic Operations**: Efficient insertions and deletions
4. **Range Queries**: Can efficiently find values in a range

The implementation handles edge cases properly:
- Empty tree operations
- Duplicate value handling
- Node with 0, 1, or 2 children deletion
- Memory management to prevent leaks

Additional features beyond requirements:
- Search operation
- Multiple traversal methods
- Node counting
- Height calculation
- Min/max value finding
- Sample BST creation
- Comprehensive menu system

In real-world applications, this system could be extended to:
1. Support duplicate values with counts
2. Implement self-balancing BSTs (AVL, Red-Black)
3. Add bulk insert operations
4. Implement serialization/deserialization
5. Add visualization capabilities

The level-wise display using BFS is particularly useful for:
1. Understanding tree structure
2. Debugging tree operations
3. Educational purposes
4. Tree visualization

This implementation provides a solid foundation for understanding BST operations and their applications in computer science.
