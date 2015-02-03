## Functions
In C++, there are basically three types of functions: arithmetic functions, relational functions, and logical functions.

### ➠ Arithmetic Functions
These types of functions are your basic math functions and are used in conjunction with numeric data values and variables (int, double, float). It is important to remember that order of operations does apply to these functions.

You should be able to recognize these functions as you have used them since elementary school. The only one that you may not be familiar with is the modulus function, which divides two numbers together and returns the remainder. This function is commonly used in true-false statements or loops to recognize when a numerical variable being analyzed is positive or negative or a multiple of a certain number.  Parentheses are used like in algebra to say which operations should be done first if those actions differ from the default order of operations.

In programming, it is also quite often to use variables in conjunction with arithmetic functions. To use variables in this way, all you need to do is use the variable’s defined name where numbers would usually be used. It’s the same as basic algebra.

| Sign | Meaning |
| -- | -- |
| + | Addition |
| - |Subtraction |
| / | Division |
| * | Multiplication |
| % | Modulus |
| = | Assignment Operator |
| ( operator here ) | Parenthesis (order of operation) |
| ++/-- | Increment/decrement numeric value by 1 |

```c++
main()
{
  	int a = 5;
  	int b = 10;
  	int c = a + b;
  	int d = c * a;
  	int e = a(3 + b);
  	int f = b % 2;
  	a++;
}
```
`int a` is assigned the value 5 and `int b` is assigned the value 10. `int c`, is the sum of a and b. Because `a` and `b` are assigned the value 5 and 10, respectively, `c` is currently at `a` value 15. It can be subject to change in the event the values `a` and b change. `int d` is the product of `c` and `a`, (15*5). int `e` is the product of `a` and the sum of `3+b`. `int f` is the remainder of `b` divided by 2 (it will return `a` value of either 0 or 1).

### ➠ Relational Operators
Relational operators are used to determine whether two numbers are equal, or whether one is greater or less than the other. Every relational expression returns either 1(true) or 0 (false). These operators are used in statements (if, else, while) in order to create expressions that set conditions for that code inside the statement. Be sure not to confuse the assignment operator (=) with the relation operator of equality (==).

| Name | Operator | Sample | Evaluation |
| -- | -- | -- | -- |
| Equals | == | `100==50;` | false |
|  | | `50==50;` | true |
| Not Equals | != | `100!=50;` | true |
|  | | `50!=50;` | false |
| Greater than | > | `100>50;` | true |
|  | | `50>50;` | false |
| Greater than or equals | >= | `100>=40;` | true |
|  | | `50>=50;`| true |
| Less than | < | `100<50` | false |
| | | `50<50;` | false |
| Less than or equals | <= | `100<=50` | false |
|  | | `50<=50` | true |

###➠ Logical Operators
Logical operators are used in conjunction with relational operators to create more complex statement expressions.

| OPERATOR | SYMBOL | EXAMPLE |
| -- | :--: | -- |
| AND | `&&` | 2:2 |
| OR | ([2 pipes](http://en.wikipedia.org/wiki/Vertical_bar)) | 2:3 |
| NOT | `!` | 2:4 |

A logical AND statement evaluates two expressions, and if both expressions are true, the logical AND statement is true as well.

A logical OR statement also evaluates two expressions. If either or both are true, the entire expression is true.

A NOT statement compares whether a condition is NOT what is stated (i.e. switches the return value from true to false and vice versa).

When using logical operators to form statements, make sure you use parentheses to make the order of precedence clearer to the compiler to avoid any errors. For example,
```c++
if( x > 5 && y > 5 || z > 5)
```
This statement goes to show how ambiguous these statements can get if parentheses are not used.  Do you want the statement to return true if x > 5 and y>5 or when just z >5, or did you want the statement to return true when x>5 and when either y>5 or z>5? If you wanted the latter, then you should rewrite the statement to make things clearer:
```c++
if((x > 5 && y > 5) || z > 5)
```
