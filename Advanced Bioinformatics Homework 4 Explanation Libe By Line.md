# Jad Elgaali Advanced Bioinformatics Homework 4 3/17/19

```
setwd("~/rnaseq")      # this line sets the working directory of the rnaseq as the home directory
library(ggplot2)       # Use the library command to load the "ggplot2" package  
library(ggfortify)     # Use the library command to load the "ggfortify" package

data <- read.csv(       # This reads in the CSV file called "Quant/tutorial.count.kallisto.txt" into a data frame called data
  "Quant/tutorial.count.kallisto.txt",    # This is the name of the file being read in
  comment.char = "#",   # This line sets the comment characters as the # symbol
  sep = "\t",           # This sets the field separator character so the values on each line of the file are separated by a tab
  check.names = FALSE   # This logical statement is set to FALSE so names of the variables in the data frame are not checked to ensure that variable names have valid syntax and are not duplicated.
)                       # This bracket closes the scope for this chunk of code.

rownames(data) <- data[, 1]           # Create a data frame called rownames(data). This rownames(data) gives the row names for the data frame. And data[, 1] retrieves the entire first column.
data <- data[, tail(1:ncol(data), 6)] # This returns all of column 6 and the end of the object of the data frame with all its columns (tail(1:ncol(data)).
colnames(data) <- gsub(               # The gsub() function changes the name of the column in the dataframe.
  "^.+((KO|WT)\\d{2}).+$",            # This is the string replaced
  "\\1",                              # This is the string the previous line will be replaced with to simplify.
  colnames(data)                      # This is the data frame from which the column name will be replaced with.
)                                     # This bracket closes the scope for this chunk of code.

data.rmLow <- data[            # Create a data frame called data.rmLow and the rmLow filters genes or RNA transcripts with expression levels at a certain threshold for the samples. The data[ begins to retrieve data in a cell.
  apply(                       # The apply function allows you to make quick operations on a matrix.
    data,                      # We will use apply on elements from "data"
    1,                         # We will only apply the functions to each row.  
    function(x) {              # The function we are applying is called x.
      all(x >= 10)             # Checks to see if all values are greater than or equal to 10.
    }                          # This closes the scope of function(x).
  ),                           # This closes the scope of the apply() function.
]                              # This closes the scope of the data[] call to retrieve the data in a cell.

data.trans <- apply(           # Create a data frame called data.trans and the trans function transforms the data data frame. The second part of the line calls the apply () function to make operations on a matrix.
  data.rmLow,                  # We will do operations on data.rmLow which is a filtered dataset from the last chunk of code.
  2,                           # We will apply this operations only to the columns of this dataset.
  function(x) {                # We are calling function(x) to do an operations
    10^6 * x / sum(x)          # We are going to multiply x by 10^6 and divide that by the sum of the x-values.
  }                            # Close the function scope
)                              # Close the apply scope and also this chunk of code. 

mad <- apply(                  # Create a data frame called mad and do an operation by using the apply() function.
  log2(data.trans),            # This computes a binary log base 2 on the transformed data frame from the last chunk called data.trans.
  1,                           # The operation will only happen on the rows
  mad                          # The operation will happen on the elements in the data frame called mad.
)                              # This closes the apply function and the scope of the chunk of code. 

top <- head(                   # Creates a data frame called top and calls the head() function to return the first number of n rows.
  data.trans[order(-mad), ],   # The data frame called by head() is data.trans and is sorting the values from the previous data frame mad in DESCENDING ORDER
  500                          # Calls the first 500 rows
)                              # Closing brackets for the head function and this chunk of codee.

top.group <- cbind(            # Creates a data frame called top.group and calls the cbind (), or column bind, function to append or combine matrices or data frames by column.
  t(top),                      # The first  to be combined by column is the top data frame which is having the t() function done on it to transpose it.
  data.frame(                  # The second data frame to be combined is called data.frame.
    group = gsub("\\d{2}", "", colnames(top))         # We are specifying the values of group by using the gsub() function to change the characters "\\d{2}" to "" which is whitespace.
  ) 						   # The closes the data.frame() scope
) 							   # This closes the cbind() scope and that of the chunk of code in general.


pdf(                                     # This creates a PDF  
  file = "Quant/tutorial1.pca.pdf",      # The name of the PDF file will be "Quant/tutorial1.pca.pdf".
  width = 8, 						     # The information in the PDF will have a width of 8.
  height = 8 							 # The information in the PDF will have a height of 8.
) 										 # This closing bracket closes the scope of this chunk of code.

autoplot( 				# This function autoplots survival fit curves using the ggplot2 package.
  prcomp(t(top))        # This conducts a principle component analysis (PCA) and transposes the data frame created earlier called "top".
  data = top.group,     # This loads the data set of the data frame top and loads them by groups.
  colour = 'group',     # Automatically plots the colours by their groups
  shape = FALSE,        # Makes a plot without points 
  label.size = 5        # This changes the font size to 5. 
) +                     # This closing bracket closes the scope of this chunk of code but the + sign adds one more function which will be "theme_minimal(base_size = 18)".
  theme_minimal(base_size = 18)      # This creates a basic theme with no background annotation with a size of 18. 

dev.off()               # This shuts down the device so the saved PDF will show up in the computer.


print(sessionInfo())    # This prints the information of the current R session which is read and collected by the sessionInfo() function.
q(save = "no")          # This quits the program and does not save the progress.

```