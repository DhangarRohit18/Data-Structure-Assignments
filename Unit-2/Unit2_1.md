# Unit II Assignment 1: Singly Linked List for Vertex Club Membership Records

Implementation of a Singly Linked List to manage 'Vertex Club' membership records in the Computer Engineering Department.

## Problem Statement

The Department of Computer Engineering has a student club named 'Vertex Club' for second, third, and final year students. The first member is the President and the last member is the Secretary. Implementation includes:

- Add/delete members (including President/Secretary)
- Count members
- Display members
- Concatenate two division lists
- Additional operations: reverse, search by PRN, and sort by PRN

## Pseudo Code

### Node Structure
```
Structure Node:
    data: (name, PRN, year)
    next: pointer to Node
```

### Add Member at Beginning (President)
```
Algorithm AddPresident(list, name, PRN, year):
    Create new node with given data
    If list is empty:
        head = new node
    Else:
        new node.next = head
        head = new node
```

### Add Member at End (Secretary)
```
Algorithm AddSecretary(list, name, PRN, year):
    Create new node with given data
    If list is empty:
        head = new node
    Else:
        Traverse to last node
        last node.next = new node
```

### Delete Member by PRN
```
Algorithm DeleteMember(list, PRN):
    If head is null:
        Return "List is empty"
    If head.data.PRN equals PRN:
        head = head.next
        Return "Deleted"
    Traverse list to find node with given PRN
    If found:
        Update previous node's next pointer
        Return "Deleted"
    Else:
        Return "Not found"
```

### Count Members
```
Algorithm CountMembers(list):
    Initialize count = 0
    current = head
    While current is not null:
        Increment count
        current = current.next
    Return count
```

### Display Members
```
Algorithm DisplayMembers(list):
    current = head
    While current is not null:
        Print current.data
        current = current.next
```

### Reverse List
```
Algorithm ReverseList(list):
    Initialize prev = null, current = head, next = null
    While current is not null:
        next = current.next
        current.next = prev
        prev = current
        current = next
    head = prev
```

### Search by PRN
```
Algorithm SearchByPRN(list, PRN):
    current = head
    While current is not null:
        If current.data.PRN equals PRN:
            Return current
        current = current.next
    Return null
```

### Sort by PRN
```
Algorithm SortByPRN(list):
    If list is empty or has one node:
        Return
    Use bubble sort on linked list:
        For each node i:
            For each node j after i:
                If i.PRN > j.PRN:
                    Swap data of i and j
```

### Concatenate Lists
```
Algorithm ConcatenateLists(list1, list2):
    If list1 is empty:
        Return list2
    If list2 is empty:
        Return list1
    Traverse to end of list1
    Connect end of list1 to head of list2
    Return list1
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Student_rrd {
    char name_rrd[50];
    int prn_rrd;
    int year_rrd;
    struct Student_rrd* next_rrd;
};

struct Student_rrd* createStudent_rrd(char name_rrd[], int prn_rrd, int year_rrd);
void addPresident_rrd(struct Student_rrd** head_rrd, char name_rrd[], int prn_rrd, int year_rrd);
void addSecretary_rrd(struct Student_rrd** head_rrd, char name_rrd[], int prn_rrd, int year_rrd);
void addMember_rrd(struct Student_rrd** head_rrd, char name_rrd[], int prn_rrd, int year_rrd, int position_rrd);
void deleteMember_rrd(struct Student_rrd** head_rrd, int prn_rrd);
int countMembers_rrd(struct Student_rrd* head_rrd);
void displayMembers_rrd(struct Student_rrd* head_rrd);
void reverseList_rrd(struct Student_rrd** head_rrd);
struct Student_rrd* searchByPRN_rrd(struct Student_rrd* head_rrd, int prn_rrd);
void sortByPRN_rrd(struct Student_rrd** head_rrd);
struct Student_rrd* concatenateLists_rrd(struct Student_rrd* list1_rrd, struct Student_rrd* list2_rrd);
void displayMenu_rrd();
int main() {
    struct Student_rrd* head_rrd = NULL;
    struct Student_rrd* division2_rrd = NULL;
    int choice_rrd;
    printf("Welcome to Vertex Club Management System!\n");
    while (1)
{
        char name_rrd[50];
        int prn_rrd, year_rrd, position_rrd;
        struct Student_rrd* found_rrd;
        char* yearStr_rrd;
        int count_rrd;
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
{
            case 1:
                printf("Enter President's name: ");
                scanf(" %[^\n]s", name_rrd);
                printf("Enter PRN: ");
                scanf("%d", &prn_rrd);
                printf("Enter year (2 for S.Y., 3 for T.Y., 4 for B.Tech): ");
                scanf("%d", &year_rrd);
                addPresident_rrd(&head_rrd, name_rrd, prn_rrd, year_rrd);
                break;
            case 2:
                printf("Enter Secretary's name: ");
                scanf(" %[^\n]s", name_rrd);
                printf("Enter PRN: ");
                scanf("%d", &prn_rrd);
                printf("Enter year (2 for S.Y., 3 for T.Y., 4 for B.Tech): ");
                scanf("%d", &year_rrd);
                addSecretary_rrd(&head_rrd, name_rrd, prn_rrd, year_rrd);
                break;
            case 3:
                printf("Enter member's name: ");
                scanf(" %[^\n]s", name_rrd);
                printf("Enter PRN: ");
                scanf("%d", &prn_rrd);
                printf("Enter year (2 for S.Y., 3 for T.Y., 4 for B.Tech): ");
                scanf("%d", &year_rrd);
                printf("Enter position: ");
                scanf("%d", &position_rrd);
                addMember_rrd(&head_rrd, name_rrd, prn_rrd, year_rrd, position_rrd);
                break;
            case 4:
                printf("Enter PRN of member to delete: ");
                scanf("%d", &prn_rrd);
                deleteMember_rrd(&head_rrd, prn_rrd);
                break;
            case 5:
                count_rrd = countMembers_rrd(head_rrd);
                printf("Total members in the club: %d\n", count_rrd);
                break;
            case 6:
                displayMembers_rrd(head_rrd);
                break;
            case 7:
                reverseList_rrd(&head_rrd);
                break;
            case 8:
                printf("Enter PRN to search: ");
                scanf("%d", &prn_rrd);
                found_rrd = searchByPRN_rrd(head_rrd, prn_rrd);
                if (found_rrd != NULL)
{
                    switch (found_rrd->year_rrd)
{
                        case 2: yearStr_rrd = "S.Y."; break;
                        case 3: yearStr_rrd = "T.Y."; break;
                        case 4: yearStr_rrd = "B.Tech"; break;
                        default: yearStr_rrd = "Unknown";
                    }

                    printf("Member found:\nPRN: %d\nName: %s\nYear: %s\n", 
                           found_rrd->prn_rrd, found_rrd->name_rrd, yearStr_rrd);
                }

                else {
                    printf("Member with PRN %d not found!\n", prn_rrd);
                }
                break;
            case 9:
                sortByPRN_rrd(&head_rrd);
                break;
            case 10:
                addPresident_rrd(&division2_rrd, "Div2 President", 2001, 2);
                addSecretary_rrd(&division2_rrd, "Div2 Secretary", 2002, 3);
                head_rrd = concatenateLists_rrd(head_rrd, division2_rrd);
                printf("Division lists concatenated successfully!\n");
                division2_rrd = NULL;
                break;
            case 11:
                printf("Exiting... Thank you!\n");
                return 0;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    }
    return 0;
}

struct Student_rrd* createStudent_rrd(char name_rrd[], int prn_rrd, int year_rrd) {
    struct Student_rrd* newStudent_rrd = (struct Student_rrd*)malloc(sizeof(struct Student_rrd));
    strcpy(newStudent_rrd->name_rrd, name_rrd);
    newStudent_rrd->prn_rrd = prn_rrd;
    newStudent_rrd->year_rrd = year_rrd;
    newStudent_rrd->next_rrd = NULL;
    return newStudent_rrd;
}

void addPresident_rrd(struct Student_rrd** head_rrd, char name_rrd[], int prn_rrd, int year_rrd) {
    struct Student_rrd* newPresident_rrd = createStudent_rrd(name_rrd, prn_rrd, year_rrd);
    newPresident_rrd->next_rrd = *head_rrd;
    *head_rrd = newPresident_rrd;
    printf("President added successfully!\n");
}

void addSecretary_rrd(struct Student_rrd** head_rrd, char name_rrd[], int prn_rrd, int year_rrd) {
    struct Student_rrd* newSecretary_rrd = createStudent_rrd(name_rrd, prn_rrd, year_rrd);
    struct Student_rrd* temp_rrd;
    if (*head_rrd == NULL)
{
        *head_rrd = newSecretary_rrd;
        printf("Secretary added successfully!\n");
        return;
    }

    temp_rrd = *head_rrd;
    while (temp_rrd->next_rrd != NULL)
{
        temp_rrd = temp_rrd->next_rrd;
    }

    temp_rrd->next_rrd = newSecretary_rrd;
    printf("Secretary added successfully!\n");
}

void addMember_rrd(struct Student_rrd** head_rrd, char name_rrd[], int prn_rrd, int year_rrd, int position_rrd) {
    struct Student_rrd* newMember_rrd;
    struct Student_rrd* temp_rrd;
    int i_rrd;
    if (position_rrd <= 0)
{
        printf("Invalid position!\n");
        return;
    }

    if (position_rrd == 1)
{
        addPresident_rrd(head_rrd, name_rrd, prn_rrd, year_rrd);
        return;
    }

    newMember_rrd = createStudent_rrd(name_rrd, prn_rrd, year_rrd);
    temp_rrd = *head_rrd;
    for (i_rrd = 1; i_rrd < position_rrd - 1 && temp_rrd != NULL; i_rrd++)
{
        temp_rrd = temp_rrd->next_rrd;
    }

    if (temp_rrd == NULL)
{
        printf("Position out of bounds!\n");
        free(newMember_rrd);
        return;
    }

    newMember_rrd->next_rrd = temp_rrd->next_rrd;
    temp_rrd->next_rrd = newMember_rrd;
    printf("Member added successfully at position %d!\n", position_rrd);
}

void deleteMember_rrd(struct Student_rrd** head_rrd, int prn_rrd) {
    struct Student_rrd* temp_rrd;
    struct Student_rrd* nodeToDelete_rrd;
    if (*head_rrd == NULL)
{
        printf("List is empty!\n");
        return;
    }

    if ((*head_rrd)->prn_rrd == prn_rrd)
{
        temp_rrd = *head_rrd;
        *head_rrd = (*head_rrd)->next_rrd;
        free(temp_rrd);
        printf("Member deleted successfully!\n");
        return;
    }

    temp_rrd = *head_rrd;
    while (temp_rrd->next_rrd != NULL && temp_rrd->next_rrd->prn_rrd != prn_rrd)
{
        temp_rrd = temp_rrd->next_rrd;
    }

    if (temp_rrd->next_rrd == NULL)
{
        printf("Member with PRN %d not found!\n", prn_rrd);
        return;
    }

    nodeToDelete_rrd = temp_rrd->next_rrd;
    temp_rrd->next_rrd = temp_rrd->next_rrd->next_rrd;
    free(nodeToDelete_rrd);
    printf("Member deleted successfully!\n");
}

int countMembers_rrd(struct Student_rrd* head_rrd) {
    int count_rrd = 0;
    struct Student_rrd* temp_rrd = head_rrd;
    while (temp_rrd != NULL)
{
        count_rrd++;
        temp_rrd = temp_rrd->next_rrd;
    }
    return count_rrd;
}

void displayMembers_rrd(struct Student_rrd* head_rrd) {
    struct Student_rrd* temp_rrd;
    char* yearStr_rrd;
    if (head_rrd == NULL)
{
        printf("No members in the club!\n");
        return;
    }

    printf("\nVertex Club Members:\n");
    printf("PRN\tName\t\tYear\n");
    printf("-----------------------------\n");
    temp_rrd = head_rrd;
    while (temp_rrd != NULL)
{
        switch (temp_rrd->year_rrd)
{
            case 2: yearStr_rrd = "S.Y."; break;
            case 3: yearStr_rrd = "T.Y."; break;
            case 4: yearStr_rrd = "B.Tech"; break;
            default: yearStr_rrd = "Unknown";
        }

        printf("%d\t%s\t\t%s\n", temp_rrd->prn_rrd, temp_rrd->name_rrd, yearStr_rrd);
        temp_rrd = temp_rrd->next_rrd;
    }

    printf("-----------------------------\n");
}

void reverseList_rrd(struct Student_rrd** head_rrd) {
    struct Student_rrd* prev_rrd = NULL;
    struct Student_rrd* current_rrd = *head_rrd;
    struct Student_rrd* next_rrd = NULL;
    while (current_rrd != NULL)
{
        next_rrd = current_rrd->next_rrd;
        current_rrd->next_rrd = prev_rrd;
        prev_rrd = current_rrd;
        current_rrd = next_rrd;
    }

    *head_rrd = prev_rrd;
    printf("List reversed successfully!\n");
}

struct Student_rrd* searchByPRN_rrd(struct Student_rrd* head_rrd, int prn_rrd) {
    struct Student_rrd* temp_rrd = head_rrd;
    while (temp_rrd != NULL)
{
        if (temp_rrd->prn_rrd == prn_rrd)
{
            return temp_rrd;
        }

        temp_rrd = temp_rrd->next_rrd;
    }
    return NULL;
}

void sortByPRN_rrd(struct Student_rrd** head_rrd) {
    int swapped_rrd;
    struct Student_rrd* ptr1_rrd;
    struct Student_rrd* lptr_rrd = NULL;
    int tempPRN_rrd;
    char tempName_rrd[50];
    int tempYear_rrd;
    if (*head_rrd == NULL || (*head_rrd)->next_rrd == NULL)
{
        printf("List is already sorted or empty!\n");
        return;
    }

    do
{
        swapped_rrd = 0;
        ptr1_rrd = *head_rrd;
        while (ptr1_rrd->next_rrd != lptr_rrd)
{
            if (ptr1_rrd->prn_rrd > ptr1_rrd->next_rrd->prn_rrd)
{
                tempPRN_rrd = ptr1_rrd->prn_rrd;
                ptr1_rrd->prn_rrd = ptr1_rrd->next_rrd->prn_rrd;
                ptr1_rrd->next_rrd->prn_rrd = tempPRN_rrd;
                strcpy(tempName_rrd, ptr1_rrd->name_rrd);
                strcpy(ptr1_rrd->name_rrd, ptr1_rrd->next_rrd->name_rrd);
                strcpy(ptr1_rrd->next_rrd->name_rrd, tempName_rrd);
                tempYear_rrd = ptr1_rrd->year_rrd;
                ptr1_rrd->year_rrd = ptr1_rrd->next_rrd->year_rrd;
                ptr1_rrd->next_rrd->year_rrd = tempYear_rrd;
                swapped_rrd = 1;
            }

            ptr1_rrd = ptr1_rrd->next_rrd;
        }

        lptr_rrd = ptr1_rrd;
    } while (swapped_rrd);

    printf("List sorted by PRN successfully!\n");
}

struct Student_rrd* concatenateLists_rrd(struct Student_rrd* list1_rrd, struct Student_rrd* list2_rrd) {
    struct Student_rrd* temp_rrd;
    if (list1_rrd == NULL)
{
        return list2_rrd;
    }

    if (list2_rrd == NULL)
{
        return list1_rrd;
    }

    temp_rrd = list1_rrd;
    while (temp_rrd->next_rrd != NULL)
{
        temp_rrd = temp_rrd->next_rrd;
    }

    temp_rrd->next_rrd = list2_rrd;
    return list1_rrd;
}

void displayMenu_rrd() {
    printf("\n===== Vertex Club Management System =====\n");
    printf("1. Add President\n");
    printf("2. Add Secretary\n");
    printf("3. Add Member at Position\n");
    printf("4. Delete Member by PRN\n");
    printf("5. Count Members\n");
    printf("6. Display Members\n");
    printf("7. Reverse List\n");
    printf("8. Search Member by PRN\n");
    printf("9. Sort Members by PRN\n");
    printf("10. Concatenate Two Division Lists\n");
    printf("11. Exit\n");
    printf("========================================\n");
    printf("Enter your choice: ");
}

                head_rrd = concatenateLists_rrd(head_rrd, division2_rrd);
                division2_rrd = NULL;
                printf("Lists concatenated successfully!\n");
                break;
            }

{
                printf("Thank you for using Vertex Club Management System!\n");
                while (head_rrd != NULL)
{
                    struct Student_rrd* temp_rrd = head_rrd;
                    head_rrd = head_rrd->next_rrd;
                    free(temp_rrd);
                }

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
Welcome to Vertex Club Management System!
===== Vertex Club Management System =====
1. Add President
2. Add Secretary
3. Add Member at Position
4. Delete Member by PRN
5. Count Members
6. Display Members
7. Reverse List
8. Search Member by PRN
9. Sort Members by PRN
10. Concatenate Two Division Lists
11. Exit
========================================
Enter your choice: 1
Enter President's name: John Smith
Enter PRN: 1001
Enter year (2 for S.Y., 3 for T.Y., 4 for B.Tech): 4
President added successfully!
===== Vertex Club Management System =====
1. Add President
2. Add Secretary
3. Add Member at Position
4. Delete Member by PRN
5. Count Members
6. Display Members
7. Reverse List
8. Search Member by PRN
9. Sort Members by PRN
10. Concatenate Two Division Lists
11. Exit
========================================
Enter your choice: 2
Enter Secretary's name: Jane Doe
Enter PRN: 1002
Enter year (2 for S.Y., 3 for T.Y., 4 for B.Tech): 3
Secretary added successfully!
===== Vertex Club Management System =====
1. Add President
2. Add Secretary
3. Add Member at Position
4. Delete Member by PRN
5. Count Members
6. Display Members
7. Reverse List
8. Search Member by PRN
9. Sort Members by PRN
10. Concatenate Two Division Lists
11. Exit
========================================
Enter your choice: 6
Vertex Club Members:
PRN     Name            Year
-----------------------------
1001    John Smith      B.Tech
1002    Jane Doe        T.Y.
-----------------------------
```

## Dry Run

1. **Add President**: 
   - Create new node with John Smith's data (PRN: 1001, Year: 4)
   - Since list is empty, set head to this new node

2. **Add Secretary**:
   - Create new node with Jane Doe's data (PRN: 1002, Year: 3)
   - Traverse to end of list (only one node currently)
   - Set last node's next pointer to new node

3. **Display Members**:
   - Start from head node
   - Print each node's data until reaching NULL
   - Shows President first, then Secretary

4. **Search by PRN (1001)**:
   - Start from head
   - Compare each node's PRN with 1001
   - Found at first node, return that node

5. **Delete Member (PRN: 1001)**:
   - PRN matches head node
   - Update head to point to next node
   - Free memory of deleted node

## Conclusion

The implementation demonstrates efficient management of club membership using a singly linked list. Key operations include:

1. **Insertion**: O(1) for president/secretary, O(n) for position-based insertion
2. **Deletion**: O(n) in worst case as we need to traverse to find the node
3. **Search**: O(n) linear search through the list
4. **Sorting**: O(n²) using bubble sort implementation
5. **Reversal**: O(n) single pass through the list

The program efficiently handles all required operations with proper memory management. The use of linked lists allows dynamic memory allocation, which is more memory-efficient than arrays for this type of application where the number of members can vary.

The additional operations (reverse, search, sort) enhance the functionality beyond basic insertion and deletion, making it a comprehensive membership management system.

