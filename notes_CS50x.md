# CS50x Lecture 1 C
## Basics
* Vars need to be declared
* declare " int number;"; assignment "number = 17;"; initialisation "int num = 12;"
* semicolons on the line end
* %s as placeholder for content of Var (%s= string, %i=int, %f=float, %li=long, %c=char)
* * if a %i is used for a char or str[] the ACSII number gets printed and vice versa
* make Filename (without filetype ending) to build
* ./Filename (without filetype ending)  to run
* Datatypes(most common):
* * [char; double; float; int; void* ] auto included in C; [bool; string; ] from CS50.h
* * * Void is type not a Datatype for empty return Values parameters etc
* for strings ""    for chars ''
* modulus %
* logical OR || ; logical AND &&; logical NOT !; 
* strings can't be compared with == need function strmp(string_1, string_2) == 0
* increment ++ decrement --
*  += ; -= ; *= ; /= are called syntactic sugar
*  bool 1 byte; int 4 bytes; long 8 bytes; float 4 bytes; double 8 bytes; char 1 byte


```{c}
#include <stdio.h>
#include <cs50.h>

int main(void)
{
    string answer= get_string("Whats your name? ");
    printf("hello, %s\n", answer);
}
```
## conditional statements
### if else
```{c}
#include <stdio.h>
#include <cs50.h>

int main(void)
{
    if (boolean)
    {
        printf("Example");
    }
    else if
    {
        printf("example 2");
    }
    else
    {
        printf("example 3");
    }
}
```
### switch statement
* without the "break" all cases underneath will be executed too
```{c}
int x = Input;
switch(x)
{
    case 1:
        printf("it's one\n");
        break;
    case "Lala":
        printf("it's Lala\n");
        break;
    case 4:
        printf("it's 4\n");
        break;
    case 22:
        printf("it's 22\n");
        break;
    default:
        printf("Sorry, bad Luck");
}
```
### ternary operator

```{c}
int x = (boolean) ? 5 : 6;

==

int x;
if(boolean)
{
    x = 5;
}
else
{
    x = 6;
}
```
## Loops
### while Loops

```{c}
#include <stdio.h>

int main(void)
{
    int i = 0;
    while (i > 3)
    {
        printf("meow\n");
        i++;
    }
}

endless loop:
while(true)
{
    example 
}
```

### for Loops
syntax inside the for loop for (declare var; condition; action)
```{c}
#include <stdio.h>

int main(void)
{
    for (int i=0; i < 3; i++)
    {
        printf("meow\n");
    }
}
```
## writing functions
* return_type  name(argument-list)
* when calling a function it either must be above the call or the declaration line (prototype)
  must be copied above the call
```{c}
#include <stdio.h>
#include <cs50.h>

void meow(void);

int main(void)
{
    for (int i=0; i < 3; i++)
    {
        meow();
    }
}

void meow(void)
{
    printf("Meow\n");
}
```
```{c}
#include <stdio.h>
#include <cs50.h>

void Meow(void);

int main(void)
{
    Meow(3);
}


void Meow(int n)
{
    for (int i=0; i < n; i++)
    {
        printf("Meow\n");
    }
}
```
* Scope: context in which Vars exist
* * Vars declared globally can be accessed and changed by any function even if they dont return a value
* constant vars "const int Var", they are read only vars that can not be changed once declared
* do while for while with at least one

```{c}
int main(void)
{
    // makes single line comments
    do
    {
        n = get_int("Size ")
    }
    while (n <1);
}
```
* integer overflow happens when there is not enough Memory(RAM) for a programm and the 
  numbers loop back around trying to count up higher than there are bits
  eg with a 32 bit RAM you can count up to 2^32 but counting one higher would mean
  that all the ones turn to 0 and the 33 bit to one which doesnt exists ergo Looping around
  in C "int" and "float" use 32 bits "long" and "double" use 64 bits. unsigned Datatypes 
  have only positive values so an "unsigned int" uses 2^32 where in a normal int half of 
  that would be reserved for negative numbers. "unsigned" is a qualifier.

```{c}
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int x= get_int();
    int y = get_int();

    float z = (float) x / (float) y;
    printf("%f\n", z);
}
```
* if you divide two ints everything after the decimal point gets truncated not rounded even if
  the var where its saved is a float 

# CS50x Lecture 2 Arrays
## compilation 
* clang auto creates a FILE ./a; clang -o names_file file.c
* needs command line args to define the compilation
* libraries need to be linked thru command line with -l; clang -o names_file file.c -lcs50
* make is created by CS50 and only works in their could version of VSCode
  
compiling as used today consists of 4 steps
1. preprocessing - (for included libs prototypes for used functions are processed)
2. compiling - converting C code to Assembly code
3. assembling - convert to binary
4. linking - links the base files from the libraries 

* CS50 cloud version of VSCode also has a Debugger "debug50 ./Filename" a breakpoint must be 
  set (red dot right beside the line number )
## Arrays
* type name[size];
* type name[] = {1, 2, 3} // sets size to number of inputs
* you cant assign one array to another, loop over each element instead
* arrays are not passed by Value(copied) like other vars, they are passed by reference so a function call changes the actual array without a return value
```{c}
int scores[3];
scores[0] = 72;
scores[1] = 73;
scores[2] = 33;

==
const int N = 3
int scores[N];
for (int i = 0; i < N; i++)
{
    scores[i]= get_int("Score: ");
}

```
* strings a re arrays that have a length(num of bytes) of num_of_chars + 1 because the strings 
  always end with a all-0 byte(sentinel value \0 NUL) that declares the end of the string to the memory
* arrays are structures wherein several Values can be saved and accessed via indexes
* arrays need a set number of entries at declaration (for Memory allocation) except strings see above 

```
#include <sc50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    int size = 5;
    int sequence[size];
    sequence[0] = 1;
    for (int i = 1; i < size; i++)
    {
        sequence[i] = sequence[i-1] * 2;
    }
    
}
```
```
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    string phrase = get_string("");
    for (int i = 0, lenght = strlen(phrase); i < lenght - 1; i++) // lenghtb -1 since we dont want to check the last letter aginst a random memory space
    {   // assuming the input is all uppercase
        if (phrase[i]> phrase[i + 1])
        {
            printf("Not in alphabetical order\n");
            return 0;
        }
    }
    printf("Alphabetical order\n");
    return 0;
}
```
## command line arguments
```
#include <cs50.h>
#include <studio.h>

int main(int argc, string argv[]) #argc argument count argv argument vector
{
    if (argc == 2)
    {
        printf("hello, %s\n", argv[1]); # argv[0] is the filename
    }
}
    == Loop

    for (int i=0; i < argc; i++)
    {
        printf("hello, %s\n", argv[i]);
    }

```
```
#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>

int main(int argc, string argv[])
{
    if (argc != 2)
    {
        printf("Usage: filename and Argument needed") //catches the error if no arg is given
        return 1
    }
    int height = atoi(argv[1]); // casts string as int
}
```

## exit status
```
#include <cs50.h>
#include <studio.h>

int main(int argc, string argv[]) #argc argument count argv argument vector
{
    if (argc != 2)
    {
        printf("Missing command-line argument\n");
        return 1;
    }
    printf("hello, %s\n", argv[1]); # argv[0] is the filename
    return 0
}
```
* echo $? shows exit status from the last command -- Windows??

# CS50x Lecture 3 Algorithms

* binary search - divide and conquer, always half, like the phonebook example (only possible if sorted)
* linear search going in a line like from left to right
### Big O notation
* Big O Omega and Theta are asymptomatic Notations
* Big O notation always describes how log a Algorithm takes in the worst case
* in a graph linear search would be time n since in the worst case you would need to go thru all of the data
  taking every second data point would be n/2
  and binary search - halfing the data points each time and check for direction - would be log2n
* in CS this is shown in the order of a time complexity 
* * they are declared more broadly where n and n/2 would be in the order of n -> O(n)
* * and log2n would be in ther oder of log n -> O(log n)
* * common ones are 
* O(n^2), quadratic time
* O(n log n), - n log n
* O(n) - linear Time, 
* O(log n), - logarithmic time
* O(1)- constant Time[doesn't necessarily 1 step just a constant number independent of n]

### Omega notation
* describes the time complexity in the best case
* same notation as Big O: Ω(n^2); Ω(n log n); Ω(n); Ω(log n); Ω(1)
* so linear search would be O(n) and Ω(1)
* binary would be O(log n) and Ω(1)

### Theta notation
* describes Big O and Ω beeing the same for a Alogrithm like counting linear, to get to end you always have to count n times
* Θ(n^2); ΘΩ(n log n); Θ(n); Θ(log n); Θ(1)
## searching
linear search
```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int numbers[] = {20,5,48,396,2,154,52,50};

    int n = get_int("Number: ");
    for (int i = 0; i < 8; i++)
    {
        if (numbers[i] == n)
        {
            printf("Found\n");
            return 0;
        }
    }
    printf("not found\n");
    return 1;
}
```
* doing this for strings would require strcmp from string.h
## creating oown data structure
```
typedef struct
{
    string name;
    string number;
}
person; //creates a Datatype person where each person has number nad a name

int main(void)
{
    person people[3];
    people[0].name = "Carter";
    people[0].number = "0123";
    - forloop, name= input
    if (strcmp(people[i].name, name) == 0)

}
```
## sorting
* selection sort - find smallest number swap it to the beginning and go again
* * (n-1) + (n-2) + (n-3)...+1 == n(n-1)/2 so its circa O(n^2) and Ω(n^2)
* bubble sort - if the current number is smaller that the next, swap them, if there are no swaps in one run, quit
* * (n-1) x (n-1) == O(n^2) Ω(n) - since if all is sorted the algorith exits

## recursion
* recursion is a description for a function that calls itself
```
#include <cs50.h>
#include <stdio.h>

void draw(int n);
void draw2(int n);

int main(void)
{
    int height = get_int("");
    draw(height);
    draw2(height);
}

void draw(int n)
{
    for (int i = 0; i < n ; i++)
    {
        for (int j = 0; j < i+1; j++)
        {
            printf("#");
        }
        printf("\n");
    }
}

void draw2(int n)
{
    // if no more rows needed n=0 exit draw
    if (n<= 0)
    {
        return;
    }
    //print pyramid of hight n-1
    draw2(n-1);
    // print one more row with one less block each time
    for (int i = 0; i < n; i++)
    {
        printf("#");
    }
    printf("\n");
}

```
## merge sort
* sort left half of numbers the right half then merge them, if there is only one number quit
* merge means going thru both lists comparing the first entry and taking the smallest one to a new array
* sorting one half means recursivly calling merge sort till only one number is on each side then merge there is memory needed for each halfing and sorting
* generally if you want to solve something quicker you need more space and vice versa
* O(n log n) Ω(n log n)