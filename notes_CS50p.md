# CS50p Lecture 0 Functions and Variables notes

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

# CS50p Lecture 1 Conditionals

* < > <= >= == !=
* := Walross operator used to check conditional and assign value at the same time

## if elif else
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

# CS50p Lecture 2 Loops
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
# CS50p Lecture 3 Exceptions
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

# CS50p Lecture 4 Libraries
* modul/ Libraries has features and function made for reusability
```
import random

coin= random.choice(["heads","tails"])
#print(coin)

from random import choice # this way only the function choice() is importet
# so the random modul doesnt need to be called. The Scope of the choice() 
# is on one level with the built-in one and can overwrite them and my own

coin2= choice(["heads","tails"])
print(coin2)

cards= ["a","b","c"]
random.shuffle(cards)
for card in cards:
    print(card)

import statistics

statistics.mean([100,90])
```
sys.argv (stands for argument Vector) is var that automatically creates 
a list out of all the inputs given
```
import sys

print("Hello, my name is", sys.argv[1])
```
when the programm is startet with "python Filename.py" sperated with space, the input is given without prompt "python Filename.py Michelle"
which leads to the output "Hello, my name is Michelle" at index 0 is
"Filename.py" 
if no argument is given a IndexError is arises because index 1 of 
sys.arg is NA

```
import sys

if len(sys.argv) < 2:
    print("missing Arguments")
elif len(sys.argv) > 2:
    print("Too many Arguments")
else:
    print("Hello my name is", sys.argv[1])
``` 
if the conditionals should be checked, exited when True but continued 
when false instead of having the rest of the code inside an else 
statement sys.exit("exit message") can terminate the program early,
it actually terminates the program not just ie a Loop like break
```
import sys

if len(sys.argv) < 2:
    sys.exit("missing Arguments")
elif len(sys.argv) > 2:
    sys.exit("Too many Arguments")

print("Hello my name is", sys.argv[1])
```
to for example printing out several Name Tags
```
import sys

if len(sys.argv) < 2:
    sys.exit("missing Arguments")

for arg in sys.argv[1:]:
    print("Hello my name is", arg)
```
* packages third party Libraries
* API Application Program interface, "requests" Lib allows to make
  requests as if made by a Browser
* JSON Javascript object notation files, text based 
```
import requests
import json
import sys

if len(sys.argv) !=2:
    sys.exit()

response= requests.get("https://itunes.apple.com/search?entity=song&limit=1&term=" + sys.argv[1])
print(json.dumps(response.json(), indent=2))
```
to iterate over the output Dict to ie to print all track names for a 
artist

```
...
response= requests.get("https://itunes.apple.com/search?entity=song&limit=50&term=" + sys.argv[1])
object1= response.json()

for results in object1["results"]:
    print(results["trackName"])
```
## writing own Modul
```
in File: test_Modul.py

def main():
    hello("world")
    goodbye("Lala")

def hello(name):
    print(f"hello, {name}")

def goodbye(name):
    print(f"Goodbye, {name}")

main()

in File Filename.py:

from test_Modul import hello
hello(sys.argv[1])
```
if written this way even if just one function is imported main() is
called. with the " if __name__ == "__main__":" this is avoided since 
main can only be called if the Script is executed directly, because 
 __name__ is only __main__ when the script is run from the 
 command line

 # CS50p Lecture 5 Unit tests
 * by convention test_Filename.py
 * import functions to test
 * by convention "def test_functionname():"
 * format stuff to PEP8 conventions with black (pip install)

example_file:
 ```{python}
def main():
    x = int(input())
    print ("x squared is", square(x))

def square(n):
    return n * n

if __name__ == "__main__":
    main()

 ```
  * "assert" only throws errors when test fails --> AssertionError
 test_example_file:

 ```{python}
from example_file import square

def main():
    test_square()

def test_square():
    try:
        assert square(2) == 4
    except AssertionError:
        print("2 squared was not 4")
    try:
        assert square(3) == 9
    except AssertionError:
        print("3 squared was not 9")
    try:
        assert square(-2) == 4
    except AssertionError:
        print("-2 squared was not 4")
    try:
        assert square(-3) == 9
    except AssertionError:
        print("-3 squared was not 9")
    try:
        assert square(0) == 0
    except AssertionError:
        print("0 squared was not 0")
    

if __name__ == "__main__":
    main()
 ```
## pytest 
* is a 3rd party modul that takes a test as below and runs test accordingly without
  needing to use exceptions and puts out a overview.
* it also holds a number of functions like pytest.raises(ErrorType) that allow to test 
  negative of error cases
* if a several Test file should be run in the folder with the test files must be file 
  called __innit__.py to indicate the folder as a package ( a collection of Modules)
  "pytest Test_folder_name" runs all possible test s in the folder
* for testing floats since rounding errors can be expected, "pytest.approx(expected_result)"
  "pytest.approx(expected_result, abs= 0.1)" abs defines the tolerance
   
```
import pytest

from example_file import square


def test_positive():
    assert square(2) == 4
    assert square(3) == 9

def test_negative():
    assert square(-2) == 4
    assert square(-3) == 9

def test_zero():
    assert square(0) == 0

def test_string():
    with pytest.raises(TypeError):
        square("")
```
### function without return value can't be tested properly

so example file
```
def main():
    name= input("Name? ")
    hello(name)

def hello(to="world"):
    print("hello," to)

if __name__ "__main__":
    main()

```
should look like this 

```
def main():
    name= input("Name? ")
    print(hello(name))

def hello(to="world"):
    return f"hello, {to}"

if __name__ == "__main__":
    main()

```
and a test would look like
```
from testingstuff import hello


def test_argument():
    assert hello("David") == "hello, David"
    
def test_default():
    assert hello() == "hello, world"
```
# CS50p Lecture 6 File I/O
* saving information in Stored memory?? 
* "w"- writing recreating the file every time
* "a" - appending to the file, no line breaks included
* "r" - reading a txt file (default)

```
file = open("names.txt", "a")
file.write(f"{name\n"})
file.close()
==
with open("names.txt", "a") as file:
    file.write(f"{name\n"})

# omits file.close
```
```
with open("names.txt", "r") as file:
  for line in file:
      print(line.rstrip()) 
# rstrip strips the extra \n one from the input one from print

```
```
names= []

with open("names.txt") as file:
  for line in sorted(file):
      names.append(line.rstrip()) 
```
```
with open("names.csv") as file:
    for line in file:
        row = line.rstrip().split(",")

students = []

with open("names.csv") as file:
    for line in file:
        name, house = line.rstrip().split(",")
        student = {"name": name, "house" : house}
        students.append(student)

def get_name(student):
    return Student["name"]

for student in sorted(students, key=get_name):
    print(f"{student['name']}, {student['house']}")
==
for student in sorted(students, key=lambda student: student["name"]):
    print(f"{student['name']}, {student['house']}")
```
* lambda (anonyms) functions can be used when a function is only used once

```
import csv

students = []

with open("names.csv") as file:
    reader = csv.reader(file)
    for name, home in reader:
        students.append({"name": name, "home" : home})

for student in sorted(students, key=lambda student: student["name"]):
    print(f"{student['name']}, {student['home']}")

# with column headers
with open("names.csv") as file:
    reader = csv.Dictreader(file)
    for row in reader:
    students.append({"name": row["name"], "home" : row["home"]})

#writing to csv file
with open("students.csv", "a") as file:
    writer = csv.writer(file)
    writer.writerow([name. home])

#writing a dict to csv
with open("students.csv", "a") as file:
    writer = csv.DictWiter(file, fieldnames=["name", "home"])
    writer.writerow({"name": name, "home" : home})
```
### for binary files there are differnt Libraries eg Pillow
```
import sys

from PIL import Image

images = []

for arg in sys.argv:
    image = Image.open(arg)
    images.append(image)

images[0].save(
    "costumes.gif", save_all=True, append_images=[images[1]], duration=200, loop=0
)
```

# CS50p Lecture 7 Regex

* if Var ie a var holding a string if Var evaluates to True if its not empty
```
if Var:
    print("yes")
else:
    print("no")
```
* re library
* . - any char except newline
* * - 0 or more repetitions
* + - 1 or more repetitions
* ? - 0 or 1 repetition
* {m} - m repetitions
* {m,n} - m-n repetitions
* ^ - matches the start o f the string (Anker)
* $ - matches end of string or end before newline (Anker)
* [] - set of chars, a-z and 0-9 are predified ranges
* [^] - complementing set eg not any of these chars
* \w - any word character [a-zA-Z0-9_]; \W not a word character
* \d - decimal digit; \D not a decimal digit; 
* \s whitespace
* A|B A or B
* (...) () groups stuff
* (?:...) (?:) not capturing in .group
* escaping chars - raw string means not to interpret any backslashes as in \n for new line
  eg r".*\.\*\+" would be any at least one char then a . a * ending in +
* flags include re.IGNORECASE re.MULTILINE re.DOTALL
* f strings can be used in Regex fr""
* (?P<ExampleName>) - naming groups
```
import re

email = input()

if re.search(r"^(\w|\.)+@(\w+\.)+.{2.3}$", email, re.IGNORECASE): # not a final solution
    print("Valid")
else:
    print("invalid")
```
```
import re

name  = input.strip()

if matches := re.search(r"^(.+), *(.+)$", name):
#    last = matches.group(1)
#    first = matches.group(2)
    name  = matches.group(2) + " " + matches.group(1)
```
```
import re

url = input().strip()
username = re.sub(r"^(https?://)?(www\.)?twitter\.com/", "", url) # substitutes the beginning of link
print(f"Username: {username}")

url = input().strip()
 if username := re.search(r"^(?:https?://)?(?:www\.)?twitter\.com/(\w)+$", "", url, re.IGNORECASE):
    print(f"Username: {username(1)}")

== groups can be named

url = input().strip()
 if username := re.search(r"^(?:https?://)?(?:www\.)?twitter\.com/(?P<username>\w)+$", "", url, re.IGNORECASE):
    print(f"Username: {username(username)}")
```