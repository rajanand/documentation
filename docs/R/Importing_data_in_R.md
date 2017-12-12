
## Importing data in R

When you import a file into R environment, you have to provide the path of the file. If the file is in the same working directory, there are no issues. You can just provide the file name like `data <- read.csv("file_name.csv", stringsAsFactors = TRUE)`. But if the file is in a different directory, problem might arise depends on which OS is being used to execute the script. The file system is different between windows and unix/MacOS. In windows, backslash `\` is used to separate the directories where as in Mac forward slash `'/'` is used.

#### file.path()
``` r
path <- file.path("long", "directory", "name", "file_name.txt")
path
#> [1] "long/directory/name/file_name.txt" #Output in Windows
#> [1] "long\directory\name\file_name.txt" #Output in Mac/Ubuntu
```
Depends on the OS where the script is executed, the output will differ.

### Utils package
   All the below functions are from utils package. When you install R, be default these basic packages also included. Moreover, when you start a R session, this package will be available in your environment. So, it's not required to import the function using library().

####  read.csv()
   - to read csv files as a dataframe.
   - `stringsAsFactors = TRUE` is a default value. So, mostly you have to set this value as FALSE when importing a file.
   - `sep = ','` separator value is comma as the function itself is to import a comma separated file.
   ```r
   read.csv("file_name.csv", stringsAsFactors = FALSE)
   ```

#### read.delim()
- to read tab delimited file.
-  `stringsAsFactors = TRUE` is a default value. So, mostly you have to set this value as FALSE when importing a file.
- `sep = '\t'` separator value is comma as the function itself is to import a comma separated file.
```r
read.delim("file_name.txt", stringsAsFactors = FALSE)
```

#### read.table()
- this function can be used to import any type of flat file into R as a data frame. Even csv and tab delimited file can be imported. But separator should be specified explicitly.
- `stringsAsFactors = TRUE` by default like `read.csv` and `read.delim`
- `header = FALSE` is a default value. If the file has header value, this value should be changed to True explicitly. If the file does not contain header value, column name can be passed to `col.names` argument.
- `sep=""` is a default value. Based on the type of a file, separator argument should be set. Eg. `sep = ";"` or `sep = "|"`
```r
read.table("file_name.dat",
            stringsAsFactors = FALSE,
            sep = "|",
            col.names = c("country_code", "country_name", "Population"))
```
