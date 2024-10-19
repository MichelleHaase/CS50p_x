# CS50
## Week1 C
### Basics
* Vars need to be declared
* semicolons on the line end
* %s as placeholder for content of Var (%s= string, %i=int, %f=float, )
* make Filename (without filetype ending) to build
* ./Filename (without filetype ending)  to run
* Datatypes(most common):
* * bool ; char; double; float; int; long; string
* for strings ""    for chars ''
* logical or || ; logical and &&
* increment ++ decrement --


```{c}
#include <stdio.h>
#include <cs50.h>

int main(void)
{
    string answer= get_string("Whats your name? ");
    printf("hello, %s\n", answer);
}
```
### Loops
#### while Loops

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

#### for Loops
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
### writing functions
* return_Value function_Name(Input)
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