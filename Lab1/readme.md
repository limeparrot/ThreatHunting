---
"Лабораторная работа №1"
Сысоев Г.А.
---
## Цель работы

Научиться пользоваться RStudio, изучить язык R, решить задачи из swirl

## Ход работы

## Задание 1: Basic Building Blocks


### In its simplest form, R can be used as an interactive calculator. Type 5 + 7 and press | Enter.

In its simplest form, R can be used as an interactive calculator. Type 5 + 7 and press Enter.
```{r}
5+7
```
[1] 12

To assign the result of 5 + 7 to a new variable called x, you type x <- 5 + 7. This can be read as 'x gets 5 plus 7'. Give it a try now.
```{r}
x <- 5+7
```
To view the contents of the variable x, just type x and press Enter. Try it now.
```{r}
x
```
[1] 12

ow, store the result of x - 3 in a new variable called y.
```{r}
y <- x-3
```
What is the value of y? Type y to find out.
```{r}
y
```
[1] 9


The easiest way to create a vector is with the c() function, which stands for 'concatenate' or 'combine'. To create a vector containing the numbers 1.1, 9,
| and 3.14, type c(1.1, 9, 3.14). Try it now and store the result in a variable called z.
```{r}
 z <- c(1.1, 9, 3.14)
```

Type ?c and press Enter. This will bring up the help file for the c() function.
```{r}
?c
```

You can combine vectors to make a new vector. Create a new vector that contains z, 555, then z again in that order. Don't assign this vector to a new
| variable, so that we can just see the result immediately.
```{r}
c(z, 555, z)
```
[1]   1.10   9.00   3.14 555.00   1.10   9.00   3.14


Numeric vectors can be used in arithmetic expressions. Type the following to see what happens: z * 2 + 100.
```{r}
z*2 + 100
```
[1] 102.20 118.00 106.28

Take the square root of z - 1 and assign it to a new variable called my_sqrt.
```{r}
my_sqrt <- sqrt(z-1)
```
Before we view the contents of the my_sqrt variable, what do you think it contains?

1: a vector of length 0 (i.e. an empty vector)
2: a single number (i.e a vector of length 1)
3: a vector of length 3

Выбор:3

Print the contents of my_sqrt.
```{r}
my_sqrt
```
[1] 0.3162278 2.8284271 1.4628739


Now, create a new variable called my_div that gets the value of z divided by my_sqrt.
```{r}
my_div <- z/my_sqrt
```
Which statement do you think is true?

1: my_div is undefined
2: my_div is a single number (i.e a vector of length 1)
3: The first element of my_div is equal to the first element of z divided by the first element of my_sqrt, and so on...

Выбор:3

Go ahead and print the contents of my_div.
```{r}
my_div
```
[1] 3.478505 3.181981 2.146460


To see another example of how this vector 'recycling' works, try adding c(1, 2, 3, 4) and c(0, 10). Don't worry about saving the result in a new variable.
```{r}
c(1,2,3,4) + c(0,10)
```
[1]  1 12  3 14

Try c(1, 2, 3, 4) + c(0, 10, 100) for an example.
```{r}
c(1,2,3,4) + c(0,10,100)
```
[1]   1  12 103   4

Предупреждение:
В c(1, 2, 3, 4) + c(0, 10, 100) :
  длина большего объекта не является произведением длины меньшего объекта
  
In many programming environments, the up arrow will cycle through previous commands. Try hitting the up arrow on your keyboard until you get to this command
| (z * 2 + 100), then change 100 to 1000 and hit Enter. If the up arrow doesn't work for you, just type the corrected command.
```{r}
z*2 + 1000
```
[1] 1002.20 1018.00 1006.28

Finally, let's pretend you'd like to view the contents of a variable that you created earlier, but you can't seem to remember if you named it my_div or
| myDiv. You could try both and see what works, or...

...my_div

You can type the first two letters of the variable name, then hit the Tab key (possibly more than once). Most programming environments will provide a list of
| variables that you've created that begin with 'my'. This is called auto-completion and can be quite handy when you have many variables in your workspace.
| Give it a try. (If auto-completion doesn't work for you, just type my_div and press Enter.)
```{r}
my_div
```
[1] 3.478505 3.181981 2.146460

Would you like to receive credit for completing this course on Coursera.org?

1: Yes
2: No

Выбор:2



## Задание 2: Workspace and Files

Determine which directory your R session is using as its current working directory using getwd().
```{r}
getwd()
```
[1] "C:/Users/lime/OneDrive/Documents"

List all the objects in your local workspace using ls().
```{r}
ls()
```
[1] "my_div"  "my_sqrt" "x"       "y"       "z"   

Assign 9 to x using x <- 9.
```{r}
x <- 9
```

Now take a look at objects that are in your workspace using ls().
```{r}
ls()
```
[1] "my_div"  "my_sqrt" "x"       "y"       "z"  

List all the files in your working directory using list.files() or dir().
```{r}
dir()
```
 [1] "bos1.pdf"
 [2] "NetDump.zip"                                                       
 [3] "decryptor.exe"                                                                
 [4] "Adobe"
 ...

As we go through this lesson, you should be examining the help page for each new function. Check out the help page for list.files with the command
| ?list.files.
```{r}
?list.files
```

Use the args() function to determine the arguments to list.files().
args(list.files)
function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE, 
    recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE, 
    no.. = FALSE) 
NULL

Assign the value of the current working directory to a variable called "old.dir".
```{r}
old.dir <- getwd()
```
Use dir.create() to create a directory in the current working directory called "testdir".
```{r}
dir.create('testdir')
```
Set your working directory to "testdir" with the setwd() command.
```{r}
setwd('testdir')
```
Create a file in your working directory called "mytest.R" using the file.create() function.
```{r}
file.create('mytest.R')
```
TRUE

This should be the only file in this newly created directory. Let's check this by listing all the files in the current directory.
```{r}
dir()
```
[1] "mytest.R"

Check to see if "mytest.R" exists in the working directory using the file.exists() function.
```{r}
file.exists('mytest.R')
```
[1] TRUE

Access information about the file "mytest.R" by using file.info().
```{r}
file.info('mytest.R')
```
         size isdir mode               mtime               ctime               atime exe
mytest.R    0 FALSE  666 2023-12-16 20:24:47 2023-12-16 20:24:47 2023-12-16 20:24:47  no

Change the name of the file "mytest.R" to "mytest2.R" by using file.rename().
```{r}
file.rename("mytest.R","mytest2.R")
```
[1] TRUE

file.copy("mytest2.R", "mytest3.R") works.
```{r}
file.copy("mytest2.R","mytest3.R")
```
[1] TRUE


Provide the relative path to the file "mytest3.R" by using file.path().
```{r}
file.path('mytest3.R')
```
[1] "mytest3.R"

Give it another try. Or, type info() for more options.

| file.path("folder1", "folder2") works.
```{r}
file.path("folder1","folder2")
```
[1] "folder1/folder2"

| You got it right!

Create a directory in the current working directory called "testdir2" and a subdirectory for it called "testdir3", all in one command by using dir.create()
| and file.path().
```{r}
dir.create(file.path('testdir2', 'testdir3'), recursive = TRUE)
```
Go back to your original working directory using setwd(). (Recall that we created the variable old.dir with the full path for the orginal working directory
| at the start of these questions.)
```{r}
setwd(old.dir)
```

Would you like to receive credit for completing this course on Coursera.org?

1: Yes
2: No

Выбор:2


## Задание 3: Sequences of Numbers

The simplest way to create a sequence of numbers in R is by using the `:` operator. Type 1:20 to see how it works.
```{r}
1:20
```
    [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

 
That gave us every integer between (and including) 1 and 20. We could also use it to create a sequence of real numbers. For example, try pi:10.
```{r}
pi:10
```
[1] 3.141593 4.141593 5.141593 6.141593 7.141593 8.141593 9.141593

What happens if we do 15:1? Give it a try to find out.
```{r}
15:1
```
 [1] 15 14 13 12 11 10  9  8  7  6  5  4  3  2  1
 

| It counted backwards in increments of 1! It's unlikely we'd want this behavior, but nonetheless it's good to know how it could happen.

| Remember that if you have questions about a particular R function, you can access its documentation with a question mark followed by the function name:
| ?function_name_here. However, in the case of an operator like the colon used above, you must enclose the symbol in backticks like this: ?`:`. (NOTE: The
| backtick (`) key is generally located in the top left corner of a keyboard, above the Tab key. If you don't have a backtick key, you can use regular quotes.)

```{r}
?`:`
```
| The most basic use of seq() does exactly the same thing as the `:` operator. Try seq(1, 20) to see this.
```{r}
seq(1,20)
```
[1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

| This gives us the same output as 1:20. However, let's say that instead we want a vector of numbers ranging from 0 to 10, incremented by 0.5. seq(0, 10,
| by=0.5) does just that. Try it out.
```{r}
seq(1,10,0.5)
```
 [1]  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0  7.5  8.0  8.5  9.0  9.5 10.0

| Give it another try. Or, type info() for more options.

| You are still using the seq() function here, but this time with an extra argument that tells R you want to increment your sequence by 0.5. Try seq(0, 10,
| by=0.5).
```{r}
seq(0,10,0.5)
```
 [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0  7.5  8.0  8.5  9.0  9.5 10.0

| Or maybe we don't care what the increment is and we just want a sequence of 30 numbers between 5 and 10. seq(5, 10, length=30) does the trick. Give it a shot
| now and store the result in a new variable called my_seq.
```{r}
my_seq <- seq(5,10,30)
```

| You're using the same function here, but changing its arguments for different results. Be sure to store the result in a new variable called my_seq, like
| this: my_seq <- seq(5, 10, length=30).
```{r}
my_seq <- seq(5,10,length=30)
```
| To confirm that my_seq has length 30, we can use the length() function. Try it now.
```{r}
length(my_seq)
```
 [1] 30


| There are several ways we could do this. One possibility is to combine the `:` operator and the length() function like this: 1:length(my_seq). Give that a
| try.
```{r}
1:length(my_seq)
```
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30


| Another option is to use seq(along.with = my_seq). Give that a try.
```{r}
seq(along.with = my_seq)
```
[1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30


| However, as is the case with many common tasks, R has a separate built-in function for this purpose called seq_along(). Type seq_along(my_seq) to see it in
| action.
```{r}
seq_along(my_seq)
```
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30

| If we're interested in creating a vector that contains 40 zeros, we can use rep(0, times = 40). Try it out.
```{r}
rep(0, times = 40)
```
 [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

| If instead we want our vector to contain 10 repetitions of the vector (0, 1, 2), we can do rep(c(0, 1, 2), times = 10). Go ahead.
```{r}
rep(c(0, 1, 2), times = 10)
```
 [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2

| Finally, let's say that rather than repeating the vector (0, 1, 2) over and over again, we want our vector to contain 10 zeros, then 10 ones, then 10 twos.
| We can do this with the `each` argument. Try rep(c(0, 1, 2), each = 10).
```{r}
rep(c(0, 1, 2), each = 10)
```
 [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2

| Would you like to receive credit for completing this course on Coursera.org?

1: No
2: Yes

Выбор:1

## Задание 4: Vectors
| The simplest and most common data structure in R is the vector.

## Vectors come in two different flavors: atomic vectors and lists. An atomic vector contains exactly one data type, whereas a list may contain multiple data
| types. We'll explore atomic vectors further before we get to lists.

## In previous lessons, we dealt entirely with numeric vectors, which are one type of atomic vector. Other types of atomic vectors include logical, character,
| integer, and complex. In this lesson, we'll take a closer look at logical and character vectors.

## Logical vectors can contain the values TRUE, FALSE, and NA (for 'not available'). These values are generated as the result of logical 'conditions'. Let's
| experiment with some simple conditions.

## First, create a numeric vector num_vect that contains the values 0.5, 55, -10, and 6.
```{r}
num_vect <- c(0.5,55,-10,6)
```
| You're the best!

| Now, create a variable called tf that gets the result of num_vect < 1, which is read as 'num_vect is less than 1'.
```{r}
tf <- num_vect < 1
```
| Nice work!

| What do you think tf will look like?

1: a single logical value
2: a vector of 4 logical values

Выбор:1

| Nice try, but that's not exactly what I was hoping for. Try again.

| Remember our lesson on vector arithmetic? The theme was that R performs many operations on an element-by-element basis. We called these 'vectorized'
| operations.

1: a vector of 4 logical values
2: a single logical value

Выбор:1

| Excellent work!

| Print the contents of tf now.
```{r}
tf
```
[1]  TRUE FALSE  TRUE FALSE

| That's a job well done!

| The statement num_vect < 1 is a condition and tf tells us whether each corresponding element of our numeric vector num_vect satisfies this condition.

## The first element of num_vect is 0.5, which is less than 1 and therefore the statement 0.5 < 1 is TRUE. The second element of num_vect is 55, which is
| greater than 1, so the statement 55 < 1 is FALSE. The same logic applies for the third and fourth elements.

## Let's try another. Type num_vect >= 6 without assigning the result to a new variable.
```{r}
num_vect >= 6
```
[1] FALSE  TRUE FALSE  TRUE

| Excellent work!

| This time, we are asking whether each individual element of num_vect is greater than OR equal to 6. Since only 55 and 6 are greater than or equal to 6, the
| second and fourth elements of the result are TRUE and the first and third elements are FALSE.

## The `<` and `>=` symbols in these examples are called 'logical operators'. Other logical operators include `>`, `<=`, `==` for exact equality, and `!=` for
| inequality.

## If we have two logical expressions, A and B, we can ask whether at least one is TRUE with A | B (logical 'or' a.k.a. 'union') or whether they are both TRUE
| with A & B (logical 'and' a.k.a. 'intersection'). Lastly, !A is the negation of A and is TRUE when A is FALSE and vice versa.

## It's a good idea to spend some time playing around with various combinations of these logical operators until you get comfortable with their use. We'll do a
| few examples here to get you started.

## Try your best to predict the result of each of the following statements. You can use pencil and paper to work them out if it's helpful. If you get stuck,
| just guess and you've got a 50% chance of getting the right answer!

...

| (3>5) & (4 == 4)

1: FALSE
2: TRUE

Выбор:1

| Keep up the great work!

| (TRUE == TRUE) | (TRUE == FALSE)

1: TRUE
2: FALSE

Выбор:1

| You are quite good my friend!

| ((111 >= 111) | !(TRUE)) & ((4 + 1) == 5)

1: FALSE
2: TRUE

Выбор:2

| That's a job well done!

| Don't worry if you found these to be tricky. They're supposed to be. Working with logical statements in R takes practice, but your efforts will be rewarded
| in future lessons (e.g. subsetting and control structures).

## Character vectors are also very common in R. Double quotes are used to distinguish character objects, as in the following example.

## Create a character vector that contains the following words: "My", "name", "is". Remember to enclose each word in its own set of double quotes, so that R
| knows they are character strings. Store the vector in a variable called my_char.
```{r}
my_char <- c("My","name","is")
```
| All that hard work is paying off!

| Print the contents of my_char to see what it looks like.
```{r}
my_char
```
[1] "My"   "name" "is"  

| You nailed it! Good job!

| Right now, my_char is a character vector of length 3. Let's say we want to join the elements of my_char together into one continuous character string (i.e.
| a character vector of length 1). We can do this using the paste() function.

## Type paste(my_char, collapse = " ") now. Make sure there's a space between the double quotes in the `collapse` argument. You'll see why in a second.
```{r}
paste(my_char, callapse = " ")
```
[1] "My  "   "name  " "is  "  

| You almost had it, but not quite. Try again. Or, type info() for more options.

| Use paste(my_char, collapse = " ") to collapse the words in the vector so they almost form a sentence. There should be a single space between the double
| quotes in the `collapse` argument so that there are single spaces separating the words.
```{r}
paste(my_char, collapse = " ")
```
[1] "My name is"

| You got it right!

| The `collapse` argument to the paste() function tells R that when we join together the elements of the my_char character vector, we'd like to separate them
| with single spaces.

## It seems that we're missing something.... Ah, yes! Your name!

## To add (or 'concatenate') your name to the end of my_char, use the c() function like this: c(my_char, "your_name_here"). Place your name in double quotes
| where I've put "your_name_here". Try it now, storing the result in a new variable called my_name.
```{r}
c(my_char, "Ruslan")
```
[1] "My"      "name"    "is"      "Ruslan"

| Not quite! Try again. Or, type info() for more options.

| Tack your name on to the end of the my_char vector using the c() function.  Be sure to assign the result to a new variable called my_name. If your name was
| "Swirl", you would type my_name <- c(my_char, "Swirl").
```{r}
my_name <- c(my_char, "Ruslan")
```
| Keep up the great work!

| Take a look at the contents of my_name.
```{r}
my_name
```
[1] "My"      "name"    "is"      "Ruslan"

| You are quite good my friend!

| Now, use the paste() function once more to join the words in my_name together into a single character string. Don't forget to say collapse = " "!
```{r}
paste(my_name, collapse = " ")
```
[1] "My name is Ruslan"

| You nailed it! Good job!

| In this example, we used the paste() function to collapse the elements of a single character vector. paste() can also be used to join the elements of
| multiple character vectors.

## In the simplest case, we can join two character vectors that are each of length 1 (i.e. join two words). Try paste("Hello", "world!", sep = " "), where the
| `sep` argument tells R that we want to separate the joined elements with a single space.
```{r}
paste("Hello","world!",sep=" ")
```
[1] "Hello world!"

| Excellent job!

| For a slightly more complicated example, we can join two vectors, each of length 3. Use paste() to join the integer vector 1:3 with the character vector
| c("X", "Y", "Z"). This time, use sep = "" to leave no space between the joined elements.
```{r}
paste(c(1:3),c("X","Y",'Z'), sep = "")
```
[1] "1X" "2Y" "3Z"

| That's correct!

| What do you think will happen if our vectors are of different length? (Hint: we talked about this in a previous lesson.)

## Vector recycling! Try paste(LETTERS, 1:4, sep = "-"), where LETTERS is a predefined variable in R containing a character vector of all 26 letters in the
| English alphabet.
```{r}
paste(LETTERS, 1:4, sep="-")
```
 [1] "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4" "M-1" "N-2" "O-3" "P-4" "Q-1" "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4" "Y-1"
[26] "Z-2"

| All that hard work is paying off!

| Since the character vector LETTERS is longer than the numeric vector 1:4, R simply recycles, or repeats, 1:4 until it matches the length of LETTERS.

...


| Also worth noting is that the numeric vector 1:4 gets 'coerced' into a character vector by the paste() function.

...


| We'll discuss coercion in another lesson, but all it really means is that the numbers 1, 2, 3, and 4 in the output above are no longer numbers to R, but
| rather characters "1", "2", "3", and "4".

## Would you like to receive credit for completing this course on Coursera.org?

1: Yes
2: No

Выбор:2

| Excellent job!

## Задание 5: Missing Values

| Any operation involving NA generally yields NA as the result. To illustrate, let's create a vector c(44, NA, 5, NA) and assign it to a variable x.
```{r}
 c(44,NA,5,NA)
```
[1] 44 NA  5 NA

| Give it another try. Or, type info() for more options.

| Assign the vector c(44, NA, 5, NA) to a variable x. The NA must uppercase.
```{r}
x<- c(44,NA,5,NA)
```
| Keep working like that and you'll get there!

| Now, let's multiply x by 3.
```{r}
x*3
```
[1] 132  NA  15  NA

| You are doing so well!

| Notice that the elements of the resulting vector that correspond with the NA values in x are also NA.

## To make things a little more interesting, lets create a vector containing 1000 draws from a standard normal distribution with y <- rnorm(1000).
```{r}
y <- rnorm(1000)
```
| You got it right!

| Next, let's create a vector containing 1000 NAs with z <- rep(NA, 1000).
```{r}
z <- (rep(NA,1000))
```
| That's not exactly what I'm looking for. Try again. Or, type info() for more options.

| Type z <- rep(NA, 1000) to generate a vector of 1000 NAs.
```{r}
z <- rep(NA,1000)
```
| You are doing so well!

| Finally, let's select 100 elements at random from these 2000 values (combining y and z) such that we don't know how many NAs we'll wind up with or what
| positions they'll occupy in our final vector -- my_data <- sample(c(y, z), 100).

```{r}
my_data <- sample(c(y,z),100)
```
| You are doing so well!

| Let's first ask the question of where our NAs are located in our data. The is.na() function tells us whether each element of a vector is NA. Call is.na() on
| my_data and assign the result to my_na.
```{r}
my_na <- is.na(my_data)
```
| You are quite good my friend!

| Now, print my_na to see what you came up with.
```{r}
my_na
```
[1] FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE
 [26] FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE
 [51] FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE
 [76]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE

| That's the answer I was looking for.

| Everywhere you see a TRUE, you know the corresponding element of my_data is NA. Likewise, everywhere you see a FALSE, you know the corresponding element of
| my_data is one of our random draws from the standard normal distribution.

## In our previous discussion of logical operators, we introduced the `==` operator as a method of testing for equality between two objects. So, you might
| think the expression my_data == NA yields the same results as is.na(). Give it a try.
```{r}
my_data == NA
```
[1] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
 [52] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA

| You are amazing!

| The reason you got a vector of all NAs is that NA is not really a value, but just a placeholder for a quantity that is not available. Therefore the logical
| expression is incomplete and R has no choice but to return a vector of the same length as my_data that contains all NAs.

## Don't worry if that's a little confusing. The key takeaway is to be cautious when using logical expressions anytime NAs might creep in, since a single NA
| value can derail the entire thing.

## So, back to the task at hand. Now that we have a vector, my_na, that has a TRUE for every NA and FALSE for every numeric value, we can compute the total
| number of NAs in our data.

## The trick is to recognize that underneath the surface, R represents TRUE as the number 1 and FALSE as the number 0. Therefore, if we take the sum of a bunch
| of TRUEs and FALSEs, we get the total number of TRUEs.

## Let's give that a try here. Call the sum() function on my_na to count the total number of TRUEs in my_na, and thus the total number of NAs in my_data. Don't
| assign the result to a new variable.
```{r}
sum(my_na)
```
[1] 47

| That's the answer I was looking for.

| Pretty cool, huh? Finally, let's take a look at the data to convince ourselves that everything 'adds up'. Print my_data to the console.
```{r}
my_data
```
 [1] -1.50190133          NA          NA  0.89351766 -0.83327373          NA          NA  0.50833279  0.03002475          NA -0.58243943          NA
 [13]  0.83330395          NA  0.56510642 -1.09854652 -0.39645243          NA -0.83643570  1.05101925          NA -0.30847711 -0.86849755          NA
 [25]  0.22347626  0.32604805 -0.57871976          NA  0.09027896          NA          NA  0.99316835  2.41807507  1.58642729          NA          NA
 [37]  0.90656119          NA          NA -0.03456743          NA  0.86298334 -0.77957127          NA          NA  0.67980838  0.50480509          NA
 [49] -0.59152530  0.32214993 -0.90777485          NA -0.18968352          NA -0.23943171  0.05031068  0.03289719  1.24506360 -0.64444871 -0.21408440
 [61]          NA          NA  0.43272234          NA          NA          NA  0.54062303          NA          NA          NA -0.32385941          NA
 [73] -0.07713543 -0.25143620 -0.07024574          NA          NA          NA          NA -1.71683911          NA  0.83456930          NA  1.26153405
 [85] -0.23120789  1.56135458  0.99824947          NA          NA          NA          NA          NA  2.16109079          NA -0.84106647          NA
 [97]          NA          NA -0.31545139  0.78168257

| Excellent job!

| Now that we've got NAs down pat, let's look at a second type of missing value -- NaN, which stands for 'not a number'. To generate NaN, try dividing (using
| a forward slash) 0 by 0 now.
```{r}
0/0
```
[1] NaN

| Keep up the great work!

| Let's do one more, just for fun. In R, Inf stands for infinity. What happens if you subtract Inf from Inf?
```{r}
0/0
```
[1] NaN

| Try again. Getting it right on the first try is boring anyway! Or, type info() for more options.

| Type Inf - Inf. Can you guess the result?
```{r}
Inf/Inf
```
[1] NaN

| Not quite! Try again. Or, type info() for more options.

| Type Inf - Inf. Can you guess the result?
```{r}
Inf - Inf
```
[1] NaN

| Keep working like that and you'll get there!

| Would you like to receive credit for completing this course on Coursera.org?

1: No
2: Yes

Выбор:1

