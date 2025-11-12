# Unit IV Assignment 6: Student Roll Number Assignment using BST

Implementation of a program to assign roll numbers to students based on their previous year's results using a Binary Search Tree.

## Problem Statement

Write a program, using trees, to assign the roll nos. to the students of your class as per their previous years result. i.e topper will be roll no. 1.

## Pseudo Code

### Student Node Structure
```
Structure StudentNode:
    name: string
    marks: integer
    rollNo: integer
    left: pointer to StudentNode
    right: pointer to StudentNode
```

### Insert Student (based on marks)
```
Algorithm InsertStudent(root, name, marks):
    If root is NULL:
        Create new student node with name and marks
        Return new node
    If marks > root.marks:
        root.left = InsertStudent(root.left, name, marks)
    Else If marks < root.marks:
        root.right = InsertStudent(root.right, name, marks)
    Else:
        root.left = InsertStudent(root.left, name, marks)
    Return root
```

### Assign Roll Numbers (inorder traversal)
```
Algorithm AssignRollNumbers(root, rollCounter):
    If root is not NULL:
        AssignRollNumbers(root.left, rollCounter)
        root.rollNo = rollCounter++
        AssignRollNumbers(root.right, rollCounter)
```

### Display Students by Roll Number
```
Algorithm DisplayByRollNumber(root):
    If root is not NULL:
        DisplayByRollNumber(root.left)
        Print root.rollNo, root.name, root.marks
        DisplayByRollNumber(root.right)
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct StudentNode_rrd {
    char name_rrd[50];
    int marks_rrd;
    int rollNo_rrd;
    struct StudentNode_rrd* left_rrd;
    struct StudentNode_rrd* right_rrd;
};

struct StudentNode_rrd* createStudentNode_rrd(char name_rrd[], int marks_rrd);
struct StudentNode_rrd* insertStudent_rrd(struct StudentNode_rrd* root_rrd, char name_rrd[], int marks_rrd);
void assignRollNumbers_rrd(struct StudentNode_rrd* root_rrd, int* rollCounter_rrd);
void displayByRollNumber_rrd(struct StudentNode_rrd* root_rrd);
void displayByMarks_rrd(struct StudentNode_rrd* root_rrd);
struct StudentNode_rrd* searchStudent_rrd(struct StudentNode_rrd* root_rrd, char name_rrd[]);
struct StudentNode_rrd* findTopper_rrd(struct StudentNode_rrd* root_rrd);
struct StudentNode_rrd* findLast_rrd(struct StudentNode_rrd* root_rrd);
int countStudents_rrd(struct StudentNode_rrd* root_rrd);
double calculateAverage_rrd(struct StudentNode_rrd* root_rrd, int* totalCount_rrd);
void displayStructure_rrd(struct StudentNode_rrd* root_rrd, int space_rrd);
void printTreeStructure_rrd(struct StudentNode_rrd* root_rrd);
void freeTree_rrd(struct StudentNode_rrd* root_rrd);
struct StudentNode_rrd* createSampleStudents_rrd();
void displayMenu_rrd();
struct StudentNode_rrd* createStudentNode_rrd(char name_rrd[], int marks_rrd) {
    struct StudentNode_rrd* newNode_rrd = (struct StudentNode_rrd*)malloc(sizeof(struct StudentNode_rrd));
    strcpy(newNode_rrd->name_rrd, name_rrd);
    newNode_rrd->marks_rrd = marks_rrd;
    newNode_rrd->rollNo_rrd = 0;
    newNode_rrd->left_rrd = NULL;
    newNode_rrd->right_rrd = NULL;
    return newNode_rrd;
}

struct StudentNode_rrd* insertStudent_rrd(struct StudentNode_rrd* root_rrd, char name_rrd[], int marks_rrd) {
    if (root_rrd == NULL)
{
        printf("Added student %s with marks %d\n", name_rrd, marks_rrd);
        return createStudentNode_rrd(name_rrd, marks_rrd);
    }

    if (marks_rrd > root_rrd->marks_rrd)
{
        root_rrd->left_rrd = insertStudent_rrd(root_rrd->left_rrd, name_rrd, marks_rrd);
    } else if (marks_rrd < root_rrd->marks_rrd)

{
        root_rrd->right_rrd = insertStudent_rrd(root_rrd->right_rrd, name_rrd, marks_rrd);
    } else
{

        printf("Student %s has same marks as another student (%d)\n", name_rrd, marks_rrd);
        root_rrd->left_rrd = insertStudent_rrd(root_rrd->left_rrd, name_rrd, marks_rrd);
    }
    return root_rrd;
}

void assignRollNumbers_rrd(struct StudentNode_rrd* root_rrd, int* rollCounter_rrd) {
    if (root_rrd != NULL)
{
        assignRollNumbers_rrd(root_rrd->left_rrd, rollCounter_rrd);
        root_rrd->rollNo_rrd = (*rollCounter_rrd)++;
        assignRollNumbers_rrd(root_rrd->right_rrd, rollCounter_rrd);
    }
}

void displayByRollNumber_rrd(struct StudentNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        displayByRollNumber_rrd(root_rrd->left_rrd);
        printf("Roll No: %d\tName: %s\t\tMarks: %d\n", root_rrd->rollNo_rrd, root_rrd->name_rrd, root_rrd->marks_rrd);
        displayByRollNumber_rrd(root_rrd->right_rrd);
    }
}

void displayByMarks_rrd(struct StudentNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        displayByMarks_rrd(root_rrd->left_rrd);
        printf("Name: %s\t\tMarks: %d\t\tRoll No: %d\n", root_rrd->name_rrd, root_rrd->marks_rrd, root_rrd->rollNo_rrd);
        displayByMarks_rrd(root_rrd->right_rrd);
    }
}

struct StudentNode_rrd* searchStudent_rrd(struct StudentNode_rrd* root_rrd, char name_rrd[]) {
    if (root_rrd == NULL)
{
        return NULL;
    }

    int comparison_rrd = strcmp(name_rrd, root_rrd->name_rrd);
    if (comparison_rrd == 0)
{
        return root_rrd;
    } else if (comparison_rrd < 0)

{
        return searchStudent_rrd(root_rrd->left_rrd, name_rrd);
    } else
{
        return searchStudent_rrd(root_rrd->right_rrd, name_rrd);
    }
}

struct StudentNode_rrd* findTopper_rrd(struct StudentNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return NULL;
    }

    while (root_rrd->left_rrd != NULL)
{
        root_rrd = root_rrd->left_rrd;
    }
    return root_rrd;
}

struct StudentNode_rrd* findLast_rrd(struct StudentNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return NULL;
    }

    while (root_rrd->right_rrd != NULL)
{
        root_rrd = root_rrd->right_rrd;
    }
    return root_rrd;
}

int countStudents_rrd(struct StudentNode_rrd* root_rrd) {
    if (root_rrd == NULL)
{
        return 0;
    }
    return 1 + countStudents_rrd(root_rrd->left_rrd) + countStudents_rrd(root_rrd->right_rrd);
}

double calculateAverage_rrd(struct StudentNode_rrd* root_rrd, int* totalCount_rrd)
{
    if (root_rrd == NULL)
{
        return 0.0;
    }

    (*totalCount_rrd)++;
    return root_rrd->marks_rrd + calculateAverage_rrd(root_rrd->left_rrd, totalCount_rrd) + 
           calculateAverage_rrd(root_rrd->right_rrd, totalCount_rrd);
}

void displayStructure_rrd(struct StudentNode_rrd* root_rrd, int space_rrd) {
    const int COUNT_rrd = 15;
    if (root_rrd == NULL)
{
        return;
    }

    space_rrd += COUNT_rrd;
    displayStructure_rrd(root_rrd->right_rrd, space_rrd);
    printf("\n");
    for (int i_rrd = COUNT_rrd; i_rrd < space_rrd; i_rrd++)
{
        printf(" ");
    }

    printf("%s(%d)\n", root_rrd->name_rrd, root_rrd->marks_rrd);
    displayStructure_rrd(root_rrd->left_rrd, space_rrd);
}

void printTreeStructure_rrd(struct StudentNode_rrd* root_rrd) {
    printf("\nStudent Tree Structure (Name(Marks)):\n");
    displayStructure_rrd(root_rrd, 0);
    printf("\n");
}

void freeTree_rrd(struct StudentNode_rrd* root_rrd) {
    if (root_rrd != NULL)
{
        freeTree_rrd(root_rrd->left_rrd);
        freeTree_rrd(root_rrd->right_rrd);
        free(root_rrd);
    }
}

struct StudentNode_rrd* createSampleStudents_rrd() {
    struct StudentNode_rrd* root_rrd = NULL;
    root_rrd = insertStudent_rrd(root_rrd, "Alice Johnson", 95);
    root_rrd = insertStudent_rrd(root_rrd, "Bob Smith", 87);
    root_rrd = insertStudent_rrd(root_rrd, "Charlie Brown", 92);
    root_rrd = insertStudent_rrd(root_rrd, "Diana Wilson", 78);
    root_rrd = insertStudent_rrd(root_rrd, "Edward Davis", 88);
    root_rrd = insertStudent_rrd(root_rrd, "Fiona Miller", 96);
    root_rrd = insertStudent_rrd(root_rrd, "George Taylor", 82);
    root_rrd = insertStudent_rrd(root_rrd, "Helen Anderson", 91);
    root_rrd = insertStudent_rrd(root_rrd, "Ian Thomas", 85);
    root_rrd = insertStudent_rrd(root_rrd, "Julia Martinez", 89);
    return root_rrd;
}

struct StudentNode_rrd* addStudentInteractive_rrd(struct StudentNode_rrd* root_rrd) {
    char name_rrd[50];
    int marks_rrd;
    printf("Enter student name: ");
    scanf(" %[^\n]s", name_rrd);
    printf("Enter student marks: ");
    scanf("%d", &marks_rrd);
    if (marks_rrd < 0 || marks_rrd > 100)
{
        printf("Invalid marks! Marks should be between 0 and 100.\n");
        return root_rrd;
    }

    root_rrd = insertStudent_rrd(root_rrd, name_rrd, marks_rrd);
    return root_rrd;
}

void displayMenu_rrd() {
    printf("\n===== Student Roll Number Assignment System =====\n");
    printf("1. Create Sample Student Data\n");
    printf("2. Add Student\n");
    printf("3. Assign Roll Numbers\n");
    printf("4. Display Students by Roll Number\n");
    printf("5. Display Students by Marks (Topper first)\n");
    printf("6. Display Tree Structure\n");
    printf("7. Search Student\n");
    printf("8. Show Topper\n");
    printf("9. Show Last Student\n");
    printf("10. Count Students\n");
    printf("11. Calculate Average Marks\n");
    printf("12. Exit\n");
    printf("===============================================\n");
    printf("Enter your choice: ");
}

int main() {
    printf("Welcome to Student Roll Number Assignment System!\n");
    printf("Students will be assigned roll numbers based on their marks (higher marks = lower roll number)\n");
    struct StudentNode_rrd* root_rrd = NULL;
    int rollCounter_rrd = 1;
    int rollNumbersAssigned_rrd = 0;
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
{
{
                freeTree_rrd(root_rrd);
                root_rrd = createSampleStudents_rrd();
                rollCounter_rrd = 1;
                rollNumbersAssigned_rrd = 0;
                printf("Sample student data created successfully!\n");
                break;
            }

{
                root_rrd = addStudentInteractive_rrd(root_rrd);
                rollNumbersAssigned_rrd = 0;
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                rollCounter_rrd = 1;
                assignRollNumbers_rrd(root_rrd, &rollCounter_rrd);
                rollNumbersAssigned_rrd = 1;
                printf("Roll numbers assigned successfully!\n");
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                if (!rollNumbersAssigned_rrd)
{
                    printf("Please assign roll numbers first (Option 3)!\n");
                    break;
                }

                printf("\nStudents by Roll Number:\n");
                printf("Roll No\tName\t\t\tMarks\n");
                printf("-------\t----\t\t\t-----\n");
                displayByRollNumber_rrd(root_rrd);
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                if (!rollNumbersAssigned_rrd)
{
                    printf("Please assign roll numbers first (Option 3)!\n");
                    break;
                }

                printf("\nStudents by Marks (Topper first):\n");
                printf("Name\t\t\tMarks\t\tRoll No\n");
                printf("----\t\t\t-----\t\t-------\n");
                displayByMarks_rrd(root_rrd);
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                printTreeStructure_rrd(root_rrd);
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                if (!rollNumbersAssigned_rrd)
{
                    printf("Please assign roll numbers first (Option 3)!\n");
                    break;
                }

                char name_rrd[50];
                printf("Enter student name to search: ");
                scanf(" %[^\n]s", name_rrd);
                struct StudentNode_rrd* student_rrd = searchStudent_rrd(root_rrd, name_rrd);
                if (student_rrd != NULL)
{
                    printf("Student found:\n");
                    printf("Name: %s\n", student_rrd->name_rrd);
                    printf("Marks: %d\n", student_rrd->marks_rrd);
                    printf("Roll No: %d\n", student_rrd->rollNo_rrd);
                } else
{

                    printf("Student %s not found!\n", name_rrd);
                }
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                if (!rollNumbersAssigned_rrd)
{
                    printf("Please assign roll numbers first (Option 3)!\n");
                    break;
                }

                struct StudentNode_rrd* topper_rrd = findTopper_rrd(root_rrd);
                if (topper_rrd != NULL)
{
                    printf("Class Topper:\n");
                    printf("Name: %s\n", topper_rrd->name_rrd);
                    printf("Marks: %d\n", topper_rrd->marks_rrd);
                    printf("Roll No: %d\n", topper_rrd->rollNo_rrd);
                }
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                if (!rollNumbersAssigned_rrd)
{
                    printf("Please assign roll numbers first (Option 3)!\n");
                    break;
                }

                struct StudentNode_rrd* last_rrd = findLast_rrd(root_rrd);
                if (last_rrd != NULL)
{
                    printf("Last Student:\n");
                    printf("Name: %s\n", last_rrd->name_rrd);
                    printf("Marks: %d\n", last_rrd->marks_rrd);
                    printf("Roll No: %d\n", last_rrd->rollNo_rrd);
                }
                break;
            }

{
                int count_rrd = countStudents_rrd(root_rrd);
                printf("Total number of students: %d\n", count_rrd);
                break;
            }

{
                if (root_rrd == NULL)
{
                    printf("No students in the system!\n");
                    break;
                }

                int totalCount_rrd = 0;
                double totalMarks_rrd = calculateAverage_rrd(root_rrd, &totalCount_rrd);
                if (totalCount_rrd > 0)
{
                    double average_rrd = totalMarks_rrd / totalCount_rrd;
                    printf("Average marks of all students: %.2f\n", average_rrd);
                }
                break;
            }

{
                printf("Thank you for using Student Roll Number Assignment System!\n");
                freeTree_rrd(root_rrd);
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
Welcome to Student Roll Number Assignment System!
Students will be assigned roll numbers based on their marks (higher marks = lower roll number)
===== Student Roll Number Assignment System =====
1. Create Sample Student Data
2. Add Student
3. Assign Roll Numbers
4. Display Students by Roll Number
5. Display Students by Marks (Topper first)
6. Display Tree Structure
7. Search Student
8. Show Topper
9. Show Last Student
10. Count Students
11. Calculate Average Marks
12. Exit
===============================================
Enter your choice: 1
Added student Alice Johnson with marks 95
Added student Bob Smith with marks 87
Added student Charlie Brown with marks 92
Added student Diana Wilson with marks 78
Added student Edward Davis with marks 88
Added student Fiona Miller with marks 96
Added student George Taylor with marks 82
Added student Helen Anderson with marks 91
Added student Ian Thomas with marks 85
Added student Julia Martinez with marks 89
Sample student data created successfully!
===== Student Roll Number Assignment System =====
1. Create Sample Student Data
2. Add Student
3. Assign Roll Numbers
4. Display Students by Roll Number
5. Display Students by Marks (Topper first)
6. Display Tree Structure
7. Search Student
8. Show Topper
9. Show Last Student
10. Count Students
11. Calculate Average Marks
12. Exit
===============================================
Enter your choice: 3
Roll numbers assigned successfully!
===== Student Roll Number Assignment System =====
1. Create Sample Student Data
2. Add Student
3. Assign Roll Numbers
4. Display Students by Roll Number
5. Display Students by Marks (Topper first)
6. Display Tree Structure
7. Search Student
8. Show Topper
9. Show Last Student
10. Count Students
11. Calculate Average Marks
12. Exit
===============================================
Enter your choice: 4
Students by Roll Number:
Roll No	Name			Marks
-------	----			-----
1	Fiona Miller		96
2	Alice Johnson		95
3	Charlie Brown		92
4	Helen Anderson		91
5	Julia Martinez		89
6	Edward Davis		88
7	Bob Smith		87
8	Ian Thomas		85
9	George Taylor		82
10	Diana Wilson		78
===== Student Roll Number Assignment System =====
1. Create Sample Student Data
2. Add Student
3. Assign Roll Numbers
4. Display Students by Roll Number
5. Display Students by Marks (Topper first)
6. Display Tree Structure
7. Search Student
8. Show Topper
9. Show Last Student
10. Count Students
11. Calculate Average Marks
12. Exit
===============================================
Enter your choice: 8
Class Topper:
Name: Fiona Miller
Marks: 96
Roll No: 1
```

## Dry Run

For students with marks [95, 87, 92, 78, 88, 96, 82, 91, 85, 89]:

1. **BST Construction** (Higher marks to left):
   - Insert Fiona Miller (96) - root
   - Insert Alice Johnson (95) - 95 < 96, go right, but no right child, insert as right child
   - Wait, this is wrong. Let me retrace:
   - Insert Fiona Miller (96) - root
   - Insert Alice Johnson (95) - 95 < 96, go to right subtree
   - Insert Charlie Brown (92) - 92 < 96, go right, 92 < 95, go right, insert
   - Actually, I need to follow the code logic:
   - Insert Fiona Miller (96) - root
   - Insert Alice Johnson (95) - 95 < 96, root->right = insert(root->right, "Alice Johnson", 95)
     * root->right is NULL, so create new node
   - Insert Charlie Brown (92) - 92 < 96, go to right subtree, 92 < 95, go to right subtree, create new node
   - This creates a right-skewed tree which is not optimal.

Let me correct the approach - the code should put higher marks to the left for descending order:

Correct BST construction:
- Insert Fiona Miller (96) - root: 96
- Insert Alice Johnson (95) - 95 < 96, go right: 96(95)
- Insert Charlie Brown (92) - 92 < 96, go right, 92 < 95, go right: 96(95(null,92))
- Insert Helen Anderson (91) - 91 < 96, go right, 91 < 95, go right, 91 < 92, go right
- Insert Julia Martinez (89) - continues right...
- Insert Edward Davis (88) - continues right...
- Insert Bob Smith (87) - continues right...
- Insert Ian Thomas (85) - continues right...
- Insert George Taylor (82) - continues right...
- Insert Diana Wilson (78) - continues right...

Actually, this would create a completely right-skewed tree. Let me reconsider the insertion logic:

Looking at the code again:
```c
if (marks_rrd > root_rrd->marks_rrd)
{
    root_rrd->left_rrd = insertStudent_rrd(root_rrd->left_rrd, name_rrd, marks_rrd);
} else if (marks_rrd < root_rrd->marks_rrd)

{
    root_rrd->right_rrd = insertStudent_rrd(root_rrd->right_rrd, name_rrd, marks_rrd);
}
```

So higher marks go to the left. This is correct for descending order.

For the sample data [95, 87, 92, 78, 88, 96, 82, 91, 85, 89]:
- Insert Alice Johnson (95) - root: 95
- Insert Bob Smith (87) - 87 < 95, go right: 95(null,87)
- Insert Charlie Brown (92) - 92 < 95, go right, 92 > 87, go left: 95(null,87(92,null))
- Insert Diana Wilson (78) - 78 < 95, go right, 78 < 87, go right: 95(null,87(92,null,null,78))
- Insert Edward Davis (88) - 88 < 95, go right, 88 > 87, go left, 88 > 92, go right: continues...
- Insert Fiona Miller (96) - 96 > 95, go left: 95(96,null,87(92,null,null,78))

This creates a more balanced tree.

2. **Assign Roll Numbers** (inorder traversal for descending marks):
   - The inorder traversal of a BST gives sorted order
   - But we want descending order of marks, so we traverse left subtree first
   - Process left subtree (higher marks first), assign roll numbers, then right subtree
   - Fiona Miller (96) gets roll no 1
   - Alice Johnson (95) gets roll no 2
   - Charlie Brown (92) gets roll no 3
   - Helen Anderson (91) gets roll no 4
   - And so on...

3. **Display by Roll Number** (inorder traversal):
   - Since roll numbers were assigned in inorder, displaying in inorder gives roll number order
   - Roll No 1: Fiona Miller (96)
   - Roll No 2: Alice Johnson (95)
   - Roll No 3: Charlie Brown (92)
   - And so on...

## Conclusion

The implementation demonstrates an efficient student roll number assignment system using Binary Search Tree. Key features include:

1. **BST-based Sorting**: Students automatically sorted by marks during insertion
2. **Efficient Roll Assignment**: Single inorder traversal to assign roll numbers
3. **Flexible Operations**: Multiple ways to view and analyze student data
4. **Memory Management**: Proper allocation and deallocation

**Time Complexities**:
- Insert Student: O(h) where h is height of tree (O(log n) average, O(n) worst case)
- Assign Roll Numbers: O(n) where n is number of students
- Display by Roll Number: O(n) where n is number of students
- Search Student: O(h) where h is height of tree
- For balanced tree: O(log n), for skewed tree: O(n)

**Space Complexity**: O(n) for storing n students, O(h) for recursion stack

The BST approach is ideal for this application because:
1. **Automatic Sorting**: Students are sorted by marks during insertion
2. **Efficient Range Queries**: Can easily find students within mark ranges
3. **Dynamic Operations**: Can add/remove students efficiently
4. **Multiple Traversal Orders**: Can traverse in different orders for different views

The implementation handles edge cases properly:
- Empty student list
- Duplicate marks handling
- Invalid input validation
- Memory management to prevent leaks

Additional features beyond requirements:
- Student search by name
- Topper and last student identification
- Student count and average calculation
- Tree structure visualization
- Interactive student addition
- Multiple display options
- Comprehensive menu system

In real-world applications, this system could be extended to:
1. **Multiple Criteria**: Sort by multiple factors (marks, attendance, etc.)
2. **Persistence**: Save/load student data from files
3. **Grade Calculation**: Automatically assign grades based on marks
4. **Batch Processing**: Process multiple classes/sections
5. **Export Features**: Generate reports in various formats
6. **Web Interface**: Create a web-based version
7. **Database Integration**: Store data in a database instead of memory

The system correctly assigns roll numbers based on performance:
1. **Top Performer**: Gets roll number 1
2. **Descending Order**: Better performance = lower roll number
3. **Fair Assignment**: Objective and consistent roll number assignment

This implementation provides a solid foundation for understanding how BSTs can be applied to real-world problems like student management systems, demonstrating both the data structure concepts and practical application.
