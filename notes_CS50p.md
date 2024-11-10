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
# CS50p Lecture 8 object-oriented programming
* own Datattypes(objects) are created with classes
* keyword "class" names are capitalized by conmvention
* classes have atributes acessed by .
* class - definition of new Dataype
* object - instance of class
* atributes are tecnically instance variables
* self gives access to the object at creation
* __init__ initializes an empty object when first created
* by setting a input as None in the Initialization it becommes optional
    def __init__(self, name, house=None):
* __str__
```
class Student:
    ...

def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    student = Student()
    student.name = input("Name ")
    student.house = input("House ")
    return student
    
```
```
class Student:
    def __init__(self, name, house):
        self.name = name
        self.house = house

def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    name = input("Name ")
    house = input("House ")
    student = Student(name, house)
    return student
```
```
class Student:
    def __init__(self, name, house):
        if not name:
            raise ValueError("Missing name")
        if house not in ["Griffindor", "Huffelpuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid House")
        self.name = name
        self.house = house

def main():
    student = get_student()
    print(f"{student.name} from {student.house}")


def get_student():
    name = input("Name ")
    house = input("House ")
    try:
        return Student(name, house)
    except ValueError:
        main()
```
```
class Student:
    def __init__(self, name, house, patronus):
        if not name:
            raise ValueError("Missing name")
        if house not in ["Griffindor", "Huffelpuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid House")
        self.name = name
        self.house = house
        self.patronus = patronus
    def __str__(self):
        return f"{self.name} from {self.house}"
    
    def charm(self):
        match self.patronus:
            case "Stag":
                return "🦌"
            case "Otter":
                return "🦦"
            case "Dog":
                return "🐶"
            case _:
                return "🪄"

def main():
    student = get_student()
    print("Expecto Patronum")
    print(student.charm())
    print(student)


def get_student():
    name = input("Name ")
    house = input("House ")
    patronus = input("patronus ")
    try:
        return Student(name, house, patronus)
    except ValueError:
        ...
    
main()
```
* properties 
* decorators TODO 
* a setter will always be called if student.house = is called
  even in the __init__, which measn the error checking only needs to be in the setter
* instance variables in functions can not have the same name as the function
  like self.house and def house() so by convention if there is a function like a setter 
  for a instance variable the variable is named with a leading _ like _house
  keeping the name self.house in __init__ ensures that the setter with the error check is called
* function insde of class -> methode

```

class Student:
    def __init__(self, name, house):
        if not name:
            raise ValueError("Missing name")
        self.name = name
        self.house = house
    def __str__(self):
        return f"{self.name} from {self.house}"
    # getter
    @property
    def house(self):
        return self._house
    # setter
    @house.setter
    def house(self, house):
        if house not in ["Griffindor", "Huffelpuff", "Ravenclaw", "Slytherin"]:
            raise ValueError("Invalid House")
        self._house = house
    

def main():
    student = get_student()
    print(student)


def get_student():
    name = input("Name ")
    house = input("House ")
    return Student(name, house)

    
main()
```
```
import random

class Hat:
    def __init__(self):
        self.houses = ["Griffindor", "Huffelpuff", "Ravenclaw", "Slytherin"]

    def sort(self, name):
        print(name,"is in", random.choice(self.houses))

hat= Hat()
hat.sort("Harry")
```
*class methodes are defined with the decorator @classmethod
```
import random

class Hat:
    houses = ["Griffindor", "Huffelpuff", "Ravenclaw", "Slytherin"]

    @classmethod
    def sort(cls, name):
        print(name,"is in", random.choice(cls.houses))

Hat.sort("Harry")
```
* classes are used to bundel function in topics so all student related
  functions should be in the class student
* inheritance allows subclasses to acsess functions from a superclass
  its initialized by putting the superclass in the prototype of the subclass and callintg super().function_to_be_used(Var? to be used)
  class Professor(Wizard):
  
```
class Wizard:
    def __init__(self, name):
        if not name:
            raise ValueError("Missing Name")
        self.name = name

class Student(Wizard):
    def __init__(self, name, house):
        super().__init__(name)
        self.house = house

class Prodfessor(Wizard):
    def __init__(self, name, subject):
        super().__init__(name)
        self.subject = subject


if __name__ == "__main__":
    main()
```
* operator overloading, different functions for opperators based on Datatype
```
class Vault:
    def __init__(self, galleons=0, sickels=0, knuts=0): # all function in class have acsses to those vars
        self.galleons = galleons
        self.sickels = sickels
        self.knuts = knuts
    
    def __str__(self): # called everytime print is called
        return f"{self.galleons} Galleons, {self.sickels} Sickels, {self.knuts} Knuts"

    def __add__(self, other):
        galleons = self.galleons + other.galleons
        sickels = self.sickels + other.sickels
        knuts = self.knuts + other.knuts
        return Vault(galleons, sickels, knuts)
        
potter = Vault(100, 50, 25)
print(potter)

weasly = Vault(25, 50, 100)
print(weasly)

total = potter + weasly
print(total)
```
## instance methodes / magic methodes
TODO

# CS50p Lecture 9 Et Cetera

## Sets
* duplicates get eliminated at casting
* not sorted but sortable

## global
* changes the Scope of a Variable to global but keeps it changeable
* you cant change a gloabal function inside a function only read it
* 
```
balance = 0

def main():
    deposit(100)
    withdraw(50)
    print(balance)

def deposit(n):
    balance += n

def withdraw(n):
    balance -= n
```
* causes unbound Local error because the global Var balance cant be change inside of deposit
```
def main():
    balance = 0
    deposit(100)
    withdraw(50)
    print(balance)

def deposit(n):
    balance += n

def withdraw(n):
    balance -= n
```
* causes unbound local Error because balance is only accessable in main
```
balance = 0

def main():
    deposit(100)
    withdraw(50)
    print(balance)

def deposit(n):
    global balace
    balance += n

def withdraw(n):
    global balance
    balance -= n
```
* this makes it accessable and changeable
* better change would be a class since all function in a class can access instance Vars
```
class Account:
    def __init__(self):
        self._balance = 0
    
    @property
    def balance(self):
        return self._balance
    
    def deposit(self,n):
        self._balance += n

    def withdraw(self,n):
        self._balance -= n

def main():
    account = Account()
```
## constants 
* in Python constants arent inforced its good practice to write constant Var names in all Caps to indicate theyre
  constants but they are changeable
* constants should be declared at the  top of the script 
* numbers that are randomly hardcoded ie in Loops should be constants
* same goes inside classes constants for Vars declare above __init__(vars accessable to all functions, not depedent on call)

## type Hints
* type hints are not supported py python it self the modul mypy is needed
* pip intall mypy
* excecute code with mypy filename
* the modul is made to self check code not force types
* "n: int" tells mypy the input in the function should be a int
```
def meow(n: int):
    for _ in range(n):
        print("meow")

number = input("Number: ")
meow(number)
==
number: int = input("Number: ")
meow(number)
```
output: error: Argument 1 to "meow" has incompatible type "str"; expected "int"  [arg-type]
```
def meow(n: int) -> None:
    for _ in range(n):
        print("meow")

number = int(input("Number: "))
meows: str = meow(number)
print(meows)
```
* -> None implicates that the function doesnt have a return Value can indicate str| int oä
## Docstrings
* """comment """ are used for documentation of code
* Docstrings can be used to create documentation (like a pdf) by using the markdown "restructured text"
```
def meow(n: int) -> str:
    """
    Meows n times.

    :param n: Number of times to Meow
    :type n: int
    :raise TypeError: If n is not a int
    :return: str of n meows, one per line
    :rtype: str
    """
    return "meow\n" *n
```
## argparse
```
import argparse

parser =argparse.ArgumentParser(description="Meow like a cat")
parser.add_argument("-n", default=1, help="number of times to meow", type=int) # type = int, is a actual type cast
args = parser.parse_args()

for _ in range(args.n):
    print("meow")
```
* allows for arguments to be entered (commandline) in random order copared to sys.argv
* creating a argument like that allows to easy access documentatiopn with "python filename --help" (commandline)
  outpurt would be:
```
usage: testingstuff.py [-h] [-n N]

Meow like a cat

options:
  -h, --help  show this help message and exit
  -n N        number of times to meow
```
## unpacking

