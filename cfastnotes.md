# C Programming Notes Version 2

## Table of contents

* Important points (statements, identifiers, keywords)
* Data types
* Variables and constants
* Operators and expressions
* Type conversion
* Control Statements
* Functions
* Pointers

## Important points

* What is a keyword and an identifier? Every word in a C program is either an identifier or a keyword. Identifiers are the names given to program elements such as variables and functions. Keywords are reserved words which cannot be used as identifiers.

* What is a statement?

* What is an expression?

* What is the difference between initialization and declaration?

* What is an operator?

* What are the macros? 

## First program template

```c
#include <stdio.h>

int main( int argc, char *argv[] ) {
    return 0;
}
```

## Data types

C provides four basic data types: char , int , float , and double. Their size depends on the compiler. 

```c
/* To check the actual size on the compiler use: */

printf("%d", sizeof(type));

/* Declaring and initializing data types */

char letter = 'a'; /* usually 1 byte */
int integer = 9; /* usually 2 bytes */
float fl_point = 7.14; /* usually 4 bytes */
double big_number = 231234512353421434; /* usually 8 bytes */
```

## Operators

C supports different types of operators which can be classified into following categories: arithmetic, relational, equality, logical, unary, conditional, bitwise, assignment, comma, and `sizeof()` operators.

Like arithmetic expressions, logical expressions are evaluated from left to right.

Both x++ and ++x increment the value of x, but in the former case, the value of x is returned before it
is incremented. Whereas in the latter case, the value of x is returned after it is incremented. 

## Type conversion

While type conversion is done implicitly, typecasting has to be done explicitly by the programmer. Typecasting is done when the value of one data type has to be converted into the value of another data type. It is usual for pointers.

```c
struct node {
    int x;
};

struct node *l_list = NULL;
l_list = (struct node*)malloc(sizeof(struct node)); /* Type casting */
```

## Control statements

C supports three types of control statements: decision control statements, iterative statements, and jump statements.

The break statement is used to terminate the execution of the nearest enclosing loop in which it
appears.

When the compiler encounters a continue statement, then the rest of the statements in the loop are skipped and the control is unconditionally transferred to the loop-continuation portion of the nearest enclosing loop.

```c
/* For loop syntax: 
for ( init_clause ; cond_expression ; iteration_expression ) loop_statement	*/

for(i = 0; i < 10; i++)
{
    printf("For loop!\n");
}
```

* An `init_clause`, which is an expression, is evaluated once, before the first evaluation of `cond_expression` and its result is discarded.
* `cond_expression` is evaluated before the loop body. If the result of the expression is zero, the loop statement is exited immediately.
* `iteration_expression` is evaluated after the loop body and its result is discarded. After evaluating `iteration_expression`, control is transferred to `cond_expression`.

> *init_clause*, *cond_expression*, and *iteration_expression* are all optional. If *cond_expression* is omitted, it is replaced with a non-zero integer constant, which makes the loop endless:

## Functions

Function declaration statement identifies a function’s name and the list of arguments that it accepts and
the type of data it returns.

Function definition, on the other hand, consists of a function header that identifies the function, followed
by the body of the function containing the executable code for that function. When a function is defined,
space is allocated for that function in the memory. 

A function having void as its return type cannot return any value. Similarly, a function having void as its parameter list cannot accept any value.

Call by value method passes values of the variables to the called function. Therefore, the called function uses a copy of the actual arguments to perform its intended task. This method is used when the function does not need to modify the values of the original variables in the calling function. 

In call by reference method, addresses of the variables are passed by the calling function to the called function. Hence, in this method, a function receives an implicit reference to the argument, rather than a copy of its value. This allows the function to modify the value of the variable and that change is reflected in the calling function as well.

```c
/* Arguments sometimes use the const keyword to evade you to change them */

pair *twos_difference(size_t n, const int array[n], size_t *z) {
  
}
```

##  Pointers

A pointer is a variable that contains the memory address of another variable.

The & operator retrieves the address of the variable.

We can ‘dereference’ a pointer, i.e., refer to the value of the variable to which it points by using unary * operator.

Null pointer is a special pointer variable that does not point to any variable. This means that a null pointer does not point to any valid memory address. To declare a null pointer we may use the predefined constant NULL.
A generic pointer is pointer variable that has void as its data type. The generic pointer can point to variables of any data type. 

To declare pointer to pointers, we need to add an asterisk (*) for each level of reference.

### Function pointers

**Function pointers**, point to executable code for a function in memory.

Function pointers can be stored in an array or passed as arguments to other functions.

```c
/* Syntax */
return_type (*func_name)(parameters) 
    
#include <stdio.h>
void say_hello(int num_times); /* function */

int main() {
  void (*funptr)(int);  /* function pointer */
  funptr = say_hello;  /* pointer assignment */
  funptr(3);  /* function call */
    
  return 0;
}

void say_hello(int num_times) {
  int k;
  for (k = 0; k < num_times; k++)
    printf("Hello\n");
}

/* An array of function pointers can replace a switch or an if statement for choosing an action, as in the following program: */

#include <stdio.h>

int add(int num1, int num2);
int subtract(int num1, int num2);
int multiply(int num1, int num2);
int divide(int num1, int num2);

int main() 
{
  int x, y, choice, result;
  int (*op[4])(int, int);

  op[0] = add;
  op[1] = subtract;
  op[2] = multiply;
  op[3] = divide;
  printf("Enter two integers: ");
  scanf("%d%d", &x, &y);
  printf("Enter 0 to add, 1 to subtract, 2 to multiply, or 3 to divide: ");
  scanf("%d", &choice);
  result = op[choice](x, y);
  printf("%d", result);
    
  return 0;
}

int add(int x, int y) {
  return(x + y);
}

int subtract(int x, int y) {
  return(x - y);
}

int multiply(int x, int y) {
  return(x * y);
}

int divide(int x, int y) {
  if (y != 0)
    return (x / y);
  else
    return 0;
}


```

## Arrays

Arrays are initialized by writing, `type array_name[size] = {list of values};`

The un-assigned elements are filled with zeros, `int marks [5] = {0};`

For inter-function communications you can pass individual elements of the array, data values, or adresses.

```c
int main()
{
  int arr[5] ={1, 2, 3, 4, 5};
  func(&arr[3]);
  func2(arr);
}
void func(int *num) 
{
  printf("%d , *num);
}
void func2(int arr[5]) //A function that accepts an array can declare the formal parameter in either of the two following ways. `func(int arr[]);` or `func(int *arr);`
{
    int i;
    for(i= ;i<5;i++)
        printf("%d", arr[i]);    
}
```

In C the array name refers to the first byte of the array in the memory.

When we pass the name of an array to a function, the address of the zeroth element of the array is copied to the local pointer variable in the function. An array name is often known to be a constant pointer.

> In case of one-dimensional arrays, we have discussed that if the array is completely initialized, we may omit the size of the array. The same concept can be applied to a two-dimensional array, except that only the size of the first dimension can be omitted.

### Passing 2D arrays to functions

* Passing individual elements

* Passing a row

```c
main()
{
int arr[2][3] = ({1, 2, 3}, {4, 5, 6});
        func(arr[1]);
}
void func(int arr[])
{
    int i;
    for(i= ;i<3;i++)
    printf("%d", arr[i] * 1 );
}
```

* Passing the entire 2D array

To pass a two-dimensional array to a function, we use the array name as the actual parameter (the way we did in case of a 1D array). However, the parameter in the called function must indicate that the array has two dimensions.

### Pointers and 2D arrays

```c
int mat[5][5];
int **ptr;

//Access
mat[i][j] or
*(*(mat + i) + j) or
*(mat[i]+j);
```

Here int **ptr is an array of pointers (to one-dimensional arrays), while int mat[5][5] is a 2D array. They are not the same type and are not interchangeable.

```c
#include <stdio.h>
int main()
{
    int arr[2][2]={{1,2}, {3,4}};
    int i, (*parr)[2];
    parr = arr;
    for(i = 0; i < 2; i++)
    {
    for(j = 0; j < 2 ;j++)
        printf(" %d", (*(parr+i))[j]); //arr[i][j] = (*(arr+i))[j] = 
                                                        //*((*arr+i))+j)
    }
    return 0;
}
//Output 1 2 3 4
```

> If we declare an array of pointers using, `data_type *array_name[SIZE];` Here SIZE represents the number of rows and the space for columns that can be dynamically allocated.
>
> If we declare a pointer to an array using, data_type `(*array_name)[SIZE];`
> Here SIZE represents the number of columns and the space for rows that may be dynamically allocated.

A double pointer cannot be used as a 2D array. Therefore, it is wrong to declare: ‘int **mat’ and then use ‘mat’ as a 2D array. These are two very different data types used to access different locations in memory. So running such a code may abort the program with a ‘memory access violation’ error.

### Pointers to structures

```c
struct example {
    int x; 
}

struct example one;

/* Accessing without pointer */

one.x = 4;
printf("%d", one.x);

/* Accessing the structure through pointer */

struct example *ptr;
ptr = &one;

ptr->x = 2;
printf("%d", ptr->x);
```

## Strings

A set of characters together, in an array.

```c
char myString [4] = {'H','e','l','l','o'};
```

## Structures and unions

A **structure** is a **user-defined data type** that groups related variables of different data types.

A structure **declaration** includes the keyword **struct**, a **structure tag** for referencing the structure, and curly braces { } with a list of variable declarations called **members**.

A struct variable is stored in a contiguous block of memory. The **sizeof** operator must be used to get the number of bytes needed for a struct, just as with the basic data types.

Structs can contain other structs.

```c
struct course {  
  int id;
  char title[40];
  float hours; 
}; 

/* declare two variables */
struct student s1;
struct student s2; 

/* initializing */
struct student s1 = {19, 9, "John"};

/* If you want to initialize a structure using curly braces after declaration, you will also need to type cast, as in the statements: */

s1 = (struct student) {19, 9, "John"};

/* You can use named member initialization when initializing a structure to initialize corresponding members: */

struct student s1 = { .grade = 9, .age = 19, .name = "John"}; 
```

## Memory management

malloc and calloc function description

## Files & error handling

## The preprocessor

## Extra topics

### Enum

`enum` , is a set of integer constants represented by identifiers. Enumeration constants help make programs more readable and easier to maintain.

Use only uppercase letters in the names of enumeration constants to make these constants stand out in a program and to indicate that enumeration constants are not variables.

### Storage classes

storage class specifiers auto , register , extern and static .

### The standard library 

https://www.tutorialspoint.com/c_standard_library/index.htm

### Branch-less programming 

It's meaningful to say that branch-less programming uses mathematics and also...

* Uses **boolean operators**

* Uses **multiplication and addition**

  ```c
  int is_bigger(int x, int y) {
      return x * (x > y) + y * (y > x);
  }
  ```

Its equivalent with branches will be:

```c
/* This way*/

int is_bigger(int x, int y) {
    if(x > y)
        return x;
    else if(y > x)
        return y;
}

/*Or this way*/

int is_bigger(int x, int y) {
	return (x > y) ?  x : y; //This operator ?: is really useful
}
```

### Coding style

https://www.kernel.org/doc/html/latest/process/coding-style.html

https://developer.gnome.org/programming-guidelines/stable/c-coding-style.html.en

* Don't use typedefs for structures and pointers because you can't tell what type of data it is.
* Functions should be short and sweet, and do just one thing. They should fit on one or two screenfuls of text (the ISO/ANSI screen size is 80x24, as we all know), and do one thing and do that well.

### Useful references

## Algorithms

The linear search algoritm (p. 241) works well for small or unsorted arrays. For sorted arrays, the high-speed binary search algorithm can be used.

The binary search algorithm (p. 241) eliminates from consideration one-half of the elements in a sorted array after each comparison. The algorithm locates the middle element of the array and compares it to the search key. If they’re equal, the search key is found and the array index of that element is returned. If they’re not equal, the problem is reduced to searching one-half of the array. If the search key is less than the middle element of the array, the first half of the array is searched, otherwise the second half is searched. If the search key is not found in the specified subarray (piece of the original array), the algorithm is repeated on one-quarter of the original array. The search continues until the search key is equal to the middle element of a subarray, or until the subarray consists of one element that’s not equal to the search key (i.e., the search key is not found).

When using a binary search, the maximum number of comparisons required for any array can
be determined by finding the first power of 2 greater than the number of array elements.

## Data structures

### Linked lists

To create a linked list we need three pointers:

1) new_node - this pointer uses malloc() to create nodes

2) start - this pointer points to the start of the linked list

3) ptr - joins the node->next to the next node
