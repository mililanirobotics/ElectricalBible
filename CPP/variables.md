## Variables
A variable is a location in the computer’s memory which allows you to store a value which can later be received. Variables are assigned names, which allow you to quickly and easily access the location in memory where the variable’s data is stored without having to know the actual memory address.

When you define a variable, you must also declare the data type of that variable. The datatype of the variable determines what kind of data the variable is holding as well as how much memory must be set aside for that variable. An example of a data type would be an integer which is declared with the ‘int’ command. Integer variables store whole number values.

Different data types require a different amount of memory, but since the use of C++ in this competition does not require you to know the details to data type memory it will not be reviewed in this section.

The tables to follow were adapted from *Sams Teach Yourself C++ in 24 Hours*.

| VARIABLE TYPES | VALUES |
| -------------- | ------ |
| unsigned short integer | 0 to 65,535 |
| short integer | -32,768 to 32,767 |
| unsigned long integer | 0 to 4,294,967,295 |
| long integer | -2,147,483,648 to 2,147,483,647 |
| integer | -2,147,483,648 to 2,147,483,647 |
| unsigned integer | 0 to 4,294,967,295 |
| long long | -9.2 quintillion to 9.2 quintillion |
| char | 256 character values |
| boolean | true or false |
| float | 1.2e-38 to 3.4e38 |
| double | 2.2e-308 to 1.8e308 |

### ➠ Defining Variables
Defining a variable is very easy. Generally, the format for defining a variable is the data type followed by the name you want to assign your variable followed by a semicolon.

```c++
int theExample;
bool iAmAmazing;
```
You must remember that there are rules and guidelines to naming variables. Among programmers, there is proper naming etiquette which allows someone who is reading your code to easily understand why you named a variable a certain way. Here is a list of rules and guidelines to follow to successfully name a variable:

**Rules:**
1. Variable names can be made with any combination of letters

2. Variable names cannot contain spaces, symbols, or punctuation marks

3. Variable names may include underscores

4. Variable names cannot begin with a number but may contain a number elsewhere 	in the name

5. Variable names cannot be the same as reserved keywords. See below table for a 	complete listing of reserved words.

6. C++ is case sensitive so keep this in mind while naming variables (int myInt refers to a different location than int MyInt or int myint)

**Guidelines: **
1. Constants are usually written in all caps

2. Variables are usually started with lower case and if a name contains more than one word, the first letter of the next word is capitalized (eg: int thisIsAnExample)

3. Variables should be named something the describes what the variable is going to be used for

4. Avoid giving variables long names, it is okay to abbreviate long words

**Reserved Words (C++)**

```c++
alignas (since C++11)
alignof (since C++11)
and
and_eq
asm
auto(changed in c++11)
bitand
bitor
bool
break
case
catch
char
char16_t (since C++11)
char32_t (since C++11)
class
compl
const
constexpr (since C++11)
const_cast
continue
decltype (since C++11)
default (changed in C++11)
delete (changed in C++11)
do
double
dynamic_cast
else
enum
explicit
export(1)
extern
false
float
for
friend
goto
if
inline
int
long
mutable
namespace
new
noexcept (since C++11)
not
not_eq
nullptr (since C++11)
operator
or
or_eq
private
protected
public
register
reinterpret_cast
return
short
signed
sizeof
static
static_assert (since C++11)
static_cast
struct
switch
template
this
thread_local (since C++11)
throw
true
try
typedef
typeid
typename
union
unsigned
using(1)
virtual
void
volatile
wchar_t
while
xor
xor_eq
```
*Adapted from [cppreference.com](cppreference.com)*

Below is an example of how to define variables in the C++ language:
```c++
main()
{
 	int a;
 	int ohMyLord;
 	char myChar;
}
```
To define more than one variable of the same data type, you can use the comma punctuation.
```c++
main()
{
 	int a, b, c;
 	char ohMahGlob, lumpySpacePrincess, partyTime;
 	bool downLieToMe, cats;
}
```
###➠ Instantiating
Instantiating a variable is also known as assigning a variable with a value. The operator used to assign values to a variable is the equals sign, (=).

The variable that the data is being assigned to is always on the left side, while the data that is being assigned to the variable is on the right.  It is important to not mix this up because variables can also be assigned values from similar variable types. This is common while using math functions with other variables.

```c++
main()
{
 	int a = 5;
 	int b = 10;
 	int c = a;
 	char character = ‘A’;
 	bool counter = true;
}
```
### ➠ Constants
Sometimes in programming, we have variables with data that we do not want to change at all. Although you could easily just not change the variable data, it is safer to declare a constant variable. A constant variable is a variable that cannot be changed once it is instantiated.

```c++
main()
{
 	const int THIS_IS_A_CONSTANT = 100;
}
```
