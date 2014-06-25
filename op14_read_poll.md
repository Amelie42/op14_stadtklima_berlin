**Name**
  
  op14_read_poll_func.md

**Description**
  
  Functions for:
  1. reading raw poll data
  2. preprocessing (converting time information to R standards)   

**Usage**
  
  call function

**Input**
  
  filepath: full path of data (.csv, comma separated!) file

**Output**
  
  data frame of poll results
  
**Example**

filepath<-"d:/TUB/Lehre/SoSe14/GP_OEKUP_OP_LA_Stadtklima_Berlin/R/data_r/ISI_2406/allefrageboegen.csv"
poll_data<- op14_read_poll_func(filepath) 


**To_DO**
keyword summertime Y/N

**Author**  
  MaO


read the data (csv)
```{r}
op14_read_poll_func <- function(filepath) {
  
  raw_data<-read.csv(filepath)  
```

convert time
```{r}

wintercon <-as.numeric(as.character(raw_data$Zeit))-100
raw_data$Zeit<-as.character(wintercon)# convert variable type to character 

raw_data$Datum<-as.character(raw_data$Datum)# convert variable type to character

time <- paste(raw_data$Datum,wintercon)

time <-strptime(time,"%d%m%y %H%M")# create one variable
  
```

prepare new data frame
```{r}
var_names <- names(raw_data)#get variable names (column names)

idx <- which(var_names != "Datum" & var_names != "Zeit") # kick out old time info 

poll_data <- cbind.data.frame(raw_data[,idx],time)# build new data fram with new time info

poll_data <- poll_data[c(1,15,2:14)]# reorder data frame (new time is in 2nd column now)
  
```

close function!
```{r}
}
  
```



