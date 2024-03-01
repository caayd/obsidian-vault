Unit 8 ref

---
# Lib
[[Arrays#Arrays |Arrays]]
[[Arrays#Accessing Array Components |Accessing Array Components]]
[[Arrays#Processing One-Dimensional Arrays |Processing One-Dimensional Arrays]]
[[Arrays#Out of bounds |Out of Bounds]]
[[Arrays#Initialization in declaration |Initialization in declaration]]
- [[Arrays#Partial Initialization in declaration |Partial Initialization in declaration]]
[[Arrays#Some Restrictions on Array Processing |Dont-Dos]]
[[Arrays#Arrays as Parameters to Functions |Arrays in Function Parameters]]


[[Arrays#Two- and Multidimensional Arrays |Two- and Multidimensional Arrays]]



---
# Arrays

passed by reference only

An <u>array</u> is a collection of a fixed number of elements all of the same data type and in adjacent memory (all int, char, string, etc.).

A <u>one-dimensional array</u> is an array in which all components are arranged in a list form.

general form of a one-dimensional array:

	dataType arrayName[intExp];

- `intExp` - specifies the number of components

Example:

	int num[5];

creates an array with components `num[0], num[1], num[2], num[3], and num[4]

(arrays start at 0)

---

# Accessing Array Components

syntax for accessing array components:

	arrayName[indexExp]

- `indexExp` ( index ) - specifies the position of component in array ^dd0b51

Example:

	int list[10] //creates components list[0] to list[9]
	
	list[5] = 34; //stores 34 in list[5]
	list[3] = 63; //stores 63 in list[3]
	list[4] = list[5] + list[3];

97 would be stored in `list[4]`

Example 2:

	int i = 3;
	list[i - 1] = 20; \\stores 20 in list[2]

**You must specify the size of the array when declaring it.
**

---
# Processing One-Dimensional Arrays

<u>Finding Max Value</u>
This code will find the largest value in an index

	maxIndex = 0;
	for(int index = 1; index < 10; index++)
		if(sales[maxIndex] < sales[index])
			maxIndex = index;
	largestScale = sales[maxIndex];

the code goes through each value and sets the `maxIndex` to whatever value of `index` is larger than it. After the loop is finished, `largestScale` will be the largest value in the array.

The same idea can be used to find numbers less than a certain parameter.

---

# Out of bounds

The [[Arrays#^dd0b51 |index]] of an array is out of bounds if it is < 0

Example:

	int list[10];
	
	for(int i = 0; i <= 10; i++)
		list[i] = 0;

When `i` becomes 10, the loop's test condition: `i <= 10` becomes `true` and the body of the loop executes, storing 0 in `list[10]`.

---

# Initialization in declaration

You initialize an array's values during its declaration, example:

	double sales[5] = {12.25, 32.50, 16.90, 16.90, 23, 45.60};

sets `sales[0] = 12.25`, `sales[1] = 32.50`, etc.

When doing this, you don't need to specify the size of the array:

	double sales[] = {12.25, 32.50, 16.90, 16.90, 23, 45.60};

is still equivalent to the example above (you must always have the brackets).

##### Partial Initialization in declaration

You don't need to initialize all components of an array:

	int list[10] = {8, 5, 12};

`list[0] = 8`, `list[1] = 5`, `list[2] = 12`, all other components are set to 0.

---

# Some Restrictions on Array Processing

You cannot use aggregate operations on arrays:

	int myList[5] = {0, 2, 1, 6, 5};
	int yourlist[5];
	
	yourList = myList;

the above code will not make both array values equal to each other.

instead do:

	yourList[0] = myList[0];
	yourList[1] = myList[1];
	yourList[2] = myList[2];
	yourList[3] = myList[3];
	yourList[4] = myList[4];

or, with loops:

	for(in index = 0; index < 5; index++)
		yourList[index] = myList[index];

---

# Arrays as Parameters to Functions

When declaring a one-dimensional array as a formal parameter, the size of the array is usually not included. If you do specify the size, it will be ignored.

Example of an array as a parameter to a function:

	void initialize(int list[], int listSize)
	{
		for(int count = 0; count < listSize; count++)
			list[count] = 0
	}

#### Constant Arrays as Parameters

	void example(ing x[], const int y[], int sizeX, int sizeY)
	{
	}

using const before the `y` array allows the `example` function to modify the array `x` but not `y`.

this can is useful if you want to preserve stored data in an array from another function.

---

# Base Address

<u>Base address</u> - the memory address of the first component in an array. 

ex: if `list` is a one-dimensional array, the base address is `list[0]`.

in the code:

	if (myList <= yourList)

where both `myList` and `yourList` are arrays, `mylist <= yourlist` would evaluate to `true` if the value of the base address of `myList` is less than the the value of the base address of `yourList`.

---
# Other Ways to Declare Arrays

Examples:

	//changes size of arrays outside of declaration
	const int NO_OF_STUDENTS = 20;
	int testScores[NO_OF_STUDENTS]; 

also:

	const int SIZE = 50;
	typedef double list[SIZE];
	
	list yourList;
	list myList;
	
	//equiv to:
	
	double yourList[50];
	double myList[50];
---
# Searching an Array for a Specific Item

A <u>sequential search</u> or <u>linear search</u> searches an array starting from the first array element, comparing a given value with the values of the elements in the array until there are no more elements


### Sorting

In a <u>selection sort algorithim</u> we rearrange the list by selecting an element in the list and moving it to its proper position. The first time, we locate the smallest item in the entire list. The second time, we locate the smallest item in the list starting from the second element in the list, and so on.

ex (Pseudo):

	for(index = 0; index < length - 1; index ++)
	{
		a.Find smallest element in list[index]... list[length - 1].
		b.Swap smallest element with list[index].
	}

---
# Auto Declaration and Range-Based For Loops

The following statement declares the variable num and stores 15 in it:

	auto num = 15;

since 15 is an int value the num is set to int

A <u>ranged-based for</u> loop is used to process the elements of an array, its syntax:

	for(dataType identifier : arrayName)
		statements

`identifier` is a variable and the data type of `identifier` is the same as the data type of array elements.

You can also use auto declaration in a range-based loop to process the elements of an array. For example, using the range-based for loop, the for loop to find the largest element in the array list can be written as:

	for(auto num : list)
	{
		if(max < num)
			max = num;
	}

---
# C-Strings (Character Arrays)

Character arrays are arrays with of type `char`.

null is the first character in the ASCII character set and is represented by '`\0`'. This character is less than any other character in the `char` data set.

C-Strings are null-terminated so `"A"` represents two characters: `'A'` and `'\0'`.

The statement:

	char name[16] = {'J', 'o', 'h', 'n', '\0'};

is equivalent to the statement:

	char name[16] = "John";


### String Comparison

C-strings are compared character by character until one character is greater than the other:

- The C-string `'Air'` is less than the C-string `'Boat'` because the first character of `'Air'` is less than the first character of `'Boat'`.
- The C-string `'Air'` is less than the C-string `'An'` because the first character of both strings are the same, but the second character in `'An'` is greater than the second character in `'Air'`.

C-strings are stored in double quotation marks

---

# `string` Type Input/Output Files

Values of type `string` are not null terminated.

To convert a `string` to a C-string you need to use the function `c_str`:

	strVar.c_str()

 in which `strVar` is a var type of `string`

You can use this to read files:

	ifstream infile;
	string fileName;
	cout << "Enter the input file name: ";
	cin >> fileName
	
	infile.open(fileName.c_str());

this code will read the user input to open a desired file (when including `string` header file).

The function strcmp (s1, s2) returns 0 if s1 and s2 are the same

---

# Parallel Arrays

Two (or more) arrays are called parallel if their corresponding components hold related information. For example, an array for a students ID number (`int`) and a corresponding array for the student's letter grade (`char`).

---

# Two- and Multidimensional Arrays

stored in <u>row order form</u> in computer memory

syntax for declaring a two-dimensional array:

	dataType arrayName[intExp1][intExp2];

Example:

	double sales[10][5];

the two-dimensional array `sales` has 10 rows and 5 columns in which every data type is `double`.

![[Pasted image 20240226204934.png|300]]

---

# Accessing Components of Two-dimensional Arrays

syntax for accessing a component of a two-dimensional array:

	arrayName[indexExp1][indexExp2]

`indexExp1` specifies the row position and `indexExp2` specifies the column position.

The statement:

	sales[5][3] = 25.75;

stores `25.75` into row 5 and column 3

![[Pasted image 20240226205512.png|300]]

This statement could also be written using variables:

	int i = 5;
	int j = 3;
	
	sales[i][j] = 25.75

----

# Two-Dimensional Array Initialization during Declaration

in the following code:

	ind board[4][3] = {{2, 3, 1}, {15, 25, 13}, {20, 4, 7}, {11, 18, 14}};

`board` is 4 rows and three columns
- Row 1 contains elements 2, 3, and 1
- Row 2 contains elements 15, 25, and 13
- Row 3 contains elements 20, 4, and 7
- Row 4 contains elements 11, 18, and 14

For number arrays, if all components of a row are not specified, the unspecified components are initialized to 0. In this case, at least one of the values must be given to initialize all the components of a row.

---

### Processing Two-Dimensional Arrays

A two-dimensional array can be processed in four ways:

1. Process a single element.
2. Process the entire array.
3. Process a particular row of the array, called <u>row processing.</u>
4. Process a particular column of the array, called <u>column processing.</u>

For example look at the array:

	const int NUMBER_OF_ROWS = 7;
	const int NUMBER_OF_COLUMNS = 6;
	
	int matrix[NUMBER_OF_ROWS][NUMBER_OF_COLUMNS];

to process row 5 you would need to process elements: `martix[5][0], martix[5][1], martix[5][2]`... all the way to `martix[5][5]`

this could be done in a loop:

	for(i = 0; col < NUMBER_OF_COLUMNS; i++)
		process matrix[5][i];

---
#### Sum by row

using a nested for loop you can find the sum of a row:

	for(row = 0; row < NUMBER_OF_ROWS; row++)
	{
		sum = 0;
		for(col = 0; col < NUMBER_OF_COLUMNS; col++)
			sum = sum + matrix[row][col];
			
		cout << "Sum of row " << row + 1 << " = " << sum << endl;
	}

This is pretty much the same with columns just flipped

---

# Arrays of Strings

You can declare an array of 100 components of type string as follows:

	string list[100];

You can declare a two-dimensional array of characters of 100 rows and 16 columns as follows:

	string list[100][16];

The following statement stores "Snow White" in `list[1]`

	strcpy(list[1], "Snow White");

![[Pasted image 20240226212300.png|300]]

---

# Multidimensional Arrays

You can also define three-dimensional or longer arrays. 

The general syntax for declaring an n-dimensional array is:

	dataType arrayName[intExp1][intExp2] ... [intExpn];

The syntax to access a component of an n-dimensional array is:

	arrayName[intExp1][intExp2] ... [intExpn]

For example:

		double carDealers[10][5][7];

the size of the first dimension is 10, the second dimension 5, and the third dimension 7, creating a total of 350 components (10 * 5 * 7).