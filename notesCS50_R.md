# Lecture 1 Representing Data
in quartos(qmd) ctrl+ shift + K renders   
rstudio still best ide since jupiter has problems finding the kernel and quarto has no var viewer   
in rstudio klicking oon function and F1 opens help(also ?functionsname)
yaml header
```yaml
---
title: "My First Quarto"
format: html
editor: visual
echo: true
---
```
```r
name <- readline("What's your name? ")
greeting <- paste("Hello, ", name) # uses a space as separator
 # paste0() doesn't use anything as separator
print(greeting)

# consise
print(paste("Hello,", name))
```
using readline always assigns strings, strings can't be concatanted with +
## coercion
as.character as.double as.integer
```r
test <- "1"
test <- as.integer(test)

test2 <- as.integer(readline("text "))
```
sum(var1, var2) sums up the variables  
unique(data) - shows only the uniqe data options 
```r
data <- c(1,2,1,1,2,1,2,2,1,2,1,2,1,1,2,1,2,2,)
unique(data)
# output: [1] 1,2
```

## tables
observations rows are, variables columns  
read.csv(data.csv) - creates a Dataframe  
read_csv(data.csv) - creates a tibble  
df's automatically convert all non numeric data to factors and print out completely if columns are accessed the returned item is a vector  
tibbles print out the first 10 lines and keeps all datatypes, if columns are accessed with $ the returned item is a vector using [, "colname"] 1d tibble   

columns are accesable by variablename$columnname  
INDEXCES START AT 1  
vectors - list of values of the same storrage mode, accesable per index, can be summed up with sum like sum(var1$col1), vectors can also be added together like va1$col1 + va1$col2 which returns a vector of the values added per row
```r
df <- data.frame(name = c("Alice", "Bob", "m"), age = c(25, 30, 36), height = c(1.7, 2.0, 1.8))
ageXheight <- df$age + df$height
# Output: [1] 26.7 32.0 37.8
```
write.csv() - for df's   
write_csv() - for tibbles   

# special values
inf , -inf - infinity  
NA - not available (a vector of NA's is a vector with no data filled in but saved space for it)  
NaN - Not a number  
NULL - empty (a vector of NULL doesn't exist)  

## factors
factor(vector) - categorises data, levels are the unique options
```r
data <- c(1,2,1,1,2,1,2,2,1,2,1,2,1,1,2,1,2,2,)
factor(data, labels = c("yes", "no"))
# output: [1] yes no  yes yes no  yes no  no  yes no  yes no  yes yes no  yes no  no  yes
# Levels: yes no
```
# Lecture 2 transforming Data
## outiers
