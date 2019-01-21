# Notes on C course

## No strings in C
C only has arrays of chars with null terminators
ie:
```
char str[] = "hello";
char str2[] = "hello\0";
char str3[] = "hello\0 good bye";
str == str2 // true because \0 null terminator is auto added to end of string
str == str3 // true because \0 null terminator will stop any chars after being saved
```

### ways to declare string
```
char str1[] = "hello";
```
str1 value is the address of the start of the array
ie:
pointer=
address: 2349
value: "h"
string=
address: 2349
value: "h"

**NOTE:** in this example the pointer var and the actual var occupy the same space in memory
**NOTE:** strings only ever point to the first char in the string, the end is noted with a \0 null terminator

this sytle of initializing also wont let you re-assign
ie:
str1 = "new" // will fail

```
char *str2 = "Goodbye";
```
str2 is a pointer (number - value of which is a memory address) that points to the space in memory where the string starts
ie:
pointer=
address: 1929
value: 2349
string=
address: 2349
value: "h"

**NOTE:** in this example the pointer points to the address where the value lies

:. if you use str1 style, it will create a pointer automatically for you

can re-assign with this syntax
ie:
str2 = "new" // this will work fine

## #define
#define PI 3.14
this works like a substitution (preprocessor), can be redefined
const int PI = 3.14
this is a true constant that can not be redefined

## gets()
this function will grab any and all characters passed
this is unsafe
ie:
```
car name[5]; // declare a string of 5 chars
gets(name); // get input from user and store in 'name'
```
if the user inputs more that 4 characters then you will have issues

**NOTE:** the ``` car name[5] ``` can only hold 4 chars as the last is reserved for the null termination char ``` \0 ```

## fgets()
this is much safer
ie:
```
car name[5];
fgets(name, 5, stdin); // will only get the first 4 chars + null terminator
```

## strings v chars
'x' is a char litteral (a memory location of the value)
"x" is a string, it will iterate through till it finds a \0
for chars use ''
for strings use ""

## assignment

need to use strspy to assign a new string name ie
strcpy(some[0].name, "new_name");

integer or char can be assigned normally
some[1].age = 4;
some[1].group = 'b';

## issues with prompts
Need to flush the input if using several prompts
when user inputs data, that data is temporarily stored in memory
the next prompt for fgets will look to this temorary stack
ie: name input = 123456789
firstname=1234
lastname=5678
still in memory buffer=9
  - the second prompt for the last name reads from the buffer
the way around this is to flush the buffer between prompts

|flush_example|

## stack
the stack is memory used to keep variables and functions alive 
all the variables are removed from the stack once you have exited from that function

to keep variables around after exiting a function, it is not enough just to return the value
you must also use global memory for value by using malloc

## heap
the heap is more persistant than the stack memory, variables defined in here will persist after a function exits
when using malloc you should clear out the memory
s = malloc(20) // create space in the heap (20 bytes)
s[0] = 0; // clear out the memory, this is manditory (or you will append to random bytes), this is the same as using a null char


## C11
most compilers support C11 which has many 'safer' functions, ie string functions that all end in '_s'

## Structs and Typedefs
### struct creation
```
struct cd {
  char name[];
  char artist[];
  int raiting;
}
```
### struct instantiation
```
struct cd my_cd;
struct cd my_cd_colleciton[4]; // 4 cd collection
```
### typedef creation
```
typedef struct cd CD; // assuming cd struct is declared
// or altogether
typedef struct cd {} CD;
typedef struct cd {
  char name[];
  char artist[];
  int raiting;
} CD;

```
### typedef instantiation
CD new_cd;
CD new_collection[4];

## enums

