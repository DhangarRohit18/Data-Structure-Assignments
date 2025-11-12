# Unit VI Assignment 5: Faculty Database Management using Hash Table with Linear Probing

Implementation to simulate a faculty database as a hash table with MOD hash function and linear probing collision handling technique.

## Problem Statement

WAP to simulate a faculty database as a hash table. Search a particular faculty by using MOD as a hash function for linear probing method of collision handling technique. Assume suitable data for faculty record.

## Pseudo Code

### Faculty Record Structure
```
Structure Faculty:
    id: integer
    name: string
    department: string
    designation: string
    experience: integer
```

### Hash Table Structure
```
Structure HashTable:
    size: integer
    faculties: array of Faculty
    occupied: array of booleans
```

### Hash Function
```
Algorithm Hash(id, tableSize):
    Return id MOD tableSize
```

### Insert Faculty
```
Algorithm InsertFaculty(hashTable, faculty):
    index = Hash(faculty.id, hashTable.size)
    startIndex = index
    While hashTable.occupied[index] is true AND hashTable.faculties[index].id != faculty.id:
        index = (index + 1) MOD hashTable.size
        If index == startIndex:
            Return "Hash table is full"
    hashTable.faculties[index] = faculty
    hashTable.occupied[index] = true
```

### Search Faculty
```
Algorithm SearchFaculty(hashTable, id):
    index = Hash(id, hashTable.size)
    startIndex = index
    While hashTable.occupied[index] is true:
        If hashTable.faculties[index].id == id:
            Return hashTable.faculties[index]
        index = (index + 1) MOD hashTable.size
        If index == startIndex:
            Break
    Return NULL
```

### Delete Faculty
```
Algorithm DeleteFaculty(hashTable, id):
    index = Hash(id, hashTable.size)
    startIndex = index
    While hashTable.occupied[index] is true:
        If hashTable.faculties[index].id == id:
            hashTable.occupied[index] = false
            Return "Faculty deleted successfully"
        index = (index + 1) MOD hashTable.size
        If index == startIndex:
            Break
    Return "Faculty not found"
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define TABLE_SIZE 15
#define MAX_NAME_LENGTH 50
#define MAX_DEPT_LENGTH 30
#define MAX_DESIGNATION_LENGTH 30
struct Faculty_rrd {
    int id_rrd;
    char name_rrd[MAX_NAME_LENGTH];
    char department_rrd[MAX_DEPT_LENGTH];
    char designation_rrd[MAX_DESIGNATION_LENGTH];
    int experience_rrd;
};

struct HashTable_rrd {
    int size_rrd;
    struct Faculty_rrd* faculties_rrd;
    int* occupied_rrd;
};

struct HashTable_rrd* createHashTable_rrd(int size_rrd);
int hash_rrd(int id_rrd, int tableSize_rrd);
int insertFaculty_rrd(struct HashTable_rrd* hashTable_rrd, struct Faculty_rrd faculty_rrd);
struct Faculty_rrd* searchFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd);
int deleteFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd);
void displayFaculty_rrd(struct Faculty_rrd* faculty_rrd);
void displayAllFaculties_rrd(struct HashTable_rrd* hashTable_rrd);
float loadFactor_rrd(struct HashTable_rrd* hashTable_rrd);
int countCollisions_rrd(struct HashTable_rrd* hashTable_rrd);
void freeHashTable_rrd(struct HashTable_rrd* hashTable_rrd);
void createSampleData_rrd(struct HashTable_rrd* hashTable_rrd);
void displayMenu_rrd();
struct HashTable_rrd* createHashTable_rrd(int size_rrd) {
    struct HashTable_rrd* hashTable_rrd = (struct HashTable_rrd*)malloc(sizeof(struct HashTable_rrd));
    hashTable_rrd->size_rrd = size_rrd;
    hashTable_rrd->faculties_rrd = (struct Faculty_rrd*)malloc(size_rrd * sizeof(struct Faculty_rrd));
    hashTable_rrd->occupied_rrd = (int*)malloc(size_rrd * sizeof(int));
    for (int i_rrd = 0; i_rrd < size_rrd; i_rrd++)
{
        hashTable_rrd->occupied_rrd[i_rrd] = 0;
    }
    return hashTable_rrd;
}

int hash_rrd(int id_rrd, int tableSize_rrd) {
    return id_rrd % tableSize_rrd;
}

int insertFaculty_rrd(struct HashTable_rrd* hashTable_rrd, struct Faculty_rrd faculty_rrd) {
    int index_rrd = hash_rrd(faculty_rrd.id_rrd, hashTable_rrd->size_rrd);
    int startIndex_rrd = index_rrd;
    while (hashTable_rrd->occupied_rrd[index_rrd])
{
        if (hashTable_rrd->faculties_rrd[index_rrd].id_rrd == faculty_rrd.id_rrd)
{
            hashTable_rrd->faculties_rrd[index_rrd] = faculty_rrd;
            printf("Faculty with ID %d updated successfully\n", faculty_rrd.id_rrd);
            return 1;
        }

        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
        if (index_rrd == startIndex_rrd)
{
            printf("Hash table is full! Cannot insert faculty with ID %d\n", faculty_rrd.id_rrd);
            return 0;
        }
    }

    hashTable_rrd->faculties_rrd[index_rrd] = faculty_rrd;
    hashTable_rrd->occupied_rrd[index_rrd] = 1;
    printf("Faculty %s (ID: %d) inserted at index %d\n", faculty_rrd.name_rrd, faculty_rrd.id_rrd, index_rrd);
    return 1;
}

struct Faculty_rrd* searchFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd) {
    int index_rrd = hash_rrd(id_rrd, hashTable_rrd->size_rrd);
    int startIndex_rrd = index_rrd;
    while (hashTable_rrd->occupied_rrd[index_rrd])
{
        if (hashTable_rrd->faculties_rrd[index_rrd].id_rrd == id_rrd)
{
            return &(hashTable_rrd->faculties_rrd[index_rrd]);
        }

        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
        if (index_rrd == startIndex_rrd)
{
            break;
        }
    }
    return NULL;
}

int deleteFaculty_rrd(struct HashTable_rrd* hashTable_rrd, int id_rrd) {
    int index_rrd = hash_rrd(id_rrd, hashTable_rrd->size_rrd);
    int startIndex_rrd = index_rrd;
    while (hashTable_rrd->occupied_rrd[index_rrd])
{
        if (hashTable_rrd->faculties_rrd[index_rrd].id_rrd == id_rrd)
{
            hashTable_rrd->occupied_rrd[index_rrd] = 0;
            printf("Faculty with ID %d deleted successfully\n", id_rrd);
            return 1;
        }

        index_rrd = (index_rrd + 1) % hashTable_rrd->size_rrd;
        if (index_rrd == startIndex_rrd)
{
            break;
        }
    }

    printf("Faculty with ID %d not found\n", id_rrd);
    return 0;
}

void displayFaculty_rrd(struct Faculty_rrd* faculty_rrd) {
    if (faculty_rrd != NULL)
{
        printf("ID: %d\n", faculty_rrd->id_rrd);
        printf("Name: %s\n", faculty_rrd->name_rrd);
        printf("Department: %s\n", faculty_rrd->department_rrd);
        printf("Designation: %s\n", faculty_rrd->designation_rrd);
        printf("Experience: %d years\n", faculty_rrd->experience_rrd);
    } else
{

        printf("Faculty record not found\n");
    }
}

void displayAllFaculties_rrd(struct HashTable_rrd* hashTable_rrd) {
    printf("\nAll Faculty Records:\n");
    printf("Index\tID\tName\t\t\tDepartment\t\tDesignation\t\tExperience\n");
    printf("-----\t--\t----\t\t\t----------\t\t----------\t\t----------\n");
    int count_rrd = 0;
    for (int i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
{
        if (hashTable_rrd->occupied_rrd[i_rrd])
{
            struct Faculty_rrd* faculty_rrd = &(hashTable_rrd->faculties_rrd[i_rrd]);
            printf("%d\t%d\t%-20s\t%-20s\t%-20s\t%d years\n", 
                   i_rrd, faculty_rrd->id_rrd, faculty_rrd->name_rrd, 
                   faculty_rrd->department_rrd, faculty_rrd->designation_rrd, 
                   faculty_rrd->experience_rrd);
            count_rrd++;
        }
    }

    if (count_rrd == 0)
{
        printf("No faculty records found\n");
    } else
{

        printf("\nTotal faculties: %d\n", count_rrd);
    }
}

float loadFactor_rrd(struct HashTable_rrd* hashTable_rrd)
{
    int occupiedSlots_rrd = 0;
    for (int i_rrd = 0; i_rrd < hashTable_rrd->size_rrd; i_rrd++)
{
        if (hashTable_rrd->occupied_rrd[i_rrd])
{
            occupiedSlots_rrd++;
        }
    }
    return (float)occupiedSlots_rrd / hashTable_rrd->size_rrd;
}

void freeHashTable_rrd(struct HashTable_rrd* hashTable_rrd) {
    free(hashTable_rrd->faculties_rrd);
    free(hashTable_rrd->occupied_rrd);
    free(hashTable_rrd);
}

void createSampleData_rrd(struct HashTable_rrd* hashTable_rrd) {
    struct Faculty_rrd faculties_rrd[] = {
        {101, "Dr. Alice Johnson", "Computer Science", "Professor", 15},
        {102, "Dr. Bob Smith", "Electronics", "Associate Professor", 12},
        {103, "Dr. Charlie Brown", "Mechanical", "Assistant Professor", 8},
        {104, "Dr. Diana Prince", "Civil", "Professor", 18},
        {105, "Dr. Eve Wilson", "Electrical", "Associate Professor", 10},
        {106, "Dr. Frank Miller", "Chemical", "Assistant Professor", 6},
        {107, "Dr. Grace Lee", "Physics", "Professor", 20},
        {108, "Dr. Henry Davis", "Mathematics", "Associate Professor", 14},
        {109, "Dr. Ivy Clark", "Biotechnology", "Assistant Professor", 7},
        {110, "Dr. Jack White", "English", "Professor", 16}
    };

    int numFaculties_rrd = sizeof(faculties_rrd) / sizeof(faculties_rrd[0]);
    for (int i_rrd = 0; i_rrd < numFaculties_rrd; i_rrd++)
{
        insertFaculty_rrd(hashTable_rrd, faculties_rrd[i_rrd]);
    }

    printf("Sample faculty data created successfully!\n");
}

void addFacultyInteractive_rrd(struct HashTable_rrd* hashTable_rrd) {
    struct Faculty_rrd faculty_rrd;
    printf("Enter faculty ID: ");
    scanf("%d", &faculty_rrd.id_rrd);
    if (searchFaculty_rrd(hashTable_rrd, faculty_rrd.id_rrd) != NULL)
{
        printf("Faculty with ID %d already exists! Updating record...\n", faculty_rrd.id_rrd);
    }

    printf("Enter name: ");
    scanf(" %[^\n]s", faculty_rrd.name_rrd);
    printf("Enter department: ");
    scanf(" %[^\n]s", faculty_rrd.department_rrd);
    printf("Enter designation: ");
    scanf(" %[^\n]s", faculty_rrd.designation_rrd);
    printf("Enter experience (years): ");
    scanf("%d", &faculty_rrd.experience_rrd);
    if (faculty_rrd.experience_rrd < 0)
{
        printf("Invalid experience! Experience cannot be negative.\n");
        return;
    }

    insertFaculty_rrd(hashTable_rrd, faculty_rrd);
}

void displayMenu_rrd() {
    printf("\n===== Faculty Database Management System =====\n");
    printf("1. Add Faculty Record\n");
    printf("2. Search Faculty by ID\n");
    printf("3. Delete Faculty by ID\n");
    printf("4. Display All Faculties\n");
    printf("5. Show Load Factor\n");
    printf("6. Create Sample Data\n");
    printf("7. Exit\n");
    printf("==========================================\n");
    printf("Enter your choice: ");
}

int main() {
    printf("Welcome to Faculty Database Management System using Hash Table!\n");
    printf("Using MOD hash function with linear probing collision handling.\n");
    int tableSize_rrd;
    printf("Enter the size of the hash table: ");
    scanf("%d", &tableSize_rrd);
    if (tableSize_rrd <= 0)
{
        printf("Invalid table size! Must be positive.\n");
        return 1;
    }

    struct HashTable_rrd* hashTable_rrd = createHashTable_rrd(tableSize_rrd);
    int choice_rrd;
    while (1)
{
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
{
{
                addFacultyInteractive_rrd(hashTable_rrd);
                break;
            }

{
                int id_rrd;
                printf("Enter faculty ID to search: ");
                scanf("%d", &id_rrd);
                struct Faculty_rrd* faculty_rrd = searchFaculty_rrd(hashTable_rrd, id_rrd);
                if (faculty_rrd != NULL)
{
                    printf("\nFaculty Record Found:\n");
                    printf("====================\n");
                    displayFaculty_rrd(faculty_rrd);
                } else
{

                    printf("Faculty with ID %d not found\n", id_rrd);
                }
                break;
            }

{
                int id_rrd;
                printf("Enter faculty ID to delete: ");
                scanf("%d", &id_rrd);
                deleteFaculty_rrd(hashTable_rrd, id_rrd);
                break;
            }

{
                displayAllFaculties_rrd(hashTable_rrd);
                break;
            }

{
                float loadFactor_rrd_val = loadFactor_rrd(hashTable_rrd);
                printf("Load Factor: %.2f\n", loadFactor_rrd_val);
                break;
            }

{
                createSampleData_rrd(hashTable_rrd);
                displayAllFaculties_rrd(hashTable_rrd);
                break;
            }

{
                printf("Thank you for using Faculty Database Management System!\n");
                freeHashTable_rrd(hashTable_rrd);
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
Welcome to Faculty Database Management System using Hash Table!
Using MOD hash function with linear probing collision handling.
Enter the size of the hash table: 15
===== Faculty Database Management System =====
1. Add Faculty Record
2. Search Faculty by ID
3. Delete Faculty by ID
4. Display All Faculties
5. Show Load Factor
6. Create Sample Data
7. Exit
==========================================
Enter your choice: 6
Sample faculty data created successfully!
All Faculty Records:
Index	ID	Name			Department		Designation		Experience
-----	--	----			----------		----------		----------
1	101	Dr. Alice Johnson	Computer Science	Professor		15 years
2	102	Dr. Bob Smith		Electronics		Associate Professor	12 years
3	103	Dr. Charlie Brown	Mechanical		Assistant Professor	8 years
4	104	Dr. Diana Prince	Civil			Professor		18 years
5	105	Dr. Eve Wilson		Electrical		Associate Professor	10 years
6	106	Dr. Frank Miller	Chemical		Assistant Professor	6 years
7	107	Dr. Grace Lee		Physics			Professor		20 years
8	108	Dr. Henry Davis		Mathematics		Associate Professor	14 years
9	109	Dr. Ivy Clark		Biotechnology		Assistant Professor	7 years
10	110	Dr. Jack White		English			Professor		16 years
Total faculties: 10
===== Faculty Database Management System =====
1. Add Faculty Record
2. Search Faculty by ID
3. Delete Faculty by ID
4. Display All Faculties
5. Show Load Factor
6. Create Sample Data
7. Exit
==========================================
Enter your choice: 2
Enter faculty ID to search: 105
Faculty Record Found:
====================
ID: 105
Name: Dr. Eve Wilson
Department: Electrical
Designation: Associate Professor
Experience: 10 years
===== Faculty Database Management System =====
1. Add Faculty Record
2. Search Faculty by ID
3. Delete Faculty by ID
4. Display All Faculties
5. Show Load Factor
6. Create Sample Data
7. Exit
==========================================
Enter your choice: 3
Enter faculty ID to delete: 103
Faculty with ID 103 deleted successfully
All Faculty Records:
Index	ID	Name			Department		Designation		Experience
-----	--	----			----------		----------		----------
1	101	Dr. Alice Johnson	Computer Science	Professor		15 years
2	102	Dr. Bob Smith		Electronics		Associate Professor	12 years
4	104	Dr. Diana Prince	Civil			Professor		18 years
5	105	Dr. Eve Wilson		Electrical		Associate Professor	10 years
6	106	Dr. Frank Miller	Chemical		Assistant Professor	6 years
7	107	Dr. Grace Lee		Physics			Professor		20 years
8	108	Dr. Henry Davis		Mathematics		Associate Professor	14 years
9	109	Dr. Ivy Clark		Biotechnology		Assistant Professor	7 years
10	110	Dr. Jack White		English			Professor		16 years
Total faculties: 9
===== Faculty Database Management System =====
1. Add Faculty Record
2. Search Faculty by ID
3. Delete Faculty by ID
4. Display All Faculties
5. Show Load Factor
6. Create Sample Data
7. Exit
==========================================
Enter your choice: 5
Load Factor: 0.60
```

## Dry Run

For a hash table of size 15 with MOD hash function and linear probing:

1. **Insertions**:
   - Insert faculty (101, "Dr. Alice Johnson", "Computer Science", "Professor", 15): hash(101) = 101 % 15 = 11 → Insert at index 11
   - Insert faculty (102, "Dr. Bob Smith", "Electronics", "Associate Professor", 12): hash(102) = 102 % 15 = 12 → Insert at index 12
   - Insert faculty (103, "Dr. Charlie Brown", "Mechanical", "Assistant Professor", 8): hash(103) = 103 % 15 = 13 → Insert at index 13
   - Insert faculty (104, "Dr. Diana Prince", "Civil", "Professor", 18): hash(104) = 104 % 15 = 14 → Insert at index 14
   - Insert faculty (105, "Dr. Eve Wilson", "Electrical", "Associate Professor", 10): hash(105) = 105 % 15 = 0 → Insert at index 0
   - Insert faculty (106, "Dr. Frank Miller", "Chemical", "Assistant Professor", 6): hash(106) = 106 % 15 = 1 → Insert at index 1
   - Insert faculty (107, "Dr. Grace Lee", "Physics", "Professor", 20): hash(107) = 107 % 15 = 2 → Insert at index 2

2. **Search for faculty ID 105**:
   - hash(105) = 105 % 15 = 0
   - Check index 0:
     * Found faculty with ID 105
     * Return faculty record: Dr. Eve Wilson, Electrical, Associate Professor, 10 years

3. **Delete faculty with ID 103**:
   - hash(103) = 103 % 15 = 13
   - Check index 13:
     * Found faculty with ID 103 (Dr. Charlie Brown)
     * Mark index 13 as empty

4. **Load Factor**:
   - Total faculties: 9
   - Table size: 15
   - Load factor: 9/15 = 0.6

## Conclusion

The implementation demonstrates a faculty database management system using hash table with linear probing collision resolution. Key features include:

1. **Faculty Record Management**: Complete CRUD operations for faculty records
2. **Hash Table Implementation**: Efficient storage and retrieval using MOD hash function
3. **Linear Probing**: Collision resolution technique for handling hash collisions
4. **Data Validation**: Input validation for experience and duplicate IDs

**Time Complexities**:
- Insert Faculty: O(1) average case, O(n) worst case (when table is full or many collisions)
- Search Faculty: O(1) average case, O(n) worst case (when faculty not found or many collisions)
- Delete Faculty: O(1) average case, O(n) worst case (when faculty not found or many collisions)
- Display All Faculties: O(n) where n is table size

**Space Complexity**: O(n) where n is table size

Linear probing has advantages and disadvantages:

**Advantages**:
1. **Simple Implementation**: Easy to understand and implement
2. **Good Cache Performance**: Sequential memory access
3. **No Extra Memory**: No additional pointers or structures needed
4. **Efficient for Small Tables**: Works well when load factor is low

**Disadvantages**:
1. **Primary Clustering**: Consecutive occupied slots form clusters, increasing collision probability
2. **Performance Degradation**: As load factor increases, performance degrades significantly
3. **Deletion Complexity**: Requires special handling (marking as deleted rather than empty)

The implementation handles edge cases properly:
- Hash table full condition
- Faculty not found during search/delete
- Faculty already exists during insertion (update)
- Invalid experience validation (non-negative)
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Complete faculty record display with formatted output
- Load factor calculation
- Sample data creation for testing
- Interactive menu system
- Complete error handling

In real-world applications, this system could be extended to:
1. Support dynamic resizing
2. Implement file persistence
3. Add sorting and filtering capabilities
4. Support different search criteria (name, department, designation)
5. Implement backup and restore functionality
6. Add statistical analysis (department-wise count, experience distribution)

Hash tables are fundamental data structures used in:
1. **Database Indexing**: Fast data retrieval
2. **Caching**: Quick access to frequently used data
3. **Compiler Design**: Symbol tables for variables and functions
4. **Networking**: Routing tables and packet filtering
5. **Cryptography**: Hash functions for data integrity

This implementation provides a solid foundation for understanding hash tables and their practical applications in faculty database management systems, which are essential in educational institutions for efficient data storage and retrieval.
