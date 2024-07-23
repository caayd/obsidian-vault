

## Declaring Pointer Variables

There is no name associated with pointer data types, <u>pointer variables store memory addresses.</u>

The value of a pointer variable is an address or memory space that typically contains some data.

When you declare a pointer variable, you also specify the data type of the value to be stored in the memory location pointed to by the pointer variable. (ie. int, string, char, etc.)


You declare a pointer variable using the asterisk symbol (`*`) between the data type and the variable name. The general syntax is:

	dataType *identifier;

For example, consider:

	int *p;
	char *ch;

both `p` and `ch` are pointer variables. `p` is type `int` and `ch` is type `char`.

The asterisk can appear anywhere between the data type name and the variable name:

	int *p;
	int * p;
	int* p;

all lines are valid.


in the statement:

	int* p, q;

only p is the pointer, which is why you usually attach the asterisk to the variable name.

for both variables to be pointer variables you would write:

	int *p, *q;


## Address of Operator (&)
---

The ampersand (&) is called that <u>address of operator</u>. It is an unary operator that returns the address of its operand.

For example in the statement:

	int x;
	int *p;
	
	p = &x

assigns the address of `x` to `p`. x and the value of p refer to the same memory location.

Another example, in the statement:

	int num1, num2;
	int *numPtr;
	
	num = 100;
	
	num2 = num1; // sets value of num2 to 100
	
	numPtr = &num1;

rather than set the value of `numPtr` to 100, the last line simply asks the program to copy the address of the memory location of `num1` to `numPtr`, not the integer value its holding.

So in the statement:

	cout << num1 << endl;
	cout << numPtr << endl;

the first line will output 100 onto the screen, while the second line will output an address usually displayed in hexadecimal digits.

## Dereferencing Operator (`*`)

When used as a unary operator, `*`, commonly referred to as the <u>dereferencing operator</u> or the <u>indirection operator</u>, refers to the object to which its operand points.

For example in the statement:

	num = 78;
	
	p = &num;
	
	*p = 24;


The statement `num` = 78; stores 78 into `num`.

The statement `p = &num;` stores the address of `num`, which is 1800, into `p`.

The statement `*p = 24;` stores 24 into the memory location to which `p` points. Because the value of `p` is 1800, statement 3 stores 24 into memory location 1800. Note that the value of `num` is also changed.


## Classes, Structs, and Pointer Variables
---

assume a struct `studentType`:

	studentType student;
	studentType* studentPtr;
	
	studentPtr = &student;
	(*studentPtr).gpa = 3.9;

the parenthesis are required around `(*studentPtr).gpa` because the dot (.) has a higher precedence than the asterisk, so it would be skipped over without it.

because of this, C++ has another operator called the <u>member access operator arrow</u> (->). consisting of a hyphen and a greater than sign.

The syntax for accessing a `class` (`struct`) member using the operator -> is:

`pointervariableName->classMemberName`

so the statement:

`(*studentPtr).gpa = 3.9;`

is equivalent to:

`studentPtr->gpa = 3.9;`

eliminating the use of parenthesis and the asterisk for the dereferencing operator.

## Initializing Pointer Variables
---

Because C++ does not automatically initialize variables, pointer variables must be initialized if you do not want them to point to anything.

Pointer variables are initialized using the constant value 0, called the <u>null pointer.</u>

Some programmers use the named constant NULL to initialize pointer variables. The named constant `NULL` is defined in the header file `cstddef`. The following two statements are equivalent:

	p = NULL;
	p = 0;

## Initializing Pointer Variables Using `nullptr`
---

C++11 Standard provides the null pointer `nullptr` to initialize pointer variables.

A pointer with the value `nullptr` points to nothing, and is called the null pointer.

The following statement declares p to be a pointer of type int and it also initializes it to the null pointer:

	int *p = nullptr;

Standard, we can initialize the pointer variable using the `int` value 0, using another pointer variable of the same type, or using `nullptr`. In C++, `nullptr` is a reserved word.

## Dynamic Variables
---

Variables that are created during program execution are called <u>dynamic variables</u>.

C++ provides two operators, `new` and `delete`, to create and destroy dynamic variables, respectively. 

When a program requires a new variable, the operator `new` is used. 

When a program no longer needs a dynamic variable, the operator `delete` is used.

## Operator `new`

The operator `new` has two forms: one to allocate a single variable and another to allocate an array of variables

The syntax to use the operator `new` is:

	new dataType; // to allocate a single variable
	new dataType[intExp]; // to allocate an array of variables

The operator `new` allocates memory (as a variable) of the designated type and returns a pointer to it.

consider:

	int *p;
	chat *q;
	int x;

the statement:

	p = &x;

stores the address of x in p. However, no new memory is allocated. On the other hand, consider the following statement:

	p = new int;

This statement creates a variable during program execution somewhere in memory and stores the address of the allocated memory in `p`.

Because a dynamic variable is unnamed, it cannot be accessed directly. It is accessed indirectly by the pointer returned by `new`.

## Operator `delete`
---

Suppose:

	p = new int;
	*p = 54;
	p = new int;
	*p = 73;

![[Pasted image 20240508055159.png|550]]

After execution of the statement in Line 3, p points to the new memory space at location 1800. The previous memory space at location 1500 is now inaccessible. In addition, the memory space 1500 remains as marked allocated. It cannot be freed or reallocated.

This is called <u>memory leak</u>, there is an unused memory space that cannot be allocated.

When a dynamic variable is no longer needed, it can be destroyed; that is, its memory can be deallocated. The `delete` operator is used for this.

The syntax to use the operator `delete` has two forms:

	delete pointerVariable; // to deallocate a single dynamic variable
	
	delete [] pointerVariable; // to deallocate a dynamically created array

## Operations on Pointer Variables
---

Suppose:

	int *p, *q;

The statement:

	p = q;


copies the value of q into p. After this statement executes, both p and q point to the same memory location. Any changes made to `*p `automatically change the value of `*q`, and vice versa.

	int *p;
	double *q;
	char *chPtr;
	studentType *stdPtr;

the size of the memory allocated for an `int` variable is 4 bytes, a `double` variable is 8 bytes, and a `char` variable is 1 byte.

the statement:

`p++;` or `p = p + 1;` 

increments the value of p by 4 bytes because p is a pointer of type int. Similarly, the statements

`q++;` and `chPtr++;`

increment the value of `q` by 8 bytes and the value of `chPtr` by 1 byte, respectively.

The statement `stdPtr++;` increments the value of `stdPtr` by 40 bytes.

