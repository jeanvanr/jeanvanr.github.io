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

