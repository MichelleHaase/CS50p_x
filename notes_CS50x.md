# CS50x Lecture 1 C
## Basics
* Vars need to be declared
* declare " int number;"; assignment "number = 17;"; initialisation "int num = 12;"
* semicolons on the line end
* %s as placeholder for content of Var (%s= string, %i=int, %f=float, %li=long, %c=char, %p=pointer)
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


```c
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
```c
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
```c
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

```c
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

```c
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
```c
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
```c
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
```c
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
* global constants can also be declared as "#define Varname Value", eg "#define MAX 9" no assignment operator needed
* do while for while with at least one

```c
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

```c
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
* libraries need to be linked through command line with -l; clang -o names_file file.c -lcs50
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
```c
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

```c
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
```c
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
```c
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
```c
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
```c
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
* in a graph linear search would be time n since in the worst case you would need to go through all of the data
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
* describes Big O and Ω being the same for a Algorithm like counting linear, to get to end you always have to count n times
* Θ(n^2); ΘΩ(n log n); Θ(n); Θ(log n); Θ(1)

## creating own data structure
```c
typedef struct
{
    string name;
    string number;
}
person; //creates a Datatype person where each person has number nad a name(members)

int main(void)
{
    person people[3];
    people[0].name = "Carter";
    people[0].number = "0123";
    - forloop, name= input
    if (strcmp(people[i].name, name) == 0)

}
```

## searching
### linear search
```c
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

### merge sort
* sort left half of numbers the right half then merge them, if there is only one number quit
* merge means going through both lists comparing the first entry and taking the smallest one to a new array
* sorting one half means recursivly calling merge sort till only one number is on each side then merge there is memory needed for each halfing and sorting
* generally if you want to solve something quicker you need more space and vice versa
* O(n log n) Ω(n log n)
  
## sorting
* selection sort - find smallest number swap it to the beginning and go again
* * (n-1) + (n-2) + (n-3)...+1 == n(n-1)/2 so its circa O(n^2) and Ω(n^2)
* bubble sort - if the current number is smaller that the next, swap them, if there are no swaps in one run, quit
* * (n-1) x (n-1) == O(n^2) Ω(n) - since if all is sorted the algorith exits

## recursion
* recursion is a description for a function that calls itself
```c
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
# CS50x Lecture 4 Memory
## Hexadecimal
* 16 chars 0123456789ABCDEF
* 0-9 == 00-09; 10-15 == 0A-0F; 16-25 == 10-19 20 == 1A ... 255 == FF
* by convention prefixed by 0x as indicator for a Hexadecimal number
* to check if a byte partly matches a conditional for Hex
* *  (Array[index] & 0xf0) == 0xe0 - checks for the inforamtion in Array at index for the first 
      4 bits if they match "e" nulling the later 4 bits
  
## Pointers
* where information is located in Memory can be queried with &
* with the "*"  a var is declared as a pointer that points to ie an ints location
* using "*" outside of declaration means to go to the saved address
* if the pointer is just declared not initialized it should be set to NULL so it cant accidentally access random values(old addresses) 
* the * at initilization is part of the Datatype and part of the pointername 
  so int* a, b, c; creates a pointer to an int "a"  and two int vars "b" and "c"
  to create 3 pointers: int* a, *b, *c;

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%p\n", &n); // prints the Memory location in Hex

    int *p = &n; // creates a pointer var "p" with the Memory address of n
    printf("%p\n", p); // prints the in p saved location of n 
    printf("%p\n", *p); // prints the Value of the in p saved address from n
}
```
* vars with strings as implemented by CS50, are usually  pointers to first letter of the string 
* * the \0 NULL char that's on the end of the strings treminates the char array
* * the compilker assumes that a char* pointer has continues information till the \0

```c
string text = "LaLilu";
==
char* text = "LaLilu";
```

* thats also why compared strings with == doesn't work since the addresses are not equal
* pointer can be passed into functions so that functions can change Values outside of their Scope by changing the pointers
  this happens by passing by reference eg "void function_name(int* i, int* g)" the call would be function_name(&a, &b)

```c
void swap(int* a, int* b);
// checking the first 4 bytes for header of PDF or jpg
int main(int argc, char* argv[])
{
    int a = 5;
    int b = 6;
    swap(&a, &b);
    printf("a: %i\nb: %i\n", a, b);
}

void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
```
* accessing a the location where a pointer points to is called to dereference a pointer
* dereferencing a NULL pointer -> segmentation fault
### pointer arithmetics
* math on pointers
```c
char* s = "HI!";

printf("%c", s[0]);
printf("%c", s[1]);
printf("%c", s[2]);
==
printf("%c", *s);
printf("%c", (*s + 1));
printf("%c", (*s + 2));
```

## malloc and free
* in <stdlib.h>

```c
int main(void)
{
    char* s = hi
    char* t = s;
    t[0]= toupper(t[0]);

    printf("%s\n", s);
    printf("%s\n", t);
    // both print statements print out Hi since they point to the same changed Char
}

int main(void)
{
    char* s = hi
    char* t = malloc(strlen(s) + 1); // allocates memory to the array; plus 1 for \0
    if (t == NULL)
    {
        return 1; // returns error if the computer runs out of space
    }

    strcpy(t,s); // copies everyting from s into t; from <string.h>
    t[0]= toupper(t[0]);

    printf("%s\n", s);
    printf("%s\n", t); // now only t has the upper H
    free(t); frees the locked Memory after t is not used anymore
    return 0;
}
```
## valgrind
* catches mistakes in memory allocation that don't create errors
* USE: valgrind ./examplefile
* it catches stuff like overwriting values outside of arrays and not using free

## garbage Values
* values still stuck after memory gets allocvated but doesnt get values
* overwriting a not allocated location eg with *y = 13 can overwrite a RANDOM Value ANYWHERE

## overflow
* buffer overflow (buffer beeing a reserved space of memory); crqashes processes because of the missing memory to continue
** stack overflow
** heap overflow
## File I/O
```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    fopen("PATH.csv", "a"); // a r w
    char* name= get_string("Name: ");
    char* number = get_string("Number: ");
    fprintf(file, "%s,%s\n" , name, number)
}
```
```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

typedef unit8_t BYTE; //defines a byte sized datatype called BYTE

int main(int argc, char* argv[])
{
    FILE* sorce = fopen(argv[1], "rb"); // read binary Data
    FILE* destination = fopen(argv[2], "wb"); // write Binary Data

    BYTE b; // creating a byte sized empty Var called b

    while (fread(&b, sizeof(b), 1, sorce) !=0)
    // fread reads a chunk of information into the location of b(&b) that is the size
    // of b 1 at a time from the sorcefile, while there is data to read in.
    {
        fwrite(&b, sizeof(b), 1, destination);
        // fwrite writes what's stored at location of b(&b) in b sized chunkd 1 at a time
        // to the destination file
    }
    fclose(sorce);
    fclose(destination);
}

```
```c
int main(int argc, char* argv[])
{
    char* filename = argv[1];
    FILE* infile = fopen(filename, "r");
    unit8_t buffer[4];
    fread(buffer, 1, 4, infile);

    for (inti = 0; i<4; i++)
    {
        printf("%i\n", buffer[i]);
    }
    fclose(f);
}
```
 # CS50x Lecture 5 Datastructures
## abstract Data types
* a data type is a classification that defines the type of Data and what operations can be performed on it
* three main types
* * primitive eg int char
* * composite like arrays and classes
* * Abstract, define the operations and behavior of the data not the low level implementation
* * * eg stacks and ques have very specific operations like pop but they can be implemented with an Array or a linked list or similar
### Queues
* FIFO - First in, first out
* can be implemented with an Array as a data structure
* *enqueuing* means to form a queue
* *dequeuing* means to resolve the queue in order
```c
const in CAP = 50;

typedef struct
{
    person people[CAP];
    int size;
} queue;
```
### Stacks
* LIFO - Last in First out
* an item is *pushed* onto a stack
* and it's *poped* off 
* a stack can be implemented just like a queue the differences come the pop and push functions
  
### Linked List
* has its items in pairs, randomly placed in memory each item has two memory "slots" one for the item one for the pointer to the next node in the List, the last one has NULL instead of a pointer

#### Nodes
```c
typedef struct
{
    int number;
    struct node * next;
} node;
// doesnt work since the Node struct is named on line 5 and called on line 4

typedef struct node // names the datatype struct node
{
    int number;
    struct node * next;
} node; // shortens the datatype name to node
```
* linked lists are easiest to code in prepending nodes
* this reveres the order of the nodes
* searching a number wold be O(n) and prepending it self is constant time O(1)
```c
#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;
    struct node *next;
}
node;

int main(int argc, char *argv[])
{
    // Memory for numbers
    node *list = NULL;

    // For each command-line argument
    for (int i = 1; i < argc; i++)
    {
        // Convert argument to int
        int number = atoi(argv[i]);

        // Allocate node for number
        node *n = malloc(sizeof(node));
        if (n == NULL)
        {
            return 1;
        }
        n->number = number; // (*n).number == n->number
        n->next = NULL;

        // Prepend node to list
        n->next = list;
        list = n;
    }

    // Print numbers
    node *ptr = list;
    while (ptr != NULL)
    {
        printf("%i\n", ptr->number);
        ptr = ptr->next;
    }

    // Free memory
    ptr = list;
    while (ptr != NULL)
    {
        node *next = ptr->next;
        free(ptr);
        ptr = next;
    }
}
```
* a linked List can also be created by appending the nodes
* appending the list is O(n) since we need to iterate over it to find the ending

```c
... 

        n->number = get_int("Number: ");
        n->next = NULL;

        // If list is empty
        if (list == NULL)
        {
            // This node is the whole list
            list = n;
        }

        // If list has numbers already
        else
        {
            // Iterate over nodes in list
            for (node *ptr = list; ptr != NULL; ptr = ptr->next)
            {
                // If at end of list
                if (ptr->next == NULL)
                {
                    // Append node
                    ptr->next = n;
                    break;
                }
            }
        }
            // Free memory
    node *ptr = list;
    while (ptr != NULL)
    {
        node *next = ptr->next;
        free(ptr);
        ptr = next;
    }
    return 0;
```
SORTED VERSION
```c
...

// If list is empty
        if (list == NULL)
        {
            list = n;
        }

        // If number belongs at beginning of list
        else if (n->number < list->number)
        {
            n->next = list;
            list = n; 
        }

        // If number belongs later in list
        else
        {
            // Iterate over nodes in list
            for (node *ptr = list; ptr != NULL; ptr = ptr->next)
            {
                // If at end of list
                if (ptr->next == NULL)
                {
                    // Append node
                    ptr->next = n;
                    break;
                }

                // If in middle of list
                if (n->number < ptr->next->number)
                {
                    n->next = ptr->next;
                    ptr->next = n;
                    break;
                }
            }
        }
...
```
### Trees
#### binary search trees
* each node has two pointers pointing to the left and right child 
* a node with pointers set to NUll (no level underneath) is a Leaf
* the first Node is the root 
* nodes above the level of their children are parents
* its a binary search tree because binary seach can be preformed on ity
* * every left child is smaller than the root every right child is bigger or equal

```c
typedef struct node
{
    int number;
    struct node* left;
    struct node* right;
} node;
```
* if a search tree isn't balanced it can devolve into a linked list ie if the root is the smallest value and each child is bigger than its parent its a linked list, which means complexity goes from O(log n) to O(n)(linear time).
* trees can be imported balancing is normally already implemented.

### Hashing
* to bucketise means to put data in certain spots based on some critera eg instead of sorting a deck of cards from scratch sorting it in 4 buckets (one for each color) first. this methode is used to go from an infinte domain to finite range of values
* a Hash function is the algorithm that bucketises the data into eg a Hash table
* ideally the Hash function sorts the data in a way that every value has its own key
* Collisions occur when two datapoints are identified by the same key eg sorting name by first letter and having more than one that starts with "A", then inside the a-bucket searching becomes linear O(n) again
* without Collisions creation and searching are in constant time O(1)

#### Hash table
* a Hash table technically is an array of pointers to first nodes of, if there is more than one value per key, a linked list

#### Tries
* trees of arrays
* always true constant time O(1), take a big amount Memory
* an example would be storing names in a tree of arrays where each array has 26 spaces allocated for each potential letter and the tree has as many levels as the longest name letters. this would always allow search in constant time O(1) but would take a big amount of memory
  
# CS50x Lecture 6 Python
* Basics not noted since they are in CS50p notes

 ```c
for n in names:
    if name == n:
        Print("found")
        break
else:
    print("not found")
 ```
 * if the Loop is never broken the else statement is invoked 

# CS50x Lecture 7 SQL
* SQL Structured Query Language

## flat-file Database
* consists of just one table in a simple text format like csv

```c
import csv

# Open CSV file
with open("favorites.csv", "r") as file:

    # Create reader
    reader = csv.reader(file)

    # Skip header row
    next(reader)

    # Iterate over CSV file, printing each favorite
    for row in reader:
        print(row[1])

```
## relational Databases
* stores more complex data and allows to relate datapoints to each other

## sqLite3
* part of the python standart Lib(preinstalled)
* Import sqlite3
  ```sql
  in Terminal

  $ sqlite3 Database_name.db - creates and/ or activates db
  sqlite> .mode csv
  sqlite> .import filename table_name - creates table from file in active db
  sqlite> .schema -shows the schema, all existing executed CREATE commands
  ```
* CREATE, INSERT
* SELECT
* UPDATE
* DELETE, DROP

## B-tree
* data structure created by the INDEX keyword that creates a wide tree in memory that speeds up queries immensely 

## race conditions
* an error when a Value gets updated to fast several times, that the most current update process doesn't have the up-to-date Value yet since it's still being updated - leads to incorrect/ insufficient updating/ conflicts
* fix are BEGIN TRANSACTION which executes a bulk a of queries for the same variable, they are either all executed or not at all. this "blocks" the variable for new queries till the first bulk is completely executed and COMMITed.

## SQL injection attacks 
* using eg login forms and giving characters as input that SQL interpretes as for example wildcards or that comments out a part of a condition that checks for the password
* that's why f-strings shouldn't be used in SQL because its easier to inject for example -- that creates comments that with placeholders.
```sql
rows = db.execute(f"SELECT * FROM users WHERE username = '{username}' AND password = '{password}'")
...

translates to

username = malan@harvard.edu'--

rows = db.execute(f"SELECT * FROM users WHERE username = 'malan@harvard.edu'--' AND password = '{password}'") 
which comments out the AND password condition
...

better

rows = db.execute("SELECT * FROM users WHERE username = ? AND password = ?", username, password)
...
```
# CS50x Lecture 8 HTML, CSS, JavaScript
* routers are server that rout information from one place to another
* DNS Domain Name Systems Server translates domain names(like google.com) into ip addresses it also holds an expiration date 
  when this expires the ip has to be looked up again   
  a fully qualified name is the Domain name and the hostname like www.google.com   
  TLD Top Level Domain like .com used to define what kind of website it is   
   .com - commercial .gov - government .org - organisations   
   those can simply be bought nowadays and are no longer real idetifieres   
   TLDs with two letters .us .uk .de are technically county specific but some countries monetise them   
   good examples .ai -Anguilla .tv - Tuvalu .io - Britischen Territoriums im Indischen Ozean
  
## Protocols
IP - internet protocol 
* * ipv4 (ip version 4) #.#.#.# with 0-255 for each # (32 bit/ 4 byte)
* * ipv6 mostly used in industry not in privat computers (128 bit/ 8 byte)
* the Header contains sender and receiver Address and their corresponding Ports and other possible markers or potions
* since sending bigger information is comlicayed data gets fragmented   
    
TCP/ IP
* the TCP keeps track of the fragmented parts sequence numbers
* 

Ports
* is a unique identifier for a specific internet service like mail, streaming etc
* some ports are standardised like 80 for HTTP or 443 for HTTPS
* can be added to the address like this #.#.#.#:80 

DHCP
* dynamic Host configuartion protocol
* gives computer an ip when it boots up 

HTTP / HTTPS
* hypertext transfer protocol / Securtity
* intercommunication between browser and server
* uses eg GET or POST for requests   
  GET / HTTP/2  // 2 version of HTTP  
  Host: www.harvard.edu  
  ...
  response:  
  HTTP/2 200  // 200 is the stauscode 200 means success 301 moved permanently 404 not found  
  300 codes usually means some sort of redirection like 307 temorary redirect, 304 Not modified   
  400 codes indicates User Error 401 Unauthorised, 418 I'm a teapot   
  500 codes are Server errors 500 internal Server Error , 503 Service Unavailable   

  Content-Type: text/html  
  ...
* testing output in Bash
    curl -I http://www.harvard.edu/
    * curl - Client URL
    * -I only requests the headings not the full output
    * needs the fully qualified name or the output will have a 300 code like permanently moved

URL (not a protocol)
* Uniform Resource Locator
* it contains the fully qualified domain name, a trailing slash( often the rest of the path is hidden), protocol on how to handel the query like HTTPS

## HTML
* Hypertext Markup Language
* text file 
* http-server -starts a web server on port 8080
* comments are created with \<!-- Comment -->
```html
<!DOCTYPE html> <!--document type declaration-->

<html lang="en"> <!-- defines the beginning of an html element, defines the Language (title and body) -->
    <head> // 
        <title> <!-- open Tag for the title -->
            hello, title
        </title> <!-- close Tag for the title -->
    </head>
    <body>
        hello, body
    </body>
</html>
```
creates a website that just says "hello, body" on the page and hello, title on the browser Tab
* paragrph tag \<p> text \</p> has to be set after and before each paragraph or tyhere will be no empty lines between them
* headings in the body can be set with \<h1>Header One\</h1> to h3 similar to # ## ### in Markdown 
* can use " and ' similar as in python
* lists ul - unordered list -> bullet points
* li - List item
* ol ordered list - numbered
```html
...
    <body>
        <ul>
            <li>foo</li>
            <li>bar</li>
            <li>baz</li>
        </ul>
    <body>
...
```
* table \<table> ... \</table>
* tr - table row
* td - table data ( cells)
```html
    <body>
        <table>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
            <tr>
                <td>4</td>
                <td>5</td>
                <td>6</td>
            </tr>
        </table>
    </body>
```
* images \<img src="FILENAME.png"> bmp often not supportd by browser; png tiff jiff jpeg are normally supported
* \<img alt="Harvard University" src="FILENAME.png"> alt shows up if the imag or img path is broken it can also be read out with a screen reader
```html
    <body>
        <video controls muted> <!-- controls shows video control buttons like play and stop
                                muted means audio is muted by default -->
            <source src="video.mp4" type="video/mp4">
        </video>
    </body>
```
* links
```html
    <body>
       Visit <a href="https://www.harvard.edu">Harvard</a>. <!-- <a INput>Linktext</a> - anker; href - hyper reference-->
    </body>
```
creates a link to Harvard page on the word Harvard
* relative Link - Link to a file or page in my own port/folder
* external Link - Link to an external page
```html
    <body>
        <form action="https://www.google.com/search" method="get"> <!-- send querey to google server -->
            <input autocomplete="off" autofocus name="q" placeholder="Query" type="search"> <!-- q- query type search gives the option to clear the search box with one click in contrast to "text" autocomplete of as iy says deactivates the autocomplete; autofocus automatically activates the field; placeholder is the text shown in the field if noting is typed in-->
            <input type="submit" value="Google Search"> <!-- submit creates a search button here its named google search-->
        </form>
    </body>
```
* type can also be type="email" to only allow valid email addresses 
* buttons can also be created wit \<button>Buttonname\</button>
* attribute pattern can hold Regexes pattern=".SBP_\d"
* this can easily be overwritten by the dev tool sin a browser and is insufficient for proper format checking

validator.w3.org can be used to validate that html file is up to standart
* html entities &#169 would be the copyright symbol

## CSS
* properties - key value pairs to define stuff like colour
* style (head) \<style>\</style> OR \<link href="styles.css" rel="stylesheet"> the second version allows for the css file to be integrated and not everything in one file
```html
    <body>
        <p style="font-size: large; text-align: center;">
            John Harvard
        </p>
        <p style="font-size: medium; text-align: center;">
            Welcome to my home page!
        </p>
        <p style="font-size: small; text-align: center;">
            Copyright &#169; John Harvard
        </p>
    </body>
```
* the p should be substituted by div since the parts are not paragraphs 
* several parts can be modified by a parent
* semantic tags are usefull to keep an overview like header main footer

```html
    <head>
        <title>css</title>
    </head>
    <body style="text-align: center">
        <header style="font-size: large">
            John Harvard
        </header>
        <main style="font-size: medium">
            Welcome to my home page!
        </main>
        <footer style="font-size: small">
            Copyright &#169; John Harvard
        </footer>
    </body>
```
* HTML should be the structure CSS in a extra file the style 
```CSS
.centered
{
    text-align: center;
}

.large
{
    font-size: large;
}

.medium
{
    font-size: medium;
}

.small
{
    font-size: small;
}
```
or using the \<style> inside the HTML file

```html
<html lang="en">
    <head>
        <style>

            .centered
            {
                text-align: center;
            }

            .large
            {
                font-size: large;
            }

            .medium
            {
                font-size: medium;
            }

            .small
            {
                font-size: small;
            }

        </style>
        <title>css</title>
    </head>
    <body class="centered">
        <header class="large">
            John Harvard
        </header>
        <main class="medium">
            Welcome to my home page!
        </main>
        <footer class="small">
            Copyright &#169; John Harvard
        </footer>
    </body>
</html>
```
* Frameworks - third party code css files
* example would be [bootstrap](https://getbootstrap.com/docs/5.3/getting-started/introduction/)

## JavaScript
* Basics
```JavaScript
if (x < y)
{

}
else if (x > y)
{

}
else
{

}
```
```js
let counter =  0;
counter++;
```
```js
for (let i = 0; i < 3; i++)
{

}

while (true)
{

}
```
* code can be in header in \<script> Code \</script> or better in \<script src="script.js">\</script>
* can sometimes also be included in body if the order matters
Hello World
```HTML
<!DOCTYPE html>

<!-- Demonstrates onsubmit -->

<html lang="en">
    <head>
        <script>

            function greet()
            {
                alert('hello, ' + document.querySelector('#name').value); <!--alert creates a pop up; document is global a global Var in browsers in JS it has the function querySelector lets you select elements by id classes etc value referces to value given to #name -->
            }

        </script>
        <title>hello</title>
    </head>
    <body>
        <form onsubmit="greet(); return false;">
            <input autocomplete="off" autofocus id="name" placeholder="Name" type="text">
            <input type="submit">
        </form>
    </body>
</html>
```
better JS syntax
```js
document.querySelector('form').addEventListener('submit', function(event) { //EventListener listens for input to be submitted as soon as it is the input is registered and the function excecuted form refers to the form object in body in the chunk above
    alert('hello, ' + document.querySelector('#name').value);
    event.preventDefault(); // prevents the standart event for submit (sending the Data to the server)
    });
```
```js
document.addEventListener('DOMContentLoaded', function() { // ensures the whole html file is loaded before the following functions get executed
                document.querySelector('form').addEventListener('submit', function(e) {
                    alert('hello, ' + document.querySelector('#name').value);
                    e.preventDefault();
                });
            })
```



# CS50x Lecture 9 Flask
* needs the code in app.py and the dependencies in requirements.txt
* standart port is 5000 not 8080 as with http directly
* the requirements can be installed with
```bash
pip install -r requirements.txt # -r = requirement file pip will read in all lines one lib per line
```
```python
form flask import Flask

app = Flask(__name__) # checks if the filename is app.py


@app.route("/") # the @ decorator runs the index function as soon as a request ending with / is recieved
def index():
    return "hello, world"
```
```bash
flask run # not running the file with python but directly flask
```

* getting input using the GET methode is accessed through request.args.get
* input from POST is accessed though request.form.get
* In Flask a template is a html file that will be rendered through Flask, it must be in a templates subfolder
```python

from flask import Flask, render_template, request

app = Flask(__name__)


@app.route("/")
def index():
    name = request.args.get("name", "world") # set name either to the input in nameIn or to world
    return render_template("index.html", nameIn=name)
```
with
```html
<!DOCTYPE html>

<html lang="en">

    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>

    <body>
        hello, {{ nameIn }}
    </body>

</html>
```
layout templates can be used in a way where, one file holds all the information that every file needs and the individuals files just fill in a block. it must be in the template folder
```html
<!-- Layout.html -->
<!DOCTYPE html>

<html lang="en">

    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width"> <!-- autofits to screen width -->
        <title>hello</title>
    </head>

    <body>
        {% block body %}{% endblock %}
    </body>

</html>
```
and 
```html
{% extends "layout.html" %}

{% block body %}

    <form action="/greet" method="get">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        <button type="submit">Greet</button>
    </form>

{% endblock %}
```
* by default when creatinga route in flask only GET is supported
    all other methodes must be declared
* request.args.get for input from get
* request.form.get for input from POST
* POST is the standart for sensitive, large data since its not shown in the URL
* the data can be seen in the browser dev tools in Network/Payload 
```python
from flask import Flask, render_template, request

app = Flask(__name__)


@app.route("/", methodes=["POST"])
def index():
    name = request.form.get("name", "world") # set name either to the input in nameIn or to world
    return render_template("index.html", nameIn=name)
```
* with jinja conditionals can be added to templates 
```jinja
{% extends "layout.html" %}

{% block body %}

    hello,
    {% if name %}
        {{name}}
    {% else %}
        world
    {% endif %}

{% endblock %}
```
* client side validation - writing the html in a way that enforces eg all necessary inputs to be required - used to help User to avoid mistakes
* server side validation - writing the script in a way that only valid inputs are registered, defining what's valid in the script not the html site - protects from intentional faulty inputs
``` python
from flask import Flask, render_template, request

app = Flask(__name__)

SPORTS = ["A", "B", "C",] # trailing comma by convention

@app.route("/")
def index():
    return render_template("index.html", sport=SPORTS)

@app.route("/register", methode=["POST"])
def register():
    if request.form.get("sport") not in SPORTS:
        return render_template("error.html", message="Invalid Sport")
    return render_template("success.html")
```
```jinja
{% extends "layout.html" %}

{% block body %}

    <h1>Error</h1> 
    <p>{{ message }}</p>

{% endblock %}
```
* here only input that are valid are registered because their checked against the valid list after input

## designs
* MVC Model View Controller
    * Controller - app.py - Business logic
    * View - everthing in templates folder - everything the User sees/ interacts with
    * Model - Database/ Storage 


# CS50x Lecture 9.5 Cybersecurity
## hashing for passwords
stored for example in Databases passwords should not be stored directly they should be run through a Hashing algorithm and that result stored. in contrast to encryption which should be reversable hashing is not. Hash functions use a mix of mathematical changes that also include bitwise operators like XOR, to really ensure irreversibility even if the whole algorithm is known Modulo is used which completely truncates some of the information everytime its used. there are other factors too, the algorithm ensures that small changes result in completely different outcomes, all inputs get a fixed length output independent of the input length and more.

## rainbow table
a Table where a Hash table is created in advance with common passwords and the corresponding Hashes. would take up a massive amount of space with longer passwords.

## salting
adding some "salt" to the password that is unique for the user to the input for the hashing algorithm. This makes it impossible to infere which useres might have the same passwords from the Hashes.

## Cryptography
### symmetric cryptography
encryption and decryption work with the same algorithm and one key can encrypt and reverse the process, like the Caesar cipher from Lecture 2.

### asymmetric cryptography
encryption is done with a public key while for decryption a private key is used. These key have mathematical relations but are not inferrable from each other. This is ensured with the public key being derived from the private one with a one-way function (like hashing).

## passkeys
are credentials that are based on public and private key pairs, they allow password free login. The website server has the public key as reference for your account and if you try to login the website sends a challenge to your device that with your private key creates a digital signature which can be verified with the public key.

## end-to-end encryption
is a way encrypting communication in a way where the service provider can't see a decrypted version of the communication only the two intended parties.