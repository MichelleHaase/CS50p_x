# CS50p Functions and Variables notes

* __cli__ - command line interface
* start from Terminal - python Filename.py
* don't forget comments singleLine # multi """ """
* __pseudocode__ - comments + todo's
## functions with example print()
auto inserts whitespace, line break at the end and space between comma separated 
Arguments (only comma separated + concatenates strings and therefore doesn't insert 
whitespace)
parameters like sep='' and end='' can be overwritten when using the function like


```
print("this is text", end='\t')
```
the escape Character \ can be used to print Characters that would normally be interpreted as code eg
```
print("this is \"literally\" text")
```
f-strings allow to see certain parts inside of "" as code
```
print(f"this is text and {Variable}")

print(f"{Number:.2f}")--prints Var Number(float) with two positions after decimal point .

print(f"{Number:,}")-- makes a , after every third number (usually . in Ger)

print("meow" * 3, end="") -- multiplies print statements eg printing it 3 times

```


## String methods
### strip()
removes Whitespace from the beginning and the end of str
```
inputText = inputText.strip()
```
### capitalize ()
capitalizes the first word of a str !!! British spelling doesn't work !!!
```
inputText = inputText.capitalize()
```
### title()
Capitalises each word in the str
```
inputText = inputText.title()
```

### split()
splits str by separator if the result is saved in as many Vars as there are str pieces it's saved as str if there are more pieces that Vars error, if everything saved in one Var it's a list

```
inputText = inputText.split(" ")
```

## documentation

parameters v arguments
potential thing that could be used as shown in Documentation are parameters.
Arguments are the things actually used when using the function.
*objects means all types of objects can be used

## math operators
 \+ - * / %(modulo) **(power of)
## casting
int() str() float() 

## writing  functions
def - define
2nd example default output is hello world, with input in name ist hello {name}
```
def hello():
    print("hello")

def hello(to="world"):
    print("hello", to)
name=input("Whats your name? ")
hello(name)
```
* side effect everything that gets changed while function is running that is not 
the return Value eg print to console
## Scope
a scope of a Var describes where the Var is defined  eg globally or inside a 
function

## keywords
* return, returns value without Var for example from inside a function
* global makes a global Var not just accessible but changeable inside a function

# CS50p Lecture 2 Conditionals

* < > <= >= == !=

* if elif else
syntax :    
```
            if conditionals:
                code
            elif conditional:
                code
            else:
                code
```
you can use parentheses but they're not necessary

* or and 
```
if 90 <= Var and Var <= 100:
elif 80 <= Var and Var < 90:
    ==
if 90 <= Var <= 100:
elif 80 <= Var < 90:
    == assuming its between 0 and 100
if Var >= 90:
elif Var >= 80:
```
elif is essential here, since two if statements are not exclusive they both would be answered

* math operators + - * / %(modulo)
modulo syntax:if Var % 2 == 0 -> all even nums would be True
```
def is_even(n):
    if n % 2 == 0:
        return True
    else:
        return False
# can be condensed to

def is_even(n):
    return True if n % 2 == 0 else return False
# and further condensed to since modulo == 0 is boolean expression it self

def is_even(n):
    return n % 2 == 0
```
* case match statement
Syntax: 
```
match Var:
            case "one" | "three" | "four":      # | being a logical or
                print()
            case "two":
                print()
            case _:     #default
                print()
```
 no break or default needed case _: is optional

# CS50p Lecture 3 Loops
## while Loops

```
i=0
while i < 3:
    print()
    i+=1

while True:
    n= int(input("What's n? "))
    if n > 0:
        break
```
## For Loops
iterates over list of items
if the idx is only needed for the Loops and not used its 
costum to name it _
```
for _ in range(3):
    print()

for i in List:
    print(i)

for i in range(len(List)):
    print(i + 1, List[i]) -- prints the ranking and the contents together
```
## dicts
define absence of a Value with None


```
students =
{
    "Key": "Value",
    "Studemt2": "Huffelpuff",
    "Studemt3": "Griffindor",
    "Studemt4": "Ravenclaw",
    "Studemt5": "Griffindor",
    
}
Values can be accessed by print(students["Studemt2"]) --> Huffelpuff
or by usiung .get print(students.get("Studemt2", "Alternative Print if no Value given))

Dicts can be extended by students.update({new Key/ Value pairs})
```
# CS50p Lecture 4 Exceptions
* Syntax Errors always need fixing to run code
* Runtime Errors need extra code to cover edge cases, like promted Input
  is not provided at all
* Value Error eg giving the wrong Datatype to a function
* Name Error often when using Var that's not defined

```
while True:
    try:
        x= int(input("What's x? "))
    except ValueError:  # "ValueError" is case-sensitive
        print("given Input is not an integer")
    else: 
        break
    
print(f"x is {X}")

# with try the code tries to execute the given code, if a Value Error arises for example
# if a str is given to int() it executes the except statement, if the right input is 
# given and no Value Error raised the else is executed the Loop breaks and the Programm
# continues, here the Print statement

while True:
    try:
        x= int(input("What's x? "))
        break                       # since this line is only executed if try succeeds the 
                                    # break can be introduced here, to shorten the Programm
    except ValueError: 
        print("given Input is not an integer")

print(f"x is {X}")

def get_int():
    while True:
        try:
            x= int(input("What's x? "))
        except ValueError:  
            print("given Input is not an integer")
        else: 
            return x
# return automatically breaks the loop because it terminates the whole function
# except also takes pass as code and with that just skips the Error Message and continues the Loop

except ValueError:
    pass
```
* VSCode comes with a debugger marking the line next to the line number, clicking it until
  it's red marks the Line as a breakpoint which means when running the script with the debugger
  the execution pauses on the breakpoint line and gives the option to over or into the code 
  step by step