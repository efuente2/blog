---
title: C++ For Beginners
date: 2025-02-20 15:26:39
tags:
---
## Intro

This is my attempt to learn and document C++, While following the text: "C++ Program Design 
An Introduction To Programming and Object-Oriented Design" 

## Prerequisite  

My Current Set up :

- Windows 11
- [Vs Code (with C++ Extensions Enabled)](https://code.visualstudio.com/)
- [C++ Compiler](https://winlibs.com/)

## Hello World
 ``` cpp
    #include <iostream>
    #include <string>
    using namespace std;
    int main() {
        cout << "Hello, World!" << endl;
        return 0;
    }
```

- The top 3 lines will start almost all programs in C++
``` cpp
    #include <iostream>
    #include <string>
    using namespace std;
```
- This shows that program will use the iostream library to do inputs and outputs.
- Line 1 and 2 are know as a preprocessor which are programs that run before the compiler.
- Line 3 Indicates that the program will be using objects that are named in a special region called std

```cpp 
    int main()
```
- Line 4 is know as a function which specifies the return value 
- The main method is the first function that is called when the program is compiled and executed. 
- The Word "Int" indicates the return type I this case Int is Integer. in C++ the main method will always return and int. 
- The word "main" is the name of the method
- The () are used to delimit any arguments, in this case the main method does not require arguments. 
- The { } group together statements, and in this case this these statements make up the function. 

```cpp
    cout << "Hello, World!" << endl;
    return 0;
```
- The first statement starts with cout which is an object that indicates an output stream
- The << inserts a element in this case to the output stream 
- Following this we have "Hello World" this is out output string that would display when the program is run.
- Then the end of the first statement is end with endl this is know as a manipulator and this indicates a new line. 
- The second statement "return 0;" would be returned by the main method, a zero indicates that the program ran without issues. 
- A non zero output would mean that there was some error with the execution of the method.


## User Inputs
```cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    // cout << "Hello, World!" << endl;  
    cout << "Purchase price ?";
    float Price;
    cin >> Price;

    //compute the output sales tax
    cout << "Sales tax on $" << Price << " is ";
    cout << "$" << Price * 0.04 << endl;
    return 0;
}
```

- The following ask the user for the input to calculate the sales tax of a purchase.

``` cpp
float Price;
```
- Here im creating a variable that will store the Price as a **floating point** number. 
- this is because the expected input could be a number with a decimal place (ex. 5.99).

``` cpp 
cin >> Price;
```
- Cin is an object like cout, however Cin is an input stream 
- The users input value is converted to the internal format for floating point number and stores in the Price object.

```cpp
    cout << "Sales tax on $" << Price << " is ";
    cout << "$" << Price * 0.04 << endl;
```
- The last statements will output the price then followed by the calculated sales tax. 

## Comments

- Comments is a mechanism that allows programmers to add prose or comments in code 
- Comments are ignored by the compiler, generally used to describe what a piece of code is doing. 

``` cpp
// Here is a comment that span one line 
/* This a comment that can span 
MULTIPLE

LINES

*/
```

## Objects 

# H1 Integer
- In C++ the basic integer type is called an **int** 
- The compiler and underling hardware determine the size of int 
    - for example most pc support size of 16 bits, where int can represent integers from -32768 - 32768
    - for unix it would be 32 bits and newer system can support up to 64 bit integers. 
- There are also several other integer object types like **short** and **long** 
    - C++ does not determine the size of **short** or **long** however it does specfy the following:
        *NumberOfBits<sub>short</sub>* $\leq$ *NumberOfBits<sub>int</sub>* $\leq$ *NumberOfBits<sub>long</sub>*