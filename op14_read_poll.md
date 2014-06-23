**Name**
  
  op14_read_poll_func.md

**Description**
  
  Functions for:
  1. reading raw poll data
  2. preprocessing (converting time formate)   

**Usage**
  
  call function

**Input**
  
  filepath: full path of data (.csv, comma separeted!) file

**Output**
  
  data frame of poll results

**Author**
  
  MaO


read the data (csv)
```{r}
readGHCNdata <- function(filepath) {
  
  raw_data<-read.csv(filepath)  
```

convert time
```{r}
raw_data$Zeit<-as.character(raw_data$Zeit)

raw_data$Datum<-as.character(raw_data$Datum)

time <- paste(raw_data$Datum,raw_data$Zeit)

time <-strptime(time,"%d%m%y %H%M")
  
```

prepare new data frame
```{r}
var_names <- names(raw_data)#get variable names (column names)

idx <- which(var_names != "Datum" &  names != "Zeit") # kick out old time info 

poll_data <- cbind.data.frame(raw_data[,idx],time)# build new data fram with new time info

poll_data <- poll_data[c(1,15,2:14)]# reorder data frame (new time is in 2nd column now)
  
```

close function!
```{r}
}
  
```



