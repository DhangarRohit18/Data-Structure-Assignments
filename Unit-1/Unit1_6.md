# Assignment 6: Student Searching Implementation

Implementation to search for a specific student in a Computer Engineering Department function using appropriate searching methods.

## Pseudo Code

### Linear Search for Student
```
Algorithm LinearSearchStudent(students, n, target_name, target_roll):
    For i = 0 to n-1:
        If students[i].name == target_name AND students[i].roll_no == target_roll:
            Return i
    Return -1
```

### Binary Search for Student (if sorted by roll_no)
```
Algorithm BinarySearchStudent(students, left, right, target_roll):
    If left > right:
        Return -1
    
    mid = (left + right) / 2
    
    If students[mid].roll_no == target_roll:
        If students[mid].name == target_name:
            Return mid
        Else:

            left_result = BinarySearchStudent(students, left, mid-1, target_roll)
            If left_result != -1:
                Return left_result
            Return BinarySearchStudent(students, mid+1, right, target_roll)
    
    If students[mid].roll_no > target_roll:
        Return BinarySearchStudent(students, left, mid-1, target_roll)
    Else:
        Return BinarySearchStudent(students, mid+1, right, target_roll)
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_STUDENTS 1000

struct Student_rrd {
    char name_rrd[50];
    int roll_no_rrd;
    char division_rrd[10];
    char year_rrd[10];
};

int linearSearchStudent_rrd(struct Student_rrd students_rrd[], int n_rrd, char* target_name_rrd, int target_roll_rrd);
int binarySearchStudent_rrd(struct Student_rrd students_rrd[], int left_rrd, int right_rrd, char* target_name_rrd, int target_roll_rrd);
void displayStudent_rrd(struct Student_rrd student_rrd);
void inputStudents_rrd(struct Student_rrd students_rrd[], int n_rrd);

int main() {
    int n_rrd, target_roll_rrd, result_rrd;
    char target_name_rrd[50];
    struct Student_rrd students_rrd[MAX_STUDENTS];
    
    printf("Enter number of students: ");
    scanf("%d", &n_rrd);
    
    if (n_rrd <= 0 || n_rrd > MAX_STUDENTS) {
        printf("Invalid number of students!\n");
        return 1;
    }
    
    inputStudents_rrd(students_rrd, n_rrd);
    
    printf("\nEnter the name of student to search (XYZ): ");
    scanf("%s", target_name_rrd);
    printf("Enter the roll number of student to search (17): ");
    scanf("%d", &target_roll_rrd);
    

    result_rrd = linearSearchStudent_rrd(students_rrd, n_rrd, target_name_rrd, target_roll_rrd);
    
    if (result_rrd != -1) {
        printf("\nStudent found using Linear Search at position %d:\n", result_rrd + 1);
        displayStudent_rrd(students_rrd[result_rrd]);
    } else {
        printf("\nStudent not found using Linear Search!\n");
    }
    
    return 0;
}

void inputStudents_rrd(struct Student_rrd students_rrd[], int n_rrd) {
    int i_rrd;
    printf("\nEnter student details:\n");
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        printf("Student %d:\n", i_rrd + 1);
        printf("  Name: ");
        scanf("%s", students_rrd[i_rrd].name_rrd);
        printf("  Roll No: ");
        scanf("%d", &students_rrd[i_rrd].roll_no_rrd);
        printf("  Division (S.Y./T.Y./B.Tech.): ");
        scanf("%s", students_rrd[i_rrd].division_rrd);
        printf("  Year: ");
        scanf("%s", students_rrd[i_rrd].year_rrd);
        printf("\n");
    }
}

int linearSearchStudent_rrd(struct Student_rrd students_rrd[], int n_rrd, char* target_name_rrd, int target_roll_rrd) {
    int i_rrd;
    for (i_rrd = 0; i_rrd < n_rrd; i_rrd++) {
        if (students_rrd[i_rrd].roll_no_rrd == target_roll_rrd && 
            strcmp(students_rrd[i_rrd].name_rrd, target_name_rrd) == 0) {
            return i_rrd;
        }
    }
    return -1;
}

void displayStudent_rrd(struct Student_rrd student_rrd) {
    printf("Name: %s\n", student_rrd.name_rrd);
    printf("Roll No: %d\n", student_rrd.roll_no_rrd);
    printf("Division: %s\n", student_rrd.division_rrd);
    printf("Year: %s\n", student_rrd.year_rrd);
}
```

## Output

```
Enter number of students: 5

Enter student details:
Student 1:
  Name: ABC
  Roll No: 10
  Division (S.Y./T.Y./B.Tech.): S.Y.
  Year: 2023

Student 2:
  Name: DEF
  Roll No: 15
  Division (S.Y./T.Y./B.Tech.): T.Y.
  Year: 2022

Student 3:
  Name: XYZ
  Roll No: 17
  Division (S.Y./T.Y./B.Tech.): S.Y.
  Year: 2023

Student 4:
  Name: GHI
  Roll No: 20
  Division (S.Y./T.Y./B.Tech.): B.Tech.
  Year: 2021

Student 5:
  Name: JKL
  Roll No: 25
  Division (S.Y./T.Y./B.Tech.): S.Y.
  Year: 2023

Enter the name of student to search (XYZ): XYZ
Enter the roll number of student to search (17): 17

Student found using Linear Search at position 3:
Name: XYZ
Roll No: 17
Division: S.Y.
Year: 2023
```

## Dry Run

For a list of 5 students with the target student XYZ having roll no 17 at position 3:

1. `linearSearchStudent_rrd()`:
   - Start with i = 0
   - Compare student at index 0: ABC (roll 10) ≠ XYZ (roll 17) → Continue
   - Compare student at index 1: DEF (roll 15) ≠ XYZ (roll 17) → Continue
   - Compare student at index 2: XYZ (roll 17) = XYZ (roll 17) → Match found
   - Return index 2

2. Result:
   - Student found at position 3 (index 2)
   - Display student details

## Conclusion

The implementation demonstrates student searching using linear search, which is appropriate for unsorted data. Linear search has O(n) time complexity, making it suitable for small to medium datasets. For larger sorted datasets, binary search with O(log n) complexity would be more efficient.

The program handles the specific requirement of identifying a student by both name and roll number, ensuring accurate identification. In real-world applications, student roll numbers are typically unique, but the implementation checks both name and roll number for additional verification.