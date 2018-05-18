
## Why would I want to mix C++ and R?
C++ is a statically-typed general purpose programming language that is typically compiled. Programs that are written in C++ execute quickly and the language has extensive libraries so many standard algorithms are easy to find and deploy. When a particular calculation is bottlenecking your code in R, it sometimes makes sense to rewrite the performance-critical snippets in C++.

## Incorporating C++ into R with Rcpp
The best way to incorporate C++ into R, is to use [Rcpp](http://www.rcpp.org/). This powerful API allows R to interface with C++. Rcpp (stands for "R and C plus plus") can be downloaded as a package for R. It integrates easily with Rstudio allowing your to rewrite the slow portions of your code in C++ without disrupting your workflow.

## Short Example: Writing a C++ function for R

Let's write a function to convert Celsius to Fahrenheit in C++ and use it in R.

```r

library(Rcpp)
# make sure to declare the datatype you are returning with C++
cppFunction(
'double convert_temp(double celsius) 
{
  double fahrenheit = (celsius * 9.0) / 5.0 + 32;
  return fahrenheit;
}'
  )
# we can treat convert_temp like an R function now
convert_temp(30.0)

```
```
> convert_temp(30.0)
[1] 86
> convert_temp(20)
[1] 68
> convert_temp(-20)
[1] -4
```
## Short Example: Using C++ functions from a source file

1) Create a new C++ file

In Rstudio, go to > **New File** and choose **C++ file** (extension .cpp).

2) Add the Rcpp header file and the Rcpp namespace to the C++ file


```cpp
#include <Rcpp.h>
#include <cmath>
using namespace Rcpp;
```
* **#include \<Rcpp.h\>** : This is a preprocessor directive. We can tell because it begins with a # sign. These directives are processed before the code compiles. In this case, we are telling the program to include the Rcpp.h header file before we begin to do anything else. This header file allows the functions in our program to work with R.
 
* **#include \<cmath\>** : This is also a preprocessor directive. This header file gives us access to a library with math functions.


* **using namespace Rcpp**: In this statement, we declare Rcpp as the default namespace used in this program. Doing this prevents name collisions (two libraries using the same name for different commands).


3) Add function with an export statement

```cpp
// [[Rcpp::export]]
double take_sqrt(double number) {
  // sqrt() is a library function to calculate square root
  double squareRoot = sqrt(number);
  return squareRoot;
}

```
Note that if the *// [[Rcpp::export]]* statement is not in front of your function, you will not be able to use it in an R session.
If you cannot get the export to work, check that you have left a space between the double forward slashes and the double
brackets.

The full C++ source file should look like this: 

```cpp
#include <Rcpp.h>
#include <cmath>
using namespace Rcpp;

// [[Rcpp::export]]
double take_sqrt(double number) {
  // sqrt() is a library function to calculate square root
  double squareRoot = sqrt(number);
  return squareRoot;
}

```
4) execute the function in an R session

Use the function *sourceCpp()* from the Rcpp package to compile the source.
Now you can use the function you wrote in C++.

```shell
> sourceCpp(file ="~/PetGit/myrsandbox/Cfile.cpp")
> take_sqrt(9)
[1] 3
> 
```

## Other resources

* [Introduction to the basics of C++ for Novices](https://www.ntu.edu.sg/home/ehchua/programming/cpp/cp0_Introduction.html)
* [Intuitive C++ Tutorial](https://www.programiz.com/cpp-programming/arrays)
* [Introduction to the Rcpp package](http://adv-r.had.co.nz/Rcpp.html)
* [Using Rcpp with Rstudio](http://www.mjdenny.com/Rcpp_Intro.html)
* [Examples of how to write Rcpp packages](https://support.rstudio.com/hc/en-us/articles/200486088-Using-Rcpp-with-RStudio)
* [Benchmarking R function vs C++ function](https://www.r-bloggers.com/another-nice-rcpp-example/)




