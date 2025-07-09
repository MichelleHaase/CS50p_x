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
data <- c(1,2,1,1,2,1,2,2,1,2,1,2,1,1,2,1,2,2,1)
factor(data, labels = c("yes", "no"))
# output: [1] yes no  yes yes no  yes no  no  yes no  yes no  yes yes no  yes no  no  yes
# Levels: yes no
```
# Lecture 2 transforming Data
## logicals
```r
data <- c(1,2,3,4,5,6,7,8,9)
data[3] # returns 3
data[c(2,4,7)] # returns vector of 2,4,7
data <- data[-c(2,4,7)] # removes 2,4,7 from data
```
== equal; != not equal; > greater; >= greater equal ...  
TRUE(T) FALSE(F)
& AND | OR (for vectors) && AND || OR(for single values)
```r
data <- c(10,2,3,4,-20,6,7,8,9)
data < 0 # returns F F F F T F F F F
which(data < 0) # returns 5 (index of the value < 0)
which(data < 0 | data >= 10) # 1 5
filter <- data < 0 | data >= 10
filter2<- !(data < 0 | data >= 10)
data[filter] # return data that fit criteria
data2(filter2) # returns all other values
save(data2, file="data_filtered.RData)
```
any()- returns bool if any data meets criteria  
all()- returns boll if all fit 

mean() only works without NAs or na.rm = TRUE
```r
filter <- chicks$feed == "casein"
casein_chicks <- chicks[filter,] #indexing into dataframe is [row,col] so if only rows are addressed the koma is still necessary
```
is.na is.nan. is.null is.infinite
```r
is.na(df$col) #returns vector of bools
data <- df[!is.na(df$col)]
data <- subset(df,!is.na(col))
col_data <- subset(df, col == "valuename")
rownames(df) <- Null # resets the ids after the Nas are removed
```
## Menus
```r
# options in the column
feed_options <- unique(chicks$feed)

formatted_options <- paste0(1:length(feed_options), ". ", feed_options)

cat(formatted_options, sep ="\n")

#ask user
feed_choice <- as.integer(readline("feed type: ,"))

if (feed_choice < 1 || feed_choice > length(feed_options)){
    cat("invalid choice")
}


#print result
else {
    selected <- feed_options[feed_choice]
    print(subset(chicks, feed == selected))
}
```
rbind() binds rows of df of the same size  
Q1$quarter <- "Q1" # creates a new column and fills all rows with "Q1"  
if else can be used as a function similar to comperhension
```r
sales$value <- ifelse(sales$amount > 100, "high Value", "regular")
```


