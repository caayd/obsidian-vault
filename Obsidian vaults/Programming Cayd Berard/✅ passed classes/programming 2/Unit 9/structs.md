
---
# Structs 

`struct` -  collection of a fixed number of components in which the components are accessed by name. The components may be of different types.

components of a `struct` are called members.

the general syntax for a `struct` is:

	struct structName {
		dataType1 identifier1;
		dataType2 identifier2;
		.
		.
		.
		dataTypen identifiern
	};

The semicolon at the end of the bracket is necessary

Example:

	struct houseType {
		string style;
		int numOfBedroom;
		int numOfBathrooms;
		int numOfCarsGarage;
		int yearBuilt;
		int finishedSqaureFootage;
		double price;
		double tax;
	};

defines a `struct houseType` with eight members of varying types. 

a `struct` <u>is a definition, not a declaration, it defines only a data type; no memory is allocated.</u>

using the example:

	//variable declaration
	houseType newHouse;

The memory allocated is large enough to store `style`, `numOfBedrooms`, `numOfBathrooms`, `numOfCarsGarage`, `yearBuilt`, `finishedSquareFootage`, `price`, and `tax`.

you can also declare the variable directly after the variable:

	struct houseType {
		.
		.
		.
	} newHouse;

You usually define a `struct` before the definitions of all the functions in the program so that the `struct` can be used throughout the program.


---

## Accessing `struct` Members

 To access a struct member, you use the struct variable name together with the member name:

	structVariableName.memberName

The dot separating both names is an operator called the <u>member access operator</u>.

Example: 

	struct studentType {
		string firstName;
		string lastName;
		char courseGrade;
		int testScore;
		int programmingScore;
		double GPA;
	};
	
	//variables
	studentType newStudent;
	studentType student;

you can initialize the member of `GPA` of `newStudent` to `0.0`:

	newStudent.GPA = 0.0;

same with the names:

	newStudent.firstName = "John";
	newStudent.lastName = "Brown";


![[Pasted image 20240313213700.png|250]]

you can store values with `cin` inputs:

	cin >> newStudent.firstName;

also works with multiple values:

	cin >> newStudent.testScore >> newStudent.programmingScore;

Example:

	score = (newStudent.testScore + newStudent.programmingScore) / 2;
finds the average of `testScore` and `programmingScore` and stores it in `score`.

you can then test and store the grade:

	if (score >= 90)
		newStudent.courseGrade ='A';
	else if (score >= 80)
		newStudent.courseGrade = 'B';
	.
	.
	.

---

## Assignment

you can assign the values from one `struct` variable to another `struct` variable:

![[Pasted image 20240313215319.png]]

	student = newStudent;

![[Pasted image 20240313215338.png]]

---

## Comparison

you can compare `structs` like:

	if (student.firstName == newStudent.firstName) && (student.lastName == newStudent.lastName)

you cannot use relational operators:

	if (student == newStudent) // illegal

---

## Input/Output

Data in a `struct` variable must be read one member at a time, and the contents of a `struct` variable must be written one member at a time.

Example:

	cout << newStudent.firstName << " " << newStudent.lastName
	<< " " << newStudent.courseGrade
	<< " " << newStudent.testScore
	<< " " << newStudent.programmingScore
	<< " " << newStudent.GPA << endl;

will output all the contents of the `struct` variable `newStudent`.

---

# `struct` Variables and Functions

- A `struct` variable can be passed as a parameter either by value or by reference.
- Unlike Arrays, a function <u>can</u> return a value of type struct.

Example:

	void readIn(studentType& student) {
		int score;
		cin >> student.firstName >> student.lastName;
		cin >> student.testScore >> student.programmingScore;
		cin >> student.GPA;
		
		score = (student.testScore +  student.programmingScore) / 2;
		
		if (score >= 90)
			student.courseGrade = 'A';
		else if (score >= 80)
			student.courseGrade = 'B';
		else if (score >= 70)
			student.courseGrade = 'c';
		else if (score >= 60)
			student.courseGrade = 'D';
		else
			student.courseGrade = 'F';
	}

The statement;

	readIn(newStudent);

calls the `readIn` function and stores the appropriate info in the variable `newStudent`.

---

### Arrays v. `struct`s

|Aggregate Operation|Array|struct|
|---|---|---|
|Arithmetic|No|No|
|Assignment|No|Yes|
|Input/output|No (except strings)|No|
|Comparison|No|No|
|Parameter passing|By reference only|By value or by reference|
|Function returning a value|No|Yes|

---

# Arrays in `structs`

	const int ARRAY_SIZE = 1000;
	
	struct listType {
		int listElem[ARRAY_SIZE]; // array containing lsit
		int listLength; // length of list
	}
	
	listType intList;

![[Pasted image 20240313221324.png]]

more in chapter

---

# `struct`s in Arrays

	struct employeeType {
		string firstName;
		string lastName;
		int personID;
		string deptID;
		double yearlySalary;
		double monthlySalary;
		double yearToDatePaid;
		double monthlyBonus;
	}

you could make an array for each employee:

	employeeType employees[50];

where each element in the array holds all the members of the struct.

![[Pasted image 20240313221836.png|400]]

more info in chapter

---

# `struct`s within a `struct`

	struct nameType {
		string first;
		string middle;
		string last;
	}:
	
	struct addressType {
		.
		.
	};
	
	struct dateType {
		.
		.
	};
	
	struct contactType {
		.
		.
	};

you can use these structs inside another struct:

	struct employeeType {
		nameType name;
		string empID;
		addressType address;
		dateType hireDate;
		dateType quitDate;
		contactType contact;
		string deptID;
		double salary;
	};

Example:

	employeeTpye newEmployee;

looks like:

![[Pasted image 20240313222541.png]]

programming example in chapter.

---

