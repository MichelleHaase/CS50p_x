# CS50p Functions and Variables notes

* __cli__ - command line interface
* start from Terminal - python Filename.py
* don't forget comments singleLine # multi """ """
* __pseudocode__ - comments + todo's
## functions with example print()
auto inserts whitespace, linebreak at the en dand space between komma seperated 
Arguments (only komma seperated + concatanats strings and therefore doesn't insert 
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
print(f"{Number:.2f}")--prints Var Number(float) with two positions after decimalpoint .
print(f"{Number:,}")-- makes a , after every third number (usually . in Ger)
```


## String methodes
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
2nd exanmple default output is hello world, with input in name ist hello {name}
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