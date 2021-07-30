# rbind-in-r-Combine-Vectors-Matrix-or-Data-Frames-by-Rows

rbind in r, In this article, will describe the uses and applications of rbind(), rbind.fill() and bind_rows() functions in R programming.
rbind() in R

The name of the rbind() function indicates row-bind. The rbind()  function can be used to bind or combine several vectors, matrices, or data frames by rows.

Syntax: rbind(x1, x2, …, deparse.level = 1)

x is the first input or data frame

x1 is the second input or data frame that need to be binded

Filtering Data in R 10 Tips -tidyverse package »
Example 1: rbind vector to data frame

Let’s create a data frame and a vector list for binding.

x1 <- c(70, 45, 14, 97)              
x2 <- c(52, 27, 18, 95)                
x3 <- c(12, 25, 13, 24)                 
data1 <- data.frame(x1, x2, x3)    

Now will create a vector for binding into data1.

myvector1 <- c(90, 85, 17)

Now we can rbind myvector1 into data1.

rbind(data1, myvector1)
  x1 x2 x3
1 70 52 12
2 45 27 25
3 14 18 13
4 97 95 24
5 90 85 17

The above output’s first 4 rows are from data1 and 5th row is myvector1.
Example 2: rbind Two Data Frames in R

Let’s see how to bind rows in two different data frames.

We can utilize data1 as the first data frame and will create a new data frame data2.

y1 <- c(50, 55, 34, 47)        
y2 <- c(22, 37, 18, 15)                 
y3 <- c(22, 35, 63, 54)                 
data2 <- data.frame(y1, y2, y3)    
data2
  y1 y2 y3
1 50 22 22
2 55 37 35
3 34 18 63
4 47 15 54

If you are running rbind command you will get the following error.

datatable editor-DT package in R » Shiny, R Markdown & R »

Error in match.names(clabs, names(xi)) :names do not match previous names

This is because of column name mismatch in both the data frames.

Here you can see the column names are different, so we need to change the column names the same as the first data frame data1.

colnames(data2)<-colnames(data1)

Now will bind two data frames data1 and data2

rbind(data1,data2)
  x1 x2 x3
1 70 52 12
2 45 27 25
3 14 18 13
4 97 95 24
5 50 22 22
6 55 37 35
7 34 18 63
8 47 15 54

rbind fill() in R
Example 3: rbind fill – Row Bind with missing columns

As we see in the second example data frames with different column names is a little bit complicated with the rbind() function.  We already experienced a mismatch error in the second example.

To overcome that, the plyr package provides the rbind.fill() R function.

Let’s see how to execute rbind.fill() function in R.

We can call data2 data frame once again because we already change the column names.

y1 <- c(50, 55, 34, 47)
y2 <- c(22, 37, 18, 15)                 
y3 <- c(22, 35, 63, 54)                  
data2 <- data.frame(y1, y2, y3)    
colnames(data1)
[1] "x1" "x2" "x3"
colnames(data2)
[1] "x1" "x2" "x3"

Let’s load the plyr package in to R,

#install.packages("plyr")
library("plyr")
rbind.fill(data1, data2)
  x1 x2 x3 y1 y2 y3
1 70 52 12 NA NA NA
2 45 27 25 NA NA NA
3 14 18 13 NA NA NA
4 97 95 24 NA NA NA
5 NA NA NA 50 22 22
6 NA NA NA 55 37 35
7 NA NA NA 34 18 63
8 NA NA NA 47 15 54

Let’s see what will happen if the column names are same.

colnames(data2)<-colnames(data1)
rbind.fill(data1, data2)
  x1 x2 x3
1 70 52 12
2 45 27 25
3 14 18 13
4 97 95 24
5 50 22 22
6 55 37 35
7 34 18 63
8 47 15 54

Wow, pretty cool better than rbind function because it’s not showing any error message when column names are different and functions properly when column names are the same.
bind_rows() in R
Example 4:-bind_rows() function to bind uneven data sets

Now will try one more function bind_rows() from dplyr package. So let’s load the package into R console.

#install.packages("dplyr")
library(dplyr)
bind_rows(data1,data2)

Now both data frames data1 and data2 contains same column names, just execute the command

  x1 x2 x3
1 70 52 12
2 45 27 25
3 14 18 13
4 97 95 24
5 50 22 22
6 55 37 35
7 34 18 63
8 47 15 54

Now we want to check with different column names.

y1 <- c(50, 55, 34, 47)        
y2 <- c(22, 37, 18, 15)                 
y3 <- c(22, 35, 63, 54)                 
data2 <- data.frame(y1, y2, y3)    
bind_rows(data1,data2)
x1 x2 x3 y1 y2 y3
1 70 52 12 NA NA NA
2 45 27 25 NA NA NA
3 14 18 13 NA NA NA
4 97 95 24 NA NA NA
5 NA NA NA 50 22 22
6 NA NA NA 55 37 35
7 NA NA NA 34 18 63
8 NA NA NA 47 15 54

Pretty cool functioning same as like rbind.fill() function.
Conclusion

When it comes to data manipulation, the rbind(), rbind.fill() and bind_rows() functions are really useful.
