
## Intro
---

Using classes, you can combine data and operations in a single unit. Making objects their own self-contained entity.

You can also create classes from existing classes, encouraging code reuse. 

Two common ways to relate classes in a meaningful way are:

- <u>Inheritance</u> ("is-a" relationship)
- <u>Composition (aggregation)</u> ("has-a" relationship)

# Inheritance
---

Inheritance lets you create new classes from existing classes. The new classes created from these existing classes are called the <u>derived classes</u> and the pre-existing classes are called the <u>base classes</u>.

<u>derived classes</u> inherit the properties of the base classes so you don't have to make completely new classes from scratch.

Each derived class can become a base class for a future derived class:
- <u>single inheritance</u> - the derived class is derived from a <u>single</u> base class.
- <u>multiple inheritance</u> - the derived class is derived from <u>more than one</u> base class.


The general syntax of a derived class is:

	class className: memberAccessSpecifier baseClassName {
		member list
	};

in which `memberAccessSpecifier` is `public`, `protected`, or `private` (if not specified `private` will be assumed).


Example:

![[Pasted image 20240412204422.png]]

The following statements specify that `class circle` is derived from `shape`, and is `public` inheritance:

	class circle: public shape {
		.
		.
	};

If this statement was `private` inheritance:

	class circle: private shape {
		.
		.
	};

The public members of `shape` become `private` members of the `class circle`, so any object of type `circle` cannot directly access the members. This statement is also equivalent to:

	class circle: shape {
		.
		.
	};

since it is assumed to be private.


Things to keep in mind about base and derived classes.

1. `private` members of a base class remain `private` to the base class, meaning members of the derived class cannot directly access them.

2. `public` members of a base class can be inherited either as `public` members or as `private` members by the derived class. Members of a base class can either remain `public` or become `private` in the derived class.

3. The derived class can include additional members, data, and functions.

4. The derived class can redefine the `public` member functions of the base class, meaning you can have a member function with the same name, number, and types of parameters as a function in the base class, but with different code in the function body.

5. All member variables of the base class are also member variables of the derived class. Similarly, the member functions of the base class (unless redefined) are also member functions of the derived class.

### Redefining (Overriding) Member Functions of the Base Class
---

To redefine a `public` member function of a base class in the derived class, the corresponding function in the derived class must have the same name, number, and types of parameters.

When writing the definitions of the member functions of a derived class to specify a call to a `public` member function of the base class, we do the following:

- If the derived class overrides a `public` member function of the base class, then to specify a call to that `public` member function of the base class, you use the name of the base class, followed by the scope resolution operator (::), followed by the function name with the appropriate parameter list.
  
  For example to call the function `area` of the `class rectangleType` the statement is: `rectangleType::area()`.

- If the derived class does <u>not</u> override a `public` member function of the base class, you *may* specify a call to that `public` member function by using the name of the function and the appropriate parameter list.


Assume `boxType` is a derived class of the base class `rectangleType`, `rectangleType` has member variables `length` and `width`, and `boxType` includes the member variable `height`. To define the member function `print` for `boxType` you need to keep in mind:

- The member variables `length` and `width` are `private` members of the `class rectangleType`, so they cannot be directly accessed by `class boxType`.

- The member variables `length` and `width` of the `class rectangleType` are accessible by the `class boxType` only through the `public` member functions of the `class rectangleType`. So you would have to call the member function `print` of the `class rectangleType` to print the values of `length` and `width` and then output the value of `height` after the fact since it is a member of `class boxType`.

The definition of the member function `print` of the `class boxType` is:

	void boxType::print() const {
		rectangleType::print();
		cout << "Height = " << height;
	}

### Constructors of Derived and Base Classes
---

A derived class can have its own `private` member variables, so a derived class can explicitly include its own constructors to initialize them.

Constructors of a derived class can (directly) initialize only the (`public` data) members inherited from the base class of the derived class. So when a derived class object is declared <u>it must also trigger the execution of one of the base class's constructors</u>.

The triggering of the base class's constructor is *specified in the heading of the definition of a derived class constructor*.


The default constructor of derived `class boxType` would be defined as:

	boxType::boxType() {
		height = 0.0;
	}

assuming `class rectangleType` has its own default constructor.


When writing a definition of a constructor with parameters you write the constructor heading including all parameters needed for both the base class and derived constructors, then trigger the execution of the base class constructor with parameters using a colon (:) followed by the name of the constructor of the base class.

	boxType::boxType(double l, double w, double h): rectangleType(l, w) {
		if (h>=0)
			height = h;
		else
			height = 0;
	}

The statement:

	rectangleType myRectangle(5.0, 3.0);
	boxType myBox(6.0, 5.0, 4.0);

looks like:

![[Pasted image 20240412212945.png]]

More information bottom of 11-1b

### Header File of a Derived Class
---

in a derived class you must include the base class at the beginning of the derived class's header file. For example, before the definition of the derived `class partTimeEmployee` you would want to include the header file for base `class personType`:

	#inlcude "personType.h"
	
	class partTimeEmployee: public personType {
		.
		.
	}

### Multiple Inclusions of a Header File
---

Consider the header file `test.h`:

	//Header file test.h
	
	const int ONE = 1;
	const int TWO = 2;

Suppose that the header file `testA.h` includes the file `test.h` to use identifiers `ONE` and `TWO`:

	//Header file testA.h
	
	#include "test.h"
	.
	.

Now consider the program code:

	//Program headerTest.cpp
	
	#include "test.h"
	#include "testA.h"
	.
	.

When this code is compiled is first processed by the preprocessor. The preprocessor first includes the header file `test.h` and then the header file `testA.h`. When `testA.h` is included, the header file `test.h` is included twice because of the line `#include "test.h"` found in the header file `testA.h`, resulting in compile-time errors.

 To fix this issue you use preprocessor commands in the header file:

	#ifndef H_test
	#define H_test
	const int ONE = 1;
	const int TWO = 2;
	#endif

a. `#ifndef H_test` means "if not defined H_test"

b. `#define H_test` means "define H_test"

c. `#endif` means "end if"

Meaning, if the identifier `H_test` is not defined we must define it and let the remaining statements between `#define` and `#endif` pass. If `test.h` is included the second time, `#ifndef` fails and all statements until `#endif` are skipped.

example in 11-1d

### Protected Members of a Class
---

Sometimes it is necessary or a derived class to directly access a `private` member of a base class. If you make a `private` member become `public`, anyone can access that member. 

A derived class can directly access the `protected` members of a base class. So for a base class to give access to a member to its derived class and still prevent its direct access outside of the class, you must declare that member under `memberAccessSpecifier protected`.

If a member of a base class needs to be accessed by a derived class, that member is declared under `memberAccessSpecifier protected`.

### Inheritance as public, protected, or private
---

Consider the statement:

	class B: memberAccessSpecifier A {
		.
		.
	};

`memberAccessSpecifier` is either `public`, `protected`, or `private`.

1. If `memberAccessSpecifier` is `public`
	- The `public` members of `A` are `public` members of `B`. They can be directly accessed in `class B`.
	- The `protected` members of `A` are `protected` members of `B`. They can be directly accessed by the member functions (and `friend` functions) of `B`.
	- The `private` members of `A` are hidden in `B`. They cannot be directly accessed in `B`. They can be accessed by the member functions (and `friend` functions) of `B`.

2. If `memberAccessSpecifier` is `protected`
	- The `public` members of `A` are `protected` members of `B`. They can be accessed by the member functions (and `friend` functions) of `B`.
	-  The `protected` members of `A` are `protected` members of `B`. They can be accessed by the member functions (and `friend` functions) of `B`.
	-  The `private` members of `A` are hidden in `B`. They cannot be directly accessed in `B`. They can be accessed by the member functions (and `friend` functions) of `B`.

3. If `memberAccessSpecifier` is `private`
	- The `public` members of `A` are `private` members of `B`. They can be accessed by the member functions (and `friend` functions) `B`.
	-  The `protected` members of `A` are `private` members of `B`. They can be accessed by the member functions (and `friend` functions) of `B`.
	-  The `private` members of `A` are hidden in `B`. They cannot be directly accessed in `B`. They can be accessed by the member functions (and `friend` functions) of `B`.

example of use case of `protected` in 11-1g.

# Composition (Aggregation)
---

Composition (aggregation) is another way to relate two classes. In composition, one or more members of a class are objects of another classes type.

In the case of inheritance, use the class name to invoke the base class’s constructor. In the case of composition, use the member object name to invoke its own constructor.

example in 11-2

# Object-Oriented Design (OOD) and Object-Oriented Programming (OOP)
---

The three basic principles of Object- Oriented Design (OOD) are as follows:
- <u>Encapsulation</u> - The ability to combine data and operations on that data in a single unit.
- <u>Inheritance</u> - The ability to create new objects (classes) from existing objects (classes).
- <u>Polymorphism</u> - The ability to use the same expression to denote different operations.

In OOD, a class is a fundamental entity; in structured programming, a function is a fundamental entity.

OOD encourages code reuse, once a class becomes error-free, it can be reused in many programs because it is a self-contained entity.

### Identifying Classes, Objects, and Operations
---

The hardest part in OOD is to identify the classes and objects.

We begin with a description of the problem and then identify all of the nouns and verbs. We choose our<u> classes from the list of nouns</u>, and we choose our <u>operations from the list of verbs</u>.

Suppose that we want to write a program that calculate and prints the volume and surface area of a cylinder. We can state this problem as follows:

_Write_ a **program** to _input_ the **dimensions** of a **cylinder** and _calculate_ and _print_ the **surface area** and **volume**.

In this statement, the nouns are bold, and the verbs are italic.

nouns: **program, dimensions, cylinder, surface area,** and **volume**.

cylinder can be visualized as a class, for example, `cylinderType`, from which you can create cylinder objects of various dimensions.

After we identify a class, the next step is to determine three pieces of information:
- Operations than an object of that class type can perform.
- Operations that can be performed on an object of that class type.
- Information that an object of that class type must maintain.

for the `class cylcinderType`, the dimensions represent the data. The `center` of the base, `radius` of the base, and the `height` of the cylinder are all characteristics of the dimensions.

Identifying classes via the nouns and verbs from the descriptions of the problem is not the only technique possible.

Large example on 11-3a