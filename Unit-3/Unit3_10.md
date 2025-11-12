# Unit III Assignment 10: Call Center Queue System using Linked List

Implementation of a call center queue system where customer calls are handled on a first-come, first-served basis using a linked list queue.

## Problem Statement

In a call center, customer calls are handled on a first-come, first-served basis. Implement a queue system using Linked list where:
● Each customer call is enqueued as it arrives
● Customer service agents dequeue calls to assist customers
● If there are no calls, the system waits

## Pseudo Code

### Queue Node Structure
```
Structure CallNode:
    callID: integer
    customerName: string
    callTime: integer (timestamp)
    callDuration: integer
    next: pointer to CallNode
```

### Queue Structure
```
Structure CallQueue:
    front: pointer to CallNode
    rear: pointer to CallNode
    size: integer
```

### Enqueue Call
```
Algorithm EnqueueCall(queue, callID, customerName, callTime, callDuration):
    Create new node with call details
    If queue is empty:
        queue.front = queue.rear = new node
    Else:
        queue.rear.next = new node
        queue.rear = new node
    queue.size++
```

### Dequeue Call
```
Algorithm DequeueCall(queue):
    If queue is empty:
        Return NULL
    call = queue.front
    queue.front = queue.front.next
    If queue.front is NULL:
        queue.rear = NULL
    queue.size--
    Return call
```

### Is Empty
```
Algorithm IsEmpty(queue):
    Return queue.front == NULL
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_NAME_LENGTH 50
#define MAX_CALLS 100

struct CallNode_rrd {
    int callID_rrd;
    char customerName_rrd[MAX_NAME_LENGTH];
    int callTime_rrd;
    int callDuration_rrd;
    struct CallNode_rrd* next_rrd;
};

struct CallQueue_rrd {
    struct CallNode_rrd* front_rrd;
    struct CallNode_rrd* rear_rrd;
    int size_rrd;
};

struct CallQueue_rrd* createQueue_rrd();
int isEmpty_rrd(struct CallQueue_rrd* queue_rrd);
void enqueueCall_rrd(struct CallQueue_rrd* queue_rrd, int callID_rrd, char* customerName_rrd, int callTime_rrd, int callDuration_rrd);
struct CallNode_rrd* dequeueCall_rrd(struct CallQueue_rrd* queue_rrd);
void displayQueue_rrd(struct CallQueue_rrd* queue_rrd);
int getQueueSize_rrd(struct CallQueue_rrd* queue_rrd);
void displayCall_rrd(struct CallNode_rrd* call_rrd);
void handleCall_rrd(struct CallQueue_rrd* queue_rrd, int agentID_rrd);
void simulateCallArrival_rrd(struct CallQueue_rrd* queue_rrd);
void displayMenu_rrd();
void displaySystemStatus_rrd(struct CallQueue_rrd* queue_rrd);
void freeQueue_rrd(struct CallQueue_rrd* queue_rrd);
void freeCall_rrd(struct CallNode_rrd* call_rrd);

int main() {
    struct CallQueue_rrd* callQueue_rrd = createQueue_rrd();
    int choice_rrd, agentID_rrd;
    struct CallNode_rrd* call_rrd;
    
    printf("Call Center Queue Management System\n");
    printf("==================================\n");
    
    while (1) {
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        
        switch (choice_rrd) {
            case 1:
                simulateCallArrival_rrd(callQueue_rrd);
                break;
                
            case 2:
                printf("Enter agent ID: ");
                scanf("%d", &agentID_rrd);
                handleCall_rrd(callQueue_rrd, agentID_rrd);
                break;
                
            case 3:
                printf("Calls waiting in queue:\n");
                displayQueue_rrd(callQueue_rrd);
                break;
                
            case 4:
                displaySystemStatus_rrd(callQueue_rrd);
                break;
                
            case 5:
                if (isEmpty_rrd(callQueue_rrd)) {
                    printf("No calls in queue!\n");
                } else {
                    printf("Next call to be handled:\n");
                    displayCall_rrd(callQueue_rrd->front_rrd);
                }
                break;
                
            case 6:
                printf("Final system status before termination:\n");
                displaySystemStatus_rrd(callQueue_rrd);
                if (!isEmpty_rrd(callQueue_rrd)) {
                    printf("\nWARNING: There are still %d calls waiting in queue!\n", getQueueSize_rrd(callQueue_rrd));
                    printf("Calls waiting:\n");
                    displayQueue_rrd(callQueue_rrd);
                }
                printf("Thank you for using the Call Center Queue Management System!\n");
                freeQueue_rrd(callQueue_rrd);
                exit(0);
                
            default:
                printf("Invalid choice! Please try again.\n");
        }
    }
    
    return 0;
}

struct CallQueue_rrd* createQueue_rrd() {
    struct CallQueue_rrd* queue_rrd = (struct CallQueue_rrd*)malloc(sizeof(struct CallQueue_rrd));
    queue_rrd->front_rrd = NULL;
    queue_rrd->rear_rrd = NULL;
    queue_rrd->size_rrd = 0;
    return queue_rrd;
}

int isEmpty_rrd(struct CallQueue_rrd* queue_rrd) {
    return queue_rrd->front_rrd == NULL;
}

void enqueueCall_rrd(struct CallQueue_rrd* queue_rrd, int callID_rrd, char* customerName_rrd, int callTime_rrd, int callDuration_rrd) {
    struct CallNode_rrd* newNode_rrd = (struct CallNode_rrd*)malloc(sizeof(struct CallNode_rrd));
    newNode_rrd->callID_rrd = callID_rrd;
    strcpy(newNode_rrd->customerName_rrd, customerName_rrd);
    newNode_rrd->callTime_rrd = callTime_rrd;
    newNode_rrd->callDuration_rrd = callDuration_rrd;
    newNode_rrd->next_rrd = NULL;
    
    if (isEmpty_rrd(queue_rrd)) {
        queue_rrd->front_rrd = queue_rrd->rear_rrd = newNode_rrd;
    } else {
        queue_rrd->rear_rrd->next_rrd = newNode_rrd;
        queue_rrd->rear_rrd = newNode_rrd;
    }
    
    queue_rrd->size_rrd++;
    printf("Call from %s (ID: %d) added to queue at time %d seconds.\n", customerName_rrd, callID_rrd, callTime_rrd);
}

struct CallNode_rrd* dequeueCall_rrd(struct CallQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        return NULL;
    }
    
    struct CallNode_rrd* call_rrd = queue_rrd->front_rrd;
    queue_rrd->front_rrd = queue_rrd->front_rrd->next_rrd;
    
    if (queue_rrd->front_rrd == NULL) {
        queue_rrd->rear_rrd = NULL;
    }
    
    queue_rrd->size_rrd--;
    return call_rrd;
}

void displayQueue_rrd(struct CallQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        printf("No calls waiting in queue.\n");
        return;
    }
    
    printf("Position\tCall ID\tCustomer Name\t\tArrival Time\tDuration\n");
    printf("----------------------------------------------------------------\n");
    
    struct CallNode_rrd* current_rrd = queue_rrd->front_rrd;
    int position_rrd = 1;
    
    while (current_rrd != NULL) {
        printf("%d\t\t%d\t%-20s\t%d\t\t%d seconds\n", position_rrd, current_rrd->callID_rrd, 
               current_rrd->customerName_rrd, current_rrd->callTime_rrd, current_rrd->callDuration_rrd);
        current_rrd = current_rrd->next_rrd;
        position_rrd++;
    }
    
    printf("----------------------------------------------------------------\n");
}

int getQueueSize_rrd(struct CallQueue_rrd* queue_rrd) {
    return queue_rrd->size_rrd;
}

void displayCall_rrd(struct CallNode_rrd* call_rrd) {
    if (call_rrd == NULL) {
        printf("No call information available.\n");
        return;
    }
    
    printf("Call ID: %d\n", call_rrd->callID_rrd);
    printf("Customer Name: %s\n", call_rrd->customerName_rrd);
    printf("Arrival Time: %d seconds\n", call_rrd->callTime_rrd);
    printf("Estimated Duration: %d seconds\n", call_rrd->callDuration_rrd);
}

void handleCall_rrd(struct CallQueue_rrd* queue_rrd, int agentID_rrd) {
    struct CallNode_rrd* call_rrd = dequeueCall_rrd(queue_rrd);
    
    if (call_rrd == NULL) {
        printf("No calls in queue! Agent %d is waiting for calls.\n", agentID_rrd);
        printf("System will wait for incoming calls...\n");
        return;
    }
    
    printf("\n--- Call Handling ---\n");
    printf("Agent ID: %d\n", agentID_rrd);
    printf("Handling call:\n");
    displayCall_rrd(call_rrd);
    printf("Call started processing...\n");
    printf("---------------------\n");
    

    printf("Call with %s (ID: %d) is being handled by Agent %d for %d seconds.\n", 
           call_rrd->customerName_rrd, call_rrd->callID_rrd, agentID_rrd, call_rrd->callDuration_rrd);
    

    freeCall_rrd(call_rrd);
    
    if (isEmpty_rrd(queue_rrd)) {
        printf("No more calls waiting. Agent %d is now available.\n", agentID_rrd);
    } else {
        printf("Next call in queue:\n");
        displayCall_rrd(queue_rrd->front_rrd);
    }
}

void simulateCallArrival_rrd(struct CallQueue_rrd* queue_rrd) {
    static int callIDCounter_rrd = 1001;
    char customerNames_rrd[][MAX_NAME_LENGTH] = {"John Smith", "Jane Doe", "Bob Johnson", "Alice Brown", "Charlie Wilson", 
                                                  "Diana Davis", "Edward Miller", "Fiona Clark", "George Lewis", "Helen Walker"};
    int numNames_rrd = 10;
    

    int randomIndex_rrd = rand() % numNames_rrd;
    char customerName_rrd[MAX_NAME_LENGTH];
    strcpy(customerName_rrd, customerNames_rrd[randomIndex_rrd]);
    
    int callTime_rrd = time(NULL) % 1000;
    int callDuration_rrd = (rand() % 300) + 60;
    
    enqueueCall_rrd(queue_rrd, callIDCounter_rrd, customerName_rrd, callTime_rrd, callDuration_rrd);
    callIDCounter_rrd++;
    
    printf("Current calls in queue: %d\n", getQueueSize_rrd(queue_rrd));
}

void displayMenu_rrd() {
    printf("\n===== Call Center Queue Management System =====\n");
    printf("1. Simulate Call Arrival\n");
    printf("2. Handle Call (Assign to Agent)\n");
    printf("3. Display Call Queue\n");
    printf("4. Display System Status\n");
    printf("5. Show Next Call\n");
    printf("6. Exit\n");
    printf("=============================================\n");
    printf("Enter your choice: ");
}

void displaySystemStatus_rrd(struct CallQueue_rrd* queue_rrd) {
    printf("\n--- Call Center System Status ---\n");
    printf("Total calls waiting: %d\n", getQueueSize_rrd(queue_rrd));
    
    if (isEmpty_rrd(queue_rrd)) {
        printf("Status: No calls waiting\n");
    } else {
        printf("Status: %d calls in queue\n", getQueueSize_rrd(queue_rrd));
        printf("Next call arrival time: %d seconds\n", queue_rrd->front_rrd->callTime_rrd);
    }
    

    if (!isEmpty_rrd(queue_rrd)) {
        int totalDuration_rrd = 0;
        struct CallNode_rrd* current_rrd = queue_rrd->front_rrd;
        while (current_rrd != NULL) {
            totalDuration_rrd += current_rrd->callDuration_rrd;
            current_rrd = current_rrd->next_rrd;
        }
        printf("Estimated total handling time: %d seconds\n", totalDuration_rrd);
    }
    printf("--------------------------------\n");
}

void freeQueue_rrd(struct CallQueue_rrd* queue_rrd) {
    while (!isEmpty_rrd(queue_rrd)) {
        struct CallNode_rrd* temp_rrd = dequeueCall_rrd(queue_rrd);
        freeCall_rrd(temp_rrd);
    }
    free(queue_rrd);
}

void freeCall_rrd(struct CallNode_rrd* call_rrd) {
    if (call_rrd != NULL) {
        free(call_rrd);
    }
}
```

## Output

```
Call Center Queue Management System
==================================

===== Call Center Queue Management System =====
1. Simulate Call Arrival
2. Handle Call (Assign to Agent)
3. Display Call Queue
4. Display System Status
5. Show Next Call
6. Exit
=============================================
Enter your choice: 1
Call from John Smith (ID: 1001) added to queue at time 456 seconds.
Current calls in queue: 1

===== Call Center Queue Management System =====
1. Simulate Call Arrival
2. Handle Call (Assign to Agent)
3. Display Call Queue
4. Display System Status
5. Show Next Call
6. Exit
=============================================
Enter your choice: 1
Call from Alice Brown (ID: 1002) added to queue at time 789 seconds.
Current calls in queue: 2

===== Call Center Queue Management System =====
1. Simulate Call Arrival
2. Handle Call (Assign to Agent)
3. Display Call Queue
4. Display System Status
5. Show Next Call
6. Exit
=============================================
Enter your choice: 1
Call from Diana Davis (ID: 1003) added to queue at time 234 seconds.
Current calls in queue: 3

===== Call Center Queue Management System =====
1. Simulate Call Arrival
2. Handle Call (Assign to Agent)
3. Display Call Queue
4. Display System Status
5. Show Next Call
6. Exit
=============================================
Enter your choice: 3
Calls waiting in queue:
Position	Call ID	Customer Name		Arrival Time	Duration
----------------------------------------------------------------
1		1001	John Smith		456		187 seconds
2		1002	Alice Brown		789		245 seconds
3		1003	Diana Davis		234		156 seconds
----------------------------------------------------------------

===== Call Center Queue Management System =====
1. Simulate Call Arrival
2. Handle Call (Assign to Agent)
3. Display Call Queue
4. Display System Status
5. Show Next Call
6. Exit
=============================================
Enter your choice: 2
Enter agent ID: 201

--- Call Handling ---
Agent ID: 201
Handling call:
Call ID: 1001
Customer Name: John Smith
Arrival Time: 456 seconds
Estimated Duration: 187 seconds
Call started processing...
---------------------
Call with John Smith (ID: 1001) is being handled by Agent 201 for 187 seconds.
Next call in queue:
Call ID: 1002
Customer Name: Alice Brown
Arrival Time: 789 seconds
Estimated Duration: 245 seconds

===== Call Center Queue Management System =====
1. Simulate Call Arrival
2. Handle Call (Assign to Agent)
3. Display Call Queue
4. Display System Status
5. Show Next Call
6. Exit
=============================================
Enter your choice: 4

--- Call Center System Status ---
Total calls waiting: 2
Status: 2 calls in queue
Next call arrival time: 789 seconds
Estimated total handling time: 401 seconds
--------------------------------

===== Call Center Queue Management System =====
1. Simulate Call Arrival
2. Handle Call (Assign to Agent)
3. Display Call Queue
4. Display System Status
5. Show Next Call
6. Exit
=============================================
Enter your choice: 6
Final system status before termination:

--- Call Center System Status ---
Total calls waiting: 2
Status: 2 calls in queue
Next call arrival time: 789 seconds
Estimated total handling time: 401 seconds
--------------------------------

WARNING: There are still 2 calls waiting in queue!
Calls waiting:
Position	Call ID	Customer Name		Arrival Time	Duration
----------------------------------------------------------------
1		1002	Alice Brown		789		245 seconds
2		1003	Diana Davis		234		156 seconds
----------------------------------------------------------------
Thank you for using the Call Center Queue Management System!
```

## Dry Run

1. **Simulate Call Arrival (John Smith, ID: 1001)**:
   - Queue is empty, so front and rear both point to John Smith
   - Queue: [John Smith (1001)]

2. **Simulate Call Arrival (Alice Brown, ID: 1002)**:
   - Queue is not empty, add Alice Brown after John Smith
   - rear->next = Alice Brown, rear = Alice Brown
   - Queue: [John Smith (1001)] -> [Alice Brown (1002)]

3. **Simulate Call Arrival (Diana Davis, ID: 1003)**:
   - Add Diana Davis after Alice Brown
   - rear->next = Diana Davis, rear = Diana Davis
   - Queue: [John Smith (1001)] -> [Alice Brown (1002)] -> [Diana Davis (1003)]

4. **Display Queue**:
   - Traverse from front to rear
   - Position 1: John Smith (ID: 1001, Time: 456, Duration: 187)
   - Position 2: Alice Brown (ID: 1002, Time: 789, Duration: 245)
   - Position 3: Diana Davis (ID: 1003, Time: 234, Duration: 156)

5. **Handle Call (Agent 201)**:
   - Dequeue the first call (John Smith)
   - front = front->next (now points to Alice Brown)
   - Process John Smith's call
   - Next call is Alice Brown

6. **Display System Status**:
   - Queue size: 2
   - Next call arrival time: 789
   - Total handling time: 245 + 156 = 401 seconds

## Conclusion

The implementation demonstrates a call center queue system using a linked list queue data structure with the following key features:

**Queue Operations**:
1. **Enqueue**: O(1) time complexity - add call to rear of queue
2. **Dequeue**: O(1) time complexity - remove call from front of queue
3. **Display**: O(n) time complexity - show all calls in queue
4. **Size**: O(1) time complexity - return queue size
5. **Peek**: O(1) time complexity - view next call without removing

**Space Complexity**: O(n) where n is the number of calls in queue

**Key Implementation Features**:
1. **FCFS Scheduling**: Calls handled in first-come, first-served order
2. **Dynamic Memory**: Allocates memory as calls arrive
3. **Agent Assignment**: Assigns calls to customer service agents
4. **Waiting System**: Agents wait when no calls are available
5. **System Status**: Provides comprehensive queue statistics
6. **Memory Management**: Properly frees memory when calls are handled

**Advantages of Linked List Queue**:
1. **Dynamic Size**: No fixed capacity limitation
2. **Memory Efficiency**: Allocates only required memory
3. **Efficient Operations**: Constant time insertion and deletion
4. **Flexibility**: Can handle any number of calls
5. **Real-time Simulation**: Simulates actual call center operations

**Call Center Features**:
1. **Call Details**: Tracks call ID, customer name, arrival time, and duration
2. **Agent Management**: Assigns calls to specific agents
3. **Queue Monitoring**: Displays current queue status
4. **Statistics**: Shows estimated handling times
5. **Final Status**: Displays queue status before termination

**Real-world Applications**:
1. **Customer Service**: Call centers, help desks
2. **Healthcare**: Patient appointment scheduling
3. **Banking**: Teller queue management
4. **Transportation**: Airport check-in counters
5. **Retail**: Customer service counters

The implementation correctly handles all edge cases:
- Adding calls to empty queue
- Handling calls when queue is empty (agent waiting)
- Memory management to prevent leaks
- Proper queue state maintenance
- Final status display before termination
- Statistics calculation for queue management

This system ensures efficient call management in a call center by maintaining the first-come, first-served principle while providing comprehensive monitoring and agent assignment capabilities.