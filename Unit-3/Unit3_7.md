# Unit III Assignment 7: Pizza Parlour Order System using Circular Queue

Implementation of a pizza parlour order system that accepts maximum n orders and serves them on a first-come, first-served basis using a circular queue.

## Problem Statement

Pizza parlour accepting maximum n orders. Orders are served on an FCFS basis. Order once placed can't be cancelled. Write C++ program to simulate the system using circular QUEUE.

## Pseudo Code

### Circular Queue Structure
```
Structure CircularQueue:
    orders: array of integers (order IDs)
    front: integer
    rear: integer
    size: integer
    capacity: integer
```

### Enqueue Order
```
Algorithm EnqueueOrder(queue, orderID):
    If queue is full:
        Return "Order limit reached"
    If queue is empty:
        queue.front = queue.rear = 0
    Else:
        queue.rear = (queue.rear + 1) % queue.capacity
    queue.orders[queue.rear] = orderID
    queue.size++
```

### Dequeue Order
```
Algorithm DequeueOrder(queue):
    If queue is empty:
        Return "No orders to serve"
    orderID = queue.orders[queue.front]
    If queue has only one element:
        queue.front = queue.rear = -1
    Else:
        queue.front = (queue.front + 1) % queue.capacity
    queue.size--
    Return orderID
```

### Is Full
```
Algorithm IsFull(queue):
    Return (queue.rear + 1) % queue.capacity == queue.front
```

### Is Empty
```
Algorithm IsEmpty(queue):
    Return queue.front == -1
```

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_ORDERS 100

struct CircularQueue_rrd {
    int orders_rrd[MAX_ORDERS];
    int front_rrd;
    int rear_rrd;
    int size_rrd;
    int capacity_rrd;
};

struct CircularQueue_rrd* createQueue_rrd(int capacity_rrd);
int isFull_rrd(struct CircularQueue_rrd* queue_rrd);
int isEmpty_rrd(struct CircularQueue_rrd* queue_rrd);
void enqueueOrder_rrd(struct CircularQueue_rrd* queue_rrd, int orderID_rrd);
int dequeueOrder_rrd(struct CircularQueue_rrd* queue_rrd);
void displayQueue_rrd(struct CircularQueue_rrd* queue_rrd);
int getQueueSize_rrd(struct CircularQueue_rrd* queue_rrd);
int getAvailableSlots_rrd(struct CircularQueue_rrd* queue_rrd);
void displayMenu_rrd();

int main() {
    int capacity_rrd, choice_rrd, orderID_rrd, servedOrder_rrd;
    
    printf("Welcome to Pizza Parlour Order System\n");
    printf("====================================\n");
    printf("Enter maximum number of orders the system can handle: ");
    scanf("%d", &capacity_rrd);
    
    if (capacity_rrd <= 0 || capacity_rrd > MAX_ORDERS) {
        printf("Invalid capacity! Setting to default value of 10.\n");
        capacity_rrd = 10;
    }
    
    struct CircularQueue_rrd* orderQueue_rrd = createQueue_rrd(capacity_rrd);
    
    printf("Pizza Parlour System Initialized with capacity for %d orders\n", capacity_rrd);
    
    while (1) {
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        
        switch (choice_rrd) {
            case 1:
                if (isFull_rrd(orderQueue_rrd)) {
                    printf("Order limit reached! Cannot accept more orders.\n");
                    printf("Available slots: %d\n", getAvailableSlots_rrd(orderQueue_rrd));
                } else {
                    printf("Enter order ID: ");
                    scanf("%d", &orderID_rrd);
                    enqueueOrder_rrd(orderQueue_rrd, orderID_rrd);
                    printf("Order %d placed successfully!\n", orderID_rrd);
                    printf("Current orders in queue: %d\n", getQueueSize_rrd(orderQueue_rrd));
                    printf("Available slots: %d\n", getAvailableSlots_rrd(orderQueue_rrd));
                }
                break;
                
            case 2:
                if (isEmpty_rrd(orderQueue_rrd)) {
                    printf("No orders to serve!\n");
                } else {
                    servedOrder_rrd = dequeueOrder_rrd(orderQueue_rrd);
                    printf("Order %d served successfully!\n", servedOrder_rrd);
                    printf("Remaining orders in queue: %d\n", getQueueSize_rrd(orderQueue_rrd));
                    printf("Available slots: %d\n", getAvailableSlots_rrd(orderQueue_rrd));
                }
                break;
                
            case 3:
                printf("Current order queue:\n");
                displayQueue_rrd(orderQueue_rrd);
                break;
                
            case 4:
                printf("Queue statistics:\n");
                printf("Total capacity: %d\n", orderQueue_rrd->capacity_rrd);
                printf("Current orders: %d\n", getQueueSize_rrd(orderQueue_rrd));
                printf("Available slots: %d\n", getAvailableSlots_rrd(orderQueue_rrd));
                if (isFull_rrd(orderQueue_rrd)) {
                    printf("Status: Queue is FULL\n");
                } else if (isEmpty_rrd(orderQueue_rrd)) {
                    printf("Status: Queue is EMPTY\n");
                } else {
                    printf("Status: Queue has space available\n");
                }
                break;
                
            case 5:
                if (isEmpty_rrd(orderQueue_rrd)) {
                    printf("No orders in queue!\n");
                } else {
                    printf("Next order to be served: %d\n", orderQueue_rrd->orders_rrd[orderQueue_rrd->front_rrd]);
                }
                break;
                
            case 6:
                printf("Thank you for using Pizza Parlour Order System!\n");
                printf("Final queue status:\n");
                printf("Orders served: %d\n", orderQueue_rrd->capacity_rrd - getAvailableSlots_rrd(orderQueue_rrd));
                printf("Orders remaining: %d\n", getQueueSize_rrd(orderQueue_rrd));
                free(orderQueue_rrd);
                exit(0);
                
            default:
                printf("Invalid choice! Please try again.\n");
        }
    }
    
    return 0;
}

struct CircularQueue_rrd* createQueue_rrd(int capacity_rrd) {
    struct CircularQueue_rrd* queue_rrd = (struct CircularQueue_rrd*)malloc(sizeof(struct CircularQueue_rrd));
    queue_rrd->front_rrd = -1;
    queue_rrd->rear_rrd = -1;
    queue_rrd->size_rrd = 0;
    queue_rrd->capacity_rrd = capacity_rrd;
    return queue_rrd;
}

int isFull_rrd(struct CircularQueue_rrd* queue_rrd) {
    return (queue_rrd->size_rrd == queue_rrd->capacity_rrd);
}

int isEmpty_rrd(struct CircularQueue_rrd* queue_rrd) {
    return (queue_rrd->size_rrd == 0);
}

void enqueueOrder_rrd(struct CircularQueue_rrd* queue_rrd, int orderID_rrd) {
    if (isFull_rrd(queue_rrd)) {
        printf("Queue is full! Cannot add more orders.\n");
        return;
    }
    
    if (isEmpty_rrd(queue_rrd)) {
        queue_rrd->front_rrd = queue_rrd->rear_rrd = 0;
    } else {
        queue_rrd->rear_rrd = (queue_rrd->rear_rrd + 1) % queue_rrd->capacity_rrd;
    }
    
    queue_rrd->orders_rrd[queue_rrd->rear_rrd] = orderID_rrd;
    queue_rrd->size_rrd++;
}

int dequeueOrder_rrd(struct CircularQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        printf("Queue is empty! No orders to serve.\n");
        return -1;
    }
    
    int orderID_rrd = queue_rrd->orders_rrd[queue_rrd->front_rrd];
    
    if (queue_rrd->size_rrd == 1) {
        queue_rrd->front_rrd = queue_rrd->rear_rrd = -1;
    } else {
        queue_rrd->front_rrd = (queue_rrd->front_rrd + 1) % queue_rrd->capacity_rrd;
    }
    
    queue_rrd->size_rrd--;
    return orderID_rrd;
}

void displayQueue_rrd(struct CircularQueue_rrd* queue_rrd) {
    if (isEmpty_rrd(queue_rrd)) {
        printf("No orders in queue.\n");
        return;
    }
    
    printf("Orders in queue (FCFS order):\n");
    printf("Position\tOrder ID\n");
    printf("------------------------\n");
    
    int index_rrd = queue_rrd->front_rrd;
    int position_rrd = 1;
    
    for (int i_rrd = 0; i_rrd < queue_rrd->size_rrd; i_rrd++) {
        printf("%d\t\t%d\n", position_rrd, queue_rrd->orders_rrd[index_rrd]);
        index_rrd = (index_rrd + 1) % queue_rrd->capacity_rrd;
        position_rrd++;
    }
    
    printf("------------------------\n");
}

int getQueueSize_rrd(struct CircularQueue_rrd* queue_rrd) {
    return queue_rrd->size_rrd;
}

int getAvailableSlots_rrd(struct CircularQueue_rrd* queue_rrd) {
    return queue_rrd->capacity_rrd - queue_rrd->size_rrd;
}

void displayMenu_rrd() {
    printf("\n===== Pizza Parlour Order System =====\n");
    printf("1. Place Order\n");
    printf("2. Serve Order\n");
    printf("3. Display Order Queue\n");
    printf("4. Show Queue Statistics\n");
    printf("5. Show Next Order\n");
    printf("6. Exit\n");
    printf("=====================================\n");
    printf("Enter your choice: ");
}
```

## Output

```
Welcome to Pizza Parlour Order System
====================================
Enter maximum number of orders the system can handle: 5
Pizza Parlour System Initialized with capacity for 5 orders

===== Pizza Parlour Order System =====
1. Place Order
2. Serve Order
3. Display Order Queue
4. Show Queue Statistics
5. Show Next Order
6. Exit
=====================================
Enter your choice: 1
Enter order ID: 101
Order 101 placed successfully!
Current orders in queue: 1
Available slots: 4

===== Pizza Parlour Order System =====
1. Place Order
2. Serve Order
3. Display Order Queue
4. Show Queue Statistics
5. Show Next Order
6. Exit
=====================================
Enter your choice: 1
Enter order ID: 102
Order 102 placed successfully!
Current orders in queue: 2
Available slots: 3

===== Pizza Parlour Order System =====
1. Place Order
2. Serve Order
3. Display Order Queue
4. Show Queue Statistics
5. Show Next Order
6. Exit
=====================================
Enter your choice: 1
Enter order ID: 103
Order 103 placed successfully!
Current orders in queue: 3
Available slots: 2

===== Pizza Parlour Order System =====
1. Place Order
2. Serve Order
3. Display Order Queue
4. Show Queue Statistics
5. Show Next Order
6. Exit
=====================================
Enter your choice: 3
Current order queue:
Orders in queue (FCFS order):
Position	Order ID
------------------------
1		101
2		102
3		103
------------------------

===== Pizza Parlour Order System =====
1. Place Order
2. Serve Order
3. Display Order Queue
4. Show Queue Statistics
5. Show Next Order
6. Exit
=====================================
Enter your choice: 2
Order 101 served successfully!
Remaining orders in queue: 2
Available slots: 3
```

## Dry Run

For a circular queue with capacity 5:

**Initial State**:
- front = -1, rear = -1, size = 0

**Place Order 101**:
- Queue is empty, so front = rear = 0
- orders[0] = 101
- size = 1

**Place Order 102**:
- rear = (0 + 1) % 5 = 1
- orders[1] = 102
- size = 2

**Place Order 103**:
- rear = (1 + 1) % 5 = 2
- orders[2] = 103
- size = 3

**Queue State**: [101, 102, 103, -, -] with front=0, rear=2

**Serve Order**:
- Return orders[front] = orders[0] = 101
- front = (0 + 1) % 5 = 1
- size = 2

**Queue State**: [ -, 102, 103, -, -] with front=1, rear=2

**Continue adding orders 104, 105**:
- Add 104: rear = 3, orders[3] = 104
- Add 105: rear = 4, orders[4] = 105
- Queue: [ -, 102, 103, 104, 105] with front=1, rear=4

**Add Order 106**:
- rear = (4 + 1) % 5 = 0
- orders[0] = 106
- Queue: [106, 102, 103, 104, 105] with front=1, rear=0
- Queue is now full since (rear + 1) % 5 = 1 = front

## Conclusion

The implementation demonstrates a pizza parlour order system using a circular queue data structure with the following key features:

**Circular Queue Operations**:
1. **Enqueue**: O(1) time complexity - add order to rear of queue
2. **Dequeue**: O(1) time complexity - remove order from front of queue
3. **Display**: O(n) time complexity - show all orders in queue
4. **Full/Empty Check**: O(1) time complexity

**Space Complexity**: O(n) where n is the capacity of the queue

**Key Implementation Features**:
1. **Fixed Capacity**: Maximum n orders as specified
2. **FCFS Scheduling**: Orders served in first-come, first-served order
3. **No Cancellation**: Once placed, orders cannot be cancelled
4. **Memory Efficient**: Uses array-based implementation
5. **Boundary Handling**: Proper circular wrap-around logic

**Advantages of Circular Queue**:
1. **Memory Utilization**: Fully utilizes array space
2. **Efficiency**: No shifting of elements required
3. **Simple Implementation**: Easy to understand and implement
4. **Performance**: Constant time insertion and deletion

**Circular Queue Conditions**:
1. **Empty**: front = rear = -1
2. **Full**: (rear + 1) % capacity = front
3. **Single Element**: front = rear (and queue is not empty)

**Real-world Applications**:
1. **Buffer Management**: CPU scheduling, disk scheduling
2. **Traffic Systems**: Traffic light control
3. **Resource Management**: Connection pooling in web servers
4. **Game Development**: Multiplayer game turn management

The implementation correctly handles all edge cases:
- Adding orders to empty queue
- Serving orders when queue becomes empty
- Circular wrap-around when rear reaches array end
- Preventing overflow and underflow conditions
- Proper queue state maintenance

This system ensures efficient order management in a pizza parlour by maintaining the first-come, first-served principle while maximizing memory utilization through the circular queue structure.