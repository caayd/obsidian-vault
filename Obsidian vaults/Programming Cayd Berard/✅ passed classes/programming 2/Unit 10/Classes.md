
The general syntax for defining a class is:

	class classIdentifier {
		classMembersList
	};

in which `classMembersList` consists of variable declarations and/or functions. A member of a class can be a variable (to store data) or a function (to manipulate data).

Example:

	class courseType {
		public:
			void setCourseINfo(string cName, string cNo, int credits):
			void print() const;
			int getCredits()
			string getCourseNumber();
			string getCourseName();
		private:
			string courseName;
			string courseNo;
			int courseCredits;
	};

Things to note:

- If a member of a class is a variable, you declare it like any other variable. You cannot initialize a variable in the definition of a class.
- If a member of a class is a function, you usually use the function prototype to declare that member.
- If a member of a class is a function, it can (directly) access any member of the class (variables and functions).
- The semicolon at the end of the rights brace is needed and will produce a syntax error if missing.

---
### Categories of classes

There are 3 categories for the members of a `class`:
- `private`
- `public`
- `protected`

these categories are called <u>member access specifiers</u>.

- by default, all members of a class are `private`.
- If a member of a class is `private`, you cannot access it outside of the class.
- A `public` member is accessible outside of the `class`.
- To make a member `public`, you use the member access specifier `public` with a colon, ":".

`private` and `public` members can appear in any order (section 10-1k).

---

# Clock Example

The code:

	class clockType {
		pulbic:
			void setTime(int, int, int);
			void getTime(int&, int&, int&) const;
			void printTime() const;
			void incrementSeconds();
			void incrementMinutes();
			void incrementHours();
			bool equalTime(const clockType&) const;
			
		private:
			int hr;
			int min;
			int sec;
	}

- The class `clockType` has seven member functions: `setTime`, `getTime`, `printTime`, `incrementSeconds`, `incrementMinutes`, `incrementHours`, and `equalTime`. It has three member variables: `hr`, `min`, and `sec`.

- The variables `hr`, `min`, and `sec` are `private` to the class and cannot be accessed outside of the class.

- The seven member functions are `public` and can be accessed outside of the class, they also have access to the private member variables within the class.

- In the function `equalTime` the formal parameter is a constant reference parameter. In a call to the function `equalTime`, the formal parameter receives that address of the actual parameter, but the formal parameter cannot modify the value of the actual parameter.

- The word `const` at the end of the member functions `getTime`, `printTime`,  and`equalTime` specifies that these functions cannot modify the member variables of type `clockType`.

---

## Unified Modeling Language Class Diagrams

A class and its members can be described graphically using a notation known as the <u>Unified Modeling Language (UML)</u> notation.

UML class diagram of `clockType` from previous section:

![[Pasted image 20240329233417.png|350]]

The top box contains the name of the class. The middle box contains the member variables and their data types. The last box contains the member function name, parameter list, and the return type of the function.
- A plus sign (+) in front of a member name indicates that the member is a `public` member
- A minus sign (-) indicates that the member is a `private` member.
- The pound symbol (#) indicates that the member is a `protected` member.

---

## Variable (Object) Declaration

Once a class is defined, you can declare variables of that type. In C++ terminology, a class variable is called a <u>class object</u> or a <u>class instance</u>.

The syntax for declaring a class object is the same as that for declaring any other variable. The following declares two objects of type `clockType`:

	clockType myClock;
	clockType yourClock;

both objects contain [[#Clock Example|10 members]], seven member functions and three member variables. Each function has separate memory allocated for `hr`, `min`, and `sec`.

The C++ compiler only generates one physical copy of a member function of a class, and each class object executes the same copy of the member function. Therefor when we draw the figure of a class object, we only show the member variables:

![[Pasted image 20240329234533.png]]

---

## Accessing Class Members

Once and object of a class is declared, it can access the members of the class. The general syntax for an object to access a member of a class is: 

	classObjectName.memberName

The class members that a class object can access depend on where the object is declared.
- If the object is declared in the definition of a member function of the class, then the object can access both the `public` and `private` members.
- If the object is declared elsewhere, then the object can access only the `public` members of the class.

recall that the dot (.) is an operator called the [[structs#Accessing `struct` Members|member access operator]].

Example:

suppose you have the following declaration:

	clockType myClock;
	clockType yourClock;

Consider the following:

	myClock.setTime(5, 2, 30);
	myClock.printTime();
	yourClock.setTime(x, y, z) // assume x,y,z are variables of type int
	
	if(my.Clock.equalTime(yourClock))
	.
	.

These statements are legal.

The first statement `myClock.setTime(5, 2, 30);` executes member function `setTime` and the values of 5, 2 , and 30 are passed as parameters to the function `setTime`. The function uses these values to set the values of the three member variables `hr`, `min`, and `sec` of `myClock` to 5, 2, and 30 respectively. 

The fourth statement executes the member function `equalTime` and compares the three member variables of `myClock` to the corresponding member variables of `yourClock`. 

The objects `myClock` and `yourClock` can access only `public` members of the `class clockType`. So any statements where these objects try to access the `private` members of the class are illegal:

	myClock.hr = 10;            // illegal
	myClock.min = yourClock.min // illegal

---

## Built-in Operation on Classes

Most of C++'s built-in operations do not apply to classes.
- You cannot use arithmetic operators to perform arithmetic operations on class objects.
- You cannot use relator operators to compare two class objects for equality. (~~unless they're overloaded~~)

The two build in operations that are valid for class objects are member access (.) and assignment (=).

#### <u>Assignment Operator and Classes</u>

Suppose that `myClock` and `yourClock` are `clockType` objects, as defined previously:

![[Pasted image 20240330000934.png]]

The statement `myClock = yourClock;` copies the value of `yourClock` into `myClock`.
- the three member variables of `yourClock` are copied into the corresponding three member variables of `myClock`.

An assignment statement performs a <u>member-wise copy</u>.

---

## Class Scope

A `class` object can be:
- <u>automatic</u> - created each time the control reaches its declaration and destroyed when the control exits the surrounding block.
- <u>static</u> - created once, when the control reaches its declaration, and destroyed when the program terminates.

You can declare an array of `class` objects.

A `class` object has the same scope as other variables. A `class` object has the same scope as a member of a `struct`. That is, a member of a `class` is local to the `class`.

---

## Functions and Classes

The following rules describe the relationship between functions and classes:
- `class` objects can be passed as parameters to functions and returned as function values.
- As parameters to functions, `class` objects can be passed either by value or by reference.
- If a `class` object is passed by value, the contents of the member variables of the actual parameter are copied into the corresponding member variables of the formal parameter.

---

## Reference Parameters and Class Objects (Variables)

If a variable is passed by reference, the formal parameter receives only the address of the actual parameter. Therefore, an efficient way to pass a variable as a parameter is by reference.

If a variable is passed by reference, then when the formal parameter changes, the actual parameter also changes. Sometime however you do not want the function to be able to change the values of the member variables.

In C++, you can pass a variable by reference and still prevent the function from changing its value by using the keyword `const` in the formal parameter declaration. consider:

	void testTime(const clockType& otherClock) {
		clockType dClock;
		.
		.
	}

The function `testTime` contains a reference parameter, `otherClock` which is declared using the keyword `const`. 
In a call to the function `testTime`, the formal parameter `otherClock` receives the address of the actual parameter, but `otherClock` cannot modify the contents of the actual parameter. 

For example, after the following statement executes, the value of `myClock` will not be altered:

	testTime(myClock);

Generally if you want to declare a class object as a value parameter, you declare it as a reference parameter using the keyword `const`.

If a formal parameter is a value parameter within the function definition you can change the value of the formal parameter. However, if a formal parameter is a constant reference parameter, you cannot use an assign statement to change its value within the function, nor can you use any other function to change its value.

---

## Implementation of Member Functions

[[#Clock Example|In the definition of]] `class clockType`, we only included the function prototype for the member functions.

If you were to put the defections of the functions inside the class itself but that makes a mess inside the class.

Since the identifiers `setTime`, `printTime`, and so on are local to the class, you cannot directly reference them outside of the class. In order to reference them you need to use the <u>scope resolution operator</u> (:: double colon). 

For example:

	void clockType::setTime(int hours, int minutes, int seconds) {
		if (0<=hours && hours<24)
			hr = hours;
		else
			hr = 0;
		
		if (0<=minutes && minutes < 60)
			min = minutes;
		else
			min = 0;
		
		if (0<=seconds && seconds<60)
			sec = seconds;
		else
			sec = 0;
	}

The member functions `setTime` is a `void` function and has three parameters. Therefor:
- a call to this function is a stand-alone statement.
- we must use three parameters in a call to this function.

since `setTime` is a member of the `class clockType`, it can directly access the member variables.


A call to the function `setTime` in the example would look like:

	myClock.setTime(3, 48, 52);

![[Pasted image 20240330004939.png]]

more examples seen in the chapter (section 10-1i)

---

## Accessor and Mutator Functions

<u>Accessor functions</u> - member functions in a class that only access but do not modify the member variables. have `const` at the end of their heading.

<u>Mutator functions</u> - member functions in a class that modify the member variables.

Since accessor functions only access the values of the member variables, we typically include the reserved word `const` at the end of the headings of these functions as a safeguard.

- A member function of a class is called a <u>constant function</u> if its heading contains the reserved word `const` at the end.
	- A constant member function of a class **can *only* call other constant member functions of that class**.

more examples seen in chapter (section 10-1j)

---

## Constructors

When a class object is declared, a constructor is automatically executed.

To guarantee that the member variables of a class are initialized, you use <u>constructors</u>.

There are two types of constructors:
- with parameters
- without parameters (called the <u>default constructor</u>)

Constructors have the following properties:
- The name of a constructor is the same as the name of the class.
- A constructor is a function and it has no type. That is, it is neither a value-returning function nor a `void` function.
- A class can have more than one constructor. However, all constructors of a class have the same name.
- If a class has more than one constructor, the constructors must have different formal parameter lists (further info in chapter).
- Constructors execute automatically when a class object is declared and enters its scope. Because they have no types, they cannot be called like other functions.
- Which constructor executes depends on the types of values passed to the class object when the class object is declared.

Extended definition of the `class clockType` ([[#Clock Example|ref]]) by including two constructors:

	class clockType {
		pulbic:
			void setTime(int, int, int);
			void getTime(int&, int&, int&) const;
			void printTime() const;
			void incrementSeconds();
			void incrementMinutes();
			void incrementHours();
			bool equalTime(const clockType&) const;
			clockType(int, int, int); // constructor with parameters
			clockType(); // default constructor
			
		private:
			int hr;
			int min;
			int sec;
	}

definition of these functions is then written:

	clockType::clockType(int hours, int minutes, int seconds) {
		if (0<=hours && hours<24)
			hr = hours;
		else
			hr = 0;
		
		if (0<=minutes && minutes < 60)
			min = minutes;
		else
			min = 0;
		
		if (0<=seconds && seconds<60)
			sec = seconds;
		else
			sec = 0;
	}
	
	clockType::clockType() { // default constructor
		hr = 0;
		min = 0;
		sec = 0
	}

You can write the definition of the constructor with parameters by calling the function `setTime`, as follows:

	clockType::clockType(int hours, int minutes, int seconds) {
		setTime(hours, minutes, seconds);
	}

since `setTime` has the same code.

---

## Invoking a Constructor

Because a class might have more than one constructor, including the default constructor, it is important to know how to invoke a specific constructor.


#### <u>Invoking the Default Constructor</u>

Suppose that a class contains the default. The syntax to invoke the default constructor is:

	className classObjectName;

For example the statement below executes the default constructor:

	clockType yourClock;

Since no arguments are included in the declaration, the default constructor is executed and initializes the member variables of `yourClock` to 0.


#### <u>Invoking a Constructor with Parameters</u>

Suppose a class contains constructors with parameters. The syntax to invoke constructor with parameters is:

	className classObjectName(argument1, argument2, ...);

in which `argument1`, `argument2`, and so on are either a variable or an expression.

For example the statement below executes a constructor with parameters:

	clockType myClock(5, 12, 40);

since the variable types in the parameter of `myClock` match the variable types of the constructor `clockType`'s parameters, the `clockType` constructor with parameters is executed.

(more examples in 10-1o)

---

## Constructors and Default Parameters

A constructor can also have default parameters. The rules for declaring formal parameters are the same as those for declaring default formal parameters in a function.

You can replace both constructors:

	clockType(int, int, int);
	clockType();

using:

	clockType(int = 0, int = 0, int = 0);

This also allows you to declare `clockType` objects with zero, one, two, or three arguments:

	clockType clock1;
	clockType clock2(5);
	clockType clock3(12, 30);
	clockType clock4(7, 34, 18);

All member variables of `clock1` are initialized to 0. The member variable `hr` of `clock2` is initialized to 5, while all other member variables of `clock2` are initialized to 0. And so on.

Using these conventions, we can say that a constructor that has no parameters, or has all default parameters, is called the **default constructor**.

---

## Classes and Constructors: A Precaution

The important things to remember about classes and constructors are the following:
- If a class has no constructor(s), C++ automatically provides the default constructor. However, the object declared is still uninitialized.

- On the other hand, suppose a `class`, say, `dummyClass`, includes constructor(s) with parameter(s) and does not include the default constructor. In this case, C++ does not provide the default constructor for the `class dummyClass`. 

more info (10-1q).

---

## In-Class Initialization of Data members and the Default Constructor

You can also initialize data members when they are declared in a class. 

For example:

	class clockType {
		pulbic:
			void setTime(int, int, int);
			void getTime(int&, int&, int&) const;
			void printTime() const;
			void incrementSeconds();
			void incrementMinutes();
			void incrementHours();
			bool equalTime(const clockType&) const;
			clockType(int, int, int); // constructor with parameters
			clockType(); // default constructor
			
		private:
			int hr = 0; // initialized
			int min = 0; // initialized
			int sec = 0; // initialized
	}

In this class definition, the data members `hr`, `min`, and `sec` are declared as well as initialized. This is called in-class initialization of the data members.

If an object is declared with parameters, then the default values are overridden by the constructor with the parameters.

Example:

	clockType myTime;
	clockType yourTime(3, 40, 18);

The `hr`, `min`, and `sec` of `myTime` are each set to 0. While the `hr`, `min`, and `sec` of `yourTime` are set to 3, 40, and 18 respectively.

more info(10-r)

---

## Arrays of Class Objects (Variables) and Constructors

If a class has constructors and you declare an array of that class’s objects, the class should have the default constructor. The default constructor is typically used to initialize each (array) class object.

Suppose that you have 100 employees who are paid on an hourly basis, and you need to keep track of their arrival and departure times. You can declare two arrays, `arrrivalTimeEmp` and `departureTimeEmp`, of 100 components each where each component is an object of type `clockType`.

Example:

	clockType arrivalTimeEmp[100];

![[Pasted image 20240330032521.png]]

you can then use functions of `clockType` to manipulate the time for each employee:

	arrivalTimeEmp[49].setTime(8, 5, 10);

![[Pasted image 20240330032639.png]]

This data can be outputted for each employee using a loop:

	for (int j=0;j<100;j++) {
		cout << "Employee " << (j+1) 
			 << " arrival time:";
		arricalTimeEmp[j].printTime();
		cout << endl;
	}

more in section 10-1s

---

## Destructors

Like constructors, destructors are also functions. Moreover, like constructors, a destructor does not have a type.

A class can only have one destructor, and the destructor has no parameters.

The name of a destructor is the tilde character (~), followed by the name of the class. For example, the name if the destructor for the `class clockType` is :

	~clockType();

The destructor automatically executes when the class object goes out of scope.

---

## Data Abstraction, Classes, and Abstract Data Types

Separating the design details from its use is called <u>abstraction</u>.

<u>Data abstraction</u> - a process of separating the logical properties of the data from its implementation.

<u>Abstract data type (ADT)</u> - A data type that separates the logical properties from the logical implementation details.


Like other data types such as `int`, an ADT has three things associated with it:
- The name of the ADT (called the <u>type name</u>).
- The set of values belonging to the ADT (called the <u>domain</u>).
- And the set of <u>operations</u> on the data.

more info on 10-2

---

## A `struct` versus a `class`

Both C++ classes and structs have the same capabilities. However most programmers restrict their use of structures to adhere to their C-like structure form and thus do not use them to include member functions.

If all of the member variables of a `class` are `public` and the `class` has no member functions,, you typically use a struct to group these member variables.

---

## Information Hiding

<u>Implementation file</u> - stores implementation details. Contains the definitions of the functions to implement the operations of an object.

<u>header file (interface file)</u> - file that contains the specification details.

For any info on this topic refer to 10-3 in book. There is a lot of important info I'm too lazy to condense.

---

## Executable Code

10-4

---

More examples of classes are shown in 10-5

---
## Inline functions

However, in the definition of a class you can give the complete definition of a member function. Such member functions definitions are called <u>inline function definitions</u>.

Suppose that you want to include a function to return the hours of a clock. You can write the definition of the class `clockType` as follows:

	class clockType {
		public:
			void setTime(int, hours, int minutes, int seconds);
			void getTime(int& hours, int& minutes, int& seconds) const;
			void printTime() const;
			
			void incrementSeconds();
			void incrementMinutes();
			void incrementHours();
			
			bool equalTime(const clockType& otherClock) const;
			
			int getHours() const {
				return hr;
			}
			
			clockType(int hours = 0, minutes = 0, seconds = 0);
			
		private:
			int hr;
			int min;
			int sec;
	}

In this definition the function `getHours` is inline.

**Inline functions are typically used for very short function definitions.**

The compiler treats inline functions in a special way. It typically inserts the code of an inline function <u>at every location the function is called</u>.

---

## Static Members of a Class

A class can have <u>static</u> members, functions, or variables.

Things to note about static members of a class:
- If a function of a class is `static`, in the class definition it is declared using the keyword `static` in its heading.
- If a member variable of a class is `static`, it is declared using the keyword `static`.
- A `public` `static` member, function, or variable of a class can be accessed using the class name and the scope resolution operator (::).

more info in 10-7 to use as needed.