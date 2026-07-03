# DSA Last-Minute Pass Notes (24 Questions)

## 1. What is an Algorithm?
**Answer:** An algorithm is a step-by-step procedure used to solve a problem.

## 2. Characteristics of a Good Algorithm
- Correctness
- Finiteness
- Definiteness
- Efficiency
- Input and Output

## 3. What is an Array?
An array is a collection of elements of the same data type stored in continuous memory locations.

## 4. Why are arrays stored in continuous memory?
Because continuous memory allows fast access using indexes.

## 5. Array vs Linked List
- Array: Continuous memory, fixed size, fast access.
- Linked List: Non-continuous memory, dynamic size, easy insertion/deletion.

## 6. What is a Pointer?
A pointer is a variable that stores the memory address of another variable.

## 7. Relationship between Arrays and Pointers
The array name acts as a pointer to the first element.
- *arr = arr[0]
- *(arr+2) = arr[2]
- *(arr+4) = arr[4]

## 8. Output
```cpp
int arr[5]={10,20,30,40,60};
cout<<*arr;
cout<<*(arr+2);
cout<<*(arr+4);
```
Output:
```
10
30
60
```

## 9. What is a Structure?
A structure is a user-defined data type that stores different types of data under one name.

## 10. Array vs Structure
- Array: Same data type.
- Structure: Different data types.

## 11. Student Structure
```cpp
struct Student
{
    int rollNo;
    string name;
    float marks;
};
```

## 12. What is a Linked List?
A linked list is a linear data structure made of nodes. Each node stores data and the address of the next node.

## 13. Explain
```cpp
struct Node{
    int data;
    Node *next;
};
```
- data → stores value
- next → stores address of next node

## 14. Create 10->20->30->NULL
```cpp
Node *first=new Node();
Node *second=new Node();
Node *third=new Node();

first->data=10;
first->next=second;
second->data=20;
second->next=third;
third->data=30;
third->next=NULL;
```

## 15. What is Stack?
A stack is a linear data structure that follows LIFO (Last In First Out).

## 16. What is Queue?
A queue is a linear data structure that follows FIFO (First In First Out).

## 17. Stack vs Queue
- Stack → LIFO
- Queue → FIFO
- Stack: Push/Pop
- Queue: Enqueue/Dequeue

## 18. What is Recursion?
Recursion is when a function calls itself to solve a smaller version of the same problem.

## 19. What is a Base Condition?
The stopping condition of a recursive function. It prevents infinite recursion.

## 20. Recursive Factorial
```cpp
long factorial(long n)
{
    if(n==0)
        return 1;
    else
        return n*factorial(n-1);
}
```

## 21. Iterative Factorial
```cpp
long factorial(long n)
{
    long result=1;
    for(int i=1;i<=n;i++)
        result=result*i;
    return result;
}
```

## 22. Recursive Fibonacci
```cpp
long fibonacci(long n)
{
    if(n<=1)
        return n;
    else
        return fibonacci(n-1)+fibonacci(n-2);
}
```

## 23. Iterative Fibonacci
```cpp
int fibonacci(int n)
{
    int prev2=0, prev1=1, cur=0;
    if(n<=1)
        return n;
    for(int i=2;i<=n;i++)
    {
        cur=prev1+prev2;
        prev2=prev1;
        prev1=cur;
    }
    return cur;
}
```

## 24. Dry Run
factorial(4)
```
4×3×2×1=24
```

# Must Remember
- 0! = 1
- Fibonacci: 0 1 1 2 3 5 8
- *arr = arr[0]
- *(arr+2)=arr[2]
- LIFO = Stack
- FIFO = Queue
- Recursion = Function calls itself
- Base condition = Stops recursion
