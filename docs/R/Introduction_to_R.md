

# Introduction to R

## 1. Basics

### a. Comments
In R programming `#` is used to comment a code. If a particular line is commented in a script, when the script is executed, anything after a `#` will be ignored. There is no separate multi-line (a block comment) comments unlike other languages like HTML, SQL, JavaScript, Java etc.
```r
#Calculate 5 + 7
```
### b. Arithmetic
R can be used as a simple calculator. Consider the following arithmetic operators.

- Addition: `+`
- Subtraction: `-`
- Multiplication: `*`
- Division: `/`
- Exponentiation: `^`
- Modulo: `%%` - This returns the remainder of the division by left side of the number to the right side of the number. Eg. `10 %% 3` return 1 as a remainder.

### c. Variable Assignment
 A variable allows you to store a value. The value can be accessed later with the variable name. There are two assignment operator in R. They are `<-` and `=`. The main difference between these two assignment operator is the scope of their variable. More info is [here](https://www.r-bloggers.com/assignment-operators-in-r-%E2%80%98%E2%80%99-vs-%E2%80%98-%E2%80%99/).

### d. Basic data types in R

1. Numerics (eg. 1.5)
2. Integers (eg. 1) - Integers also a numerics in R
3. Logical (TRUE,  FALSE)
4. Characters ("string values") - single or double quotation marks should be wrapped around the string.

#### What is a datatype?
To identify the datatype of a variable you can use `class()` function.
```r
    x <- 1.5
    class(x)
    #> [1] "numeric"

    x <- 1
    class(x)
    #> [1] "numeric"

    #Uppercase L should be suffixed with the number to assign integer datatype.
    x <- 1L
    class(x)
    #> [1] "integer"

    #Both TRUE and T means logical True. It should be in uppercase as R is a case sensitive.
    x <- TRUE
    class(x)
    #> [1] "logical"


    x <- T
    class(x)
    #> [1] "logical"

    x <- 'some text'
    class(x)
    #> [1] "character"

    x <- "Isn't it?"
    class(x)
    #> [1] "character"

    x <- 'She said, "It is great"'
    class(x)
    #> [1] "character"

    x <- 'She said, "It\'s great"'
    class(x)
    #> [1] "character"

    x <- "She said, \"Wow\""
    class(x)
    #> [1] "character"
```

  ---

## 2. Vectors
Vector is a **one dimensional array** and it  can hold numeric, character or logical values. The elements in a vector all have the same data type.

### a. Create a vector
A vector can be created using combine function `c()`. The elements or values of a vector should be separated by a comma `,`.  The index of a first element of a vector is 1 not 0 as in many other programming languages (eg. Python, C, etc).

For example.
``` r
x <- c("Ett", "Två", "Tre", "Fyra")
class(x)
#> [1] "character"

x <- c(1, 2, 15.5)
class(x)
#> [1] "numeric"

x <- c(FALSE, F, TRUE, T)
class(x)
#> [1] "logical"

x <- c(1L, 5L)
class(x)
#> [1] "integer"

x <- c(1L, 5)
class(x)
#> [1] "numeric"

x <- c("1", "2", "3", 4) #Numeric value 4 is converted to character "4".
class(x)
#> [1] "character"

x <- c("FALSE", T) #Logical value T is converted to character.
class(x)
#> [1] "character"

x <- c("FALSE", True)
#> Error in eval(expr, envir, enclos): object 'True' not found
class(x)
#> [1] "character"
```
Vector can also be created using sequence `seq` function. `seq(1:4)` creates a vector of c(1, 2, 3, 4).

### b. Naming a vector
`names()` - To assign or get the names of each element of a vector.
```r
x <- c("Norway", "Oslo")
names(x) <- c("Country", "Capital")
names(x)
#> [1] "Country" "Capital"
```
### c. Calculation
If you sum two vectors in R, it takes the element-wise sum. The first element of vector 1 will be added with the first element of vector 2 and so on.
```r
vector_1 <- c(1, 2, 3)
vector_2 <- c(6, 8, 10)

vector_1 + vector_2
#> [1]  7 10 13
vector_1 - vector_2
#> [1] -5 -6 -7
vector_1 * vector_2
#> [1]  6 16 30
vector_2 / vector_1
#> [1] 6.000000 4.000000 3.333333
vector_2 %% vector_1
#> [1] 0 0 1
vector_2 > vector_1
#> [1] TRUE TRUE TRUE
```
### d. Vector selection
You can select only a few elements of a vector instead of all the elements.
#### Selection by element number
To filter the first element of a vector you type `vector_name[1]`. To select multiple elements from a vector, you have to pass a numeric vector with the indexes of the elements you wish to select. For example, if you want to select 2nd, 3rd and 4th element of a vector, you have to create a vector of these indexes. Then pass this newly created vector to filter the original vector. `vector_name[c(2,3,4)]`. There is an another way to do the same task. You can use a range instead of listing out all the sequential element index. `vector_name[2:4]`. The part `2:4` internally creates a vector `c(2, 3, 4)`. So either way works fine.

```r
virat <- c(24, 56, 0, 78, 243)
rohit <- c(59, 12, 24, 262, 75)

element_name <- c("innings_1", "innings_2", "innings_3", "innings_4", "innings_5")
names(virat) <- element_name
names(rohit) <- element_name

rohit[1]
#> innings_1
#>        59
rohit[c(3,4,5)]
#> innings_3 innings_4 innings_5
#>        24       262        75
rohit[3:5]
#> innings_3 innings_4 innings_5
#>        24       262        75
```

#### Selection by element name
Another way to select the vector element is by using the element name itself instead of element number.
```r
virat <- c(24, 56, 0, 78, 243)
rohit <- c(59, 12, 24, 262, 75)

element_name <- c("innings_1", "innings_2", "innings_3", "innings_4", "innings_5")
names(virat) <- element_name
names(rohit) <- element_name

virat["innings_2"] #selection by element name
#> innings_2
#>        56
virat[c("innings_3", "innings_4", "innings_5")] #selection by element names and there is no range selector.
#> innings_3 innings_4 innings_5
#>         0        78       243
```
#### Selection by comparison
Let's compare Virat and Rohit's runs for each innings.
```r
virat <- c(24, 56, 0, 78, 243)
rohit <- c(59, 12, 24, 262, 75)

element_name <- c("innings_1", "innings_2", "innings_3", "innings_4", "innings_5")
names(virat) <- element_name
names(rohit) <- element_name

virat[virat>50] #Virat's 50+ runs
#> innings_2 innings_4 innings_5
#>        56        78       243
virat[rohit>=100] #Virat's runs when rohit scored 100+
#> innings_4
#>        78
virat[virat>rohit] #Virat's runs when virat scored more than rohit
#> innings_2 innings_5
#>        56       243
rohit[rohit>virat] #rohit's runs when rohit scored more than virat.
#> innings_1 innings_3 innings_4
#>        59        24       262
rohit[virat!=rohit] #rohit's runs when they did not score equal runs.
#> innings_1 innings_2 innings_3 innings_4 innings_5
#>        59        12        24       262        75
```
Few more examples:
```r
countries <- c("GBR", "IND", "AUS", "SWE", "NOR", "FIN", "CAN", "KSA")
selection <- c("IND", "FIN") #using elements name
countries[countries==selection]
#automatically selection vector's length is replicated based on the countries vector length.
#> [1] "FIN"

selection <- c(2, 4, 6) #using position
countries[selection]
#> [1] "IND" "SWE" "FIN"

selection <- c(T, F) #using logical value
countries[selection]
#> [1] "GBR" "AUS" "NOR" "CAN"

selection <- c(-3, -7, -1) #using negative index
countries[selection]
#> [1] "IND" "SWE" "NOR" "FIN" "KSA"
```
---

## 3. Matrices
A matrix is a **two dimensional array** and it can hold numeric, character or logical values. The elements in a matrix all have the same data type.

A matrix can be created using a built in function `matrix()`. Let's see the below example.

### a. Matrix construction
There are several ways to construct a matrix. When you construct a matrix with data elements, by default it will be filled along the columns. The default value of `byrow` parameter in matrix function is `FALSE`. So it should be changed to true if the data to be filled by row wise in matrix.
```r
x <- matrix(
  data = seq(1,9), #data elements of this matrix
  nrow = 3, #desired number of rows
  ncol = 3, #desired number of columns.
  byrow = TRUE #fill the data elements by row.
)

print(x)
#>      [,1] [,2] [,3]
#> [1,]    1    2    3
#> [2,]    4    5    6
#> [3,]    7    8    9
```
#### Combining matrices
##### cbind() and rbind()
```r
x <- c(1, 2, 3)
y <- c(8, 9, 10)

cbind(x, y)
#>      x  y
#> [1,] 1  8
#> [2,] 2  9
#> [3,] 3 10
rbind(x, y)
#>   [,1] [,2] [,3]
#> x    1    2    3
#> y    8    9   10
```
Deparse level in rbind and cbind:
The parameter controls how the row and column name is constructed. The default value is 1.

```r
#Deparse.level
d <- 3
rbind(10:12, b = 1, "c++" = 2, d, deparse.level = 0)
#>     [,1] [,2] [,3]
#>       10   11   12
#> b      1    1    1
#> c++    2    2    2
#>        3    3    3
rbind(10:12, b = 1, "c++" = 2, d, deparse.level = 1) #deparse.level = 1 is the default
#>     [,1] [,2] [,3]
#>       10   11   12
#> b      1    1    1
#> c++    2    2    2
#> d      3    3    3
rbind(10:12, b = 1, "c++" = 2, d, deparse.level = 2)
#>       [,1] [,2] [,3]
#> 10:12   10   11   12
#> b        1    1    1
#> c++      2    2    2
#> d        3    3    3
```

### b. Matrix deconstruction
Interestingly matrix can be deconstructed to vector (one dimension) using the combine function `c()`.
```r
x <- matrix(
  data = seq(1,9), #data elements of this matrix
  nrow = 3, #desired number of rows
  ncol = 3, #desired number of columns.
  byrow = TRUE #fill the data elements by row.
)

print(x)
#>      [,1] [,2] [,3]
#> [1,]    1    2    3
#> [2,]    4    5    6
#> [3,]    7    8    9

print(c(x)) #deconstruct the matrix
#> [1] 1 4 7 2 5 8 3 6 9
```

### c. Matrix selection

- Just like vector, we can use square brackets `[ ]` to select one or more elements from a matrix.
- As matrix is a **two dimension**, we should specify row and column detail also. It should be separated by comma `,`.
- If all the row or column should be selected, the respective value can be empty before or after the comma. But comma is mandatory.

```r
x[2,] #select entire 2nd row
#> [1] 4 5 6
x[,3] #select entire 3rd column
#> [1] 3 6 9
x[2,3] #select the data element at 2nd row and 3rd column.
#> [1] 6
x[c(1,2),] #select only 1st and 2nd rows
#>      [,1] [,2] [,3]
#> [1,]    1    2    3
#> [2,]    4    5    6
x[c(-3),] #select all the rows but 3rd row.
#>      [,1] [,2] [,3]
#> [1,]    1    2    3
#> [2,]    4    5    6
x[,c(1:2)] #select all the rows and 2nd and 3rd column.
#>      [,1] [,2]
#> [1,]    1    2
#> [2,]    4    5
#> [3,]    7    8
x[c(2,3), c(2,3)] #select 2nd and 3rd rows and 2nd and 3rd columns.
#>      [,1] [,2]
#> [1,]    5    6
#> [2,]    8    9
x[2:3, 2:3] #select 2nd and 3rd rows and 2nd and 3rd columns.
#>      [,1] [,2]
#> [1,]    5    6
#> [2,]    8    9
```
### d. Useful functions
Operator / Function | Description
:--------------------|:------------
X * Y | Element-wise matrix multiplication
t(X) | Transpose of a matrix.
rbind(X,Y) | Row bind. It's similar to union all in SQL. Combine matrices vertically and returns a matrix.
cbind(X,Y) | Column bind. It's similar to join in SQL. Combine matrices horizontally and returns a matrix.
rowMeans(X) | Returns vector of row means.
rowSums(X) | Returns vector of row sums.
colMeans(X) | Returns vector of column means.
colSums(X) | Returns vector of column sums.
rownames(X) | Set row names of the matrix.
colnames(X) | Set column/field names of the matrix.
dimnames(X) | This function is used to set both row names and col names to a matrix. A list with row names and column name should be passed. Ex. `dimnames(X) < - list(c('A','B'), c('X', 'Y'))`
---
## 4. Factors

---
## 5. Dataframe
A data frame is a **two dimensional objects** and it can hold numeric, character or logical values. Within a column all elements have the same data type, but different columns can be of different data type.

---
## 6. Lists
A list in R allows you to gather a variety of objects under one name (i.e, the name of the list) in an ordered way. The object can be vectors, matrices, data frame and even other lists. The length of the objects can be different. List is kind of a super datatype and you can practically store any information on it.

### a. Create a list
`list()`

#### Create a named list

### b. List Selection

### c. Add a new object to list



## 7. Conditionals and Control flow
### a. Relational operators
### b. Logical operators

It's important to note that the `else if` keywords comes on the same line as the closing bracket of the previous part of the control construct.

:white_check_mark: Correct: :point_down:
```r
if (condition1) {
  expr1
} else if (condition2) {
  expr2
} else (condition3) {
  expr3
}
```
 :x: Incorrect: :point_down:
```r
if (condition1) {
  expr1
}
else if (condition2) {
  expr2
}
else (condition3) {
  expr3
}
```

### c. Conditional statements

## 8. Loops :loop:
### a. While loop
### b. For loop
#### Loops over a Vector

#### Loops over a Matrix
#### Loops over a List
#### break
The `break` statement quit the current active loop: the remaining code in the loop is skipped and the loop is not iterated over anymore.
#### next
The `next` statement skips the remainder of the code in the loop, but continues the iteration.

## 9. Functions
### a. Introductions
-> default value
-> argument required or optional
### b. Writing function
-> function with and without arguments
-> function with default argument value
-> function scoping
-->  The variables that are defined inside a function are not accessible outside that function.
```r
square_function <- function(x) {
  y <- x ^ 2
  return(y)
}
square_function(10)
#> [1] 100

print(x)
#> Error in print(x): object 'x' not found
print(y)
#> Error in print(y): object 'y' not found
```

### c. Calling a function
#### Arguments matching by position
#### Arguments matching by name
#### R passes arguments *by value* not *by reference*
R function cannot change the variable that you input to that function.
```r
square_function <- function(x) {
  x <- x ^ 2
  return(x)
}

x <- 5
square_function(x) #the value of x is passed to the function (not reference).
#> [1] 25
print(x) #input value can not be changed by the function
#> [1] 5
```

### d. R packages
* `install.packages()` - To install a new R packages from [CRAN](https://cran.r-project.org/).
* `library()` which loads (i.e. attaches them to the search list) packages in R workspace.  To install packages, you need administrator privileges.
* `search()`, to look at the currently attached packages in R workspace.

#### Different ways to load a package
library
require
attach?


## 10. The apply family
### a. Why apply functions?
***FOR LOOP vs APPLY
### b. apply

### c. lapply

- apply function over a list or vector
- output is always a list 
- ( `l` in the `lapply` denotes list?)

#### lapply with built-in R function
#### lapply with User defined function
#### lapply with anonymous R function
#### lapply with agruments

### d. sapply

- apply function over a list or vector
- **try to simplify** the output to array (vector or matrix). If not possible, output will be a list. This is quite dangerous if we program assuming the output will be a vector or matrix.
- *** (`s` in the `sapply` denotes simplify lapply?)
- `sapply(*, simplify = FALSE, USE.NAMES = FALSE)` is equivalent to `lapply(*)`.

```r
# 1. Return a list with `lapply()`
lapply(MyList,"[", 2, 1 )

# 2. Return a list with `sapply()`
sapply(MyList,"[", 2, 1, simplify=F)

# 3. Return a vector with `sapply()`
sapply(MyList,"[", 2, 1 )

# 4. Return a vector with `unlist()`
unlist(lapply(MyList,"[", 2, 1 ))
```
#### sapply with built-in R function
#### sapply with User defined function
#### sapply with anonymous R function
#### sapply with agruments
#### sapply with functions that returns null

### e. vapply

- apply function over a list or vector
- output format is **explicitly specified**.
- Syntax: `vapply(X, FUN, FUN.VALUE, ..., USE.NAMES = T)`
- Example: `vapply(states, nchar, numeric(1))`
- The benefit of setting this new argument `FUN.VALUE` is if we expect `character(2)` (i.e, character with length 2)  as a output of a function and the function returns anything other than specified, it throws an error. So we can fix it.
- `vapply` is safer than `sapply` if you want to simplify the result of `lapply`. `vapply` is a robust version of `sapply`. So, it is a good practice to use `vapply` in your R scripts.
### f. rapply 
rapply is a recursive version of lapply.
### g. by?

## 11. Utilities
### a. Useful functions

Functions | Description | Example
--- | --- | ---
 order() ||
sort() |(asc/desc) argument `decreasing = T` is a default value. 
identical() ||
abs() ||
round() ||
 seq() ||
rep() |Replicates elements of vector or list. Arguments: `times` and `each`|`rep(vector_x, each = 2)`
append() ||
rev() ||
is.*() ||
as.*() ||
unlist() |To convert from a list to a vector|
which() ||

### b. Regular expressions
- sequence of *meta*characters. i.e, `. \ | ( ) [ { ^ $ * + ?`
- pattern existence
- pattern replacement
- pattern extraction
- Very useful when you clean your data

`grep`, `grepl`, `regexpr`, `gregexpr` and `regexec` search for matches to argument pattern within each element of a character vector: they differ in the *format of* and *amount of detail* in the results.

- The strings in pattern should be enclosed by double quotes `""`.
- `"^a"` - Starts with `a`
- `"a$"` - Ends with `a`
- `"a|e|i|o|u"` - The pipe `|` symbol is for logical OR operation.
- `.*` - Any characters that matched zero (`.`) or more (`*`) times.
- `\\` To escape any meta character, you have to use double back slash.
- `\\s` - To match a space.
- `[0-9]+` - To match the number 0 to 9, at least once (+).
- `([0-9]+)` - The parentheses are used to make parts of the matching string available to define the replacement. The `\\1` in the replacement argument of `sub()` gets set to the string that is captured by the regular expression `[0-9]+`.
```r
token <- c("Token 2A", "Tkn 7B", "Number 3")
sub(pattern=".*\\s([0-9]+).*$", replacement ="\\1", x = token)
#> [1] "2" "7" "3"
```


#### grep() and grepl()
- `grep` , which returns a vector of indices of the character strings that contains the pattern.
- `grepl`, which returns TRUE when a pattern is found in the corresponding character string.
- `grepl(pattern = <regex>, x = <string>)` where pattern is a regular expression and x is a character vector.
```r
states <- c("Karnataka", "Tamil Nadu", "Kerala", "Assam", "Andhra Pradesh")

grep(pattern = "a$", x = states)
#> [1] 1 3 5
grepl(pattern = "a$", x = states)
#> [1]  TRUE FALSE  TRUE FALSE  TRUE
which(grepl(pattern = "a$", x = states))
#> [1] 1 3 5
```


#### sub() gsub()
`sub` and `gsub` perform replacement of the first and all matches respectively.
`sub(pattern = <regex>, replacement = <string>, x = <character vector>)`



### c. Time :hourglass: and Date :date:
#### Sys.Date() and Sys.time()
```r
thedhi <- Sys.Date()
class(thedhi)

neram <- Sys.time()
class(neram)
```


#### Useful R packages

- lubridate
- zoo
- xts
