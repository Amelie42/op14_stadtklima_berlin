**Name**
  
  op14_merge_pmv_poll_func.md

**Description**
  
  Functions for:
  1. reading raw BIOMET and poll Data
  2. merging both   

**Usage**
  library(FGClimatology)
  source(op14_read_poll_func.md)
  call function

**Input**
  raw data of BIOMET station  
  file_BM2<-"d:/TUB/Lehre/SoSe14/GP_OEKUP_OP_LA_Stadtklima_Berlin/R/data_r/CR1000_BIOMET2.dat"
  file_BM1<-"d:/TUB/Lehre/SoSe14/GP_OEKUP_OP_LA_Stadtklima_Berlin/R/data_r/CR1000_BIOMET1.dat"
  file_WM<-"d:/TUB/Lehre/SoSe14/GP_OEKUP_OP_LA_Stadtklima_Berlin/R/data_r/CR1000_BIOMET2_Gill_Windmaster.dat"
  
  file_poll: poll data

**Output**
  
  data frame of poll and UTCI
  infos on UTCI at: http://www.utci.org/utci_doku.php
  
**Example**


**TO_DO**
keyword index for pmv,tmrt,utci


**Author** 
  MaO


```{r}
op14_merge_pmv_poll_func<-function(file_BM2,file_BM1,file_WM,file_poll){
```


read biomet and poll compute PMV

```{r}
biomet  <- read_BIOMET(file_BM1, file_BM2, file_WM)
utci    <- calc_utci(biomet)
poll    <- op14_read_poll_func(file_poll)

```


```{r}

biomet$TIMESTAMP<-as.POSIXlt(biomet$TIMESTAMP)
poll   <-subset(poll, time>=biomet$TIMESTAMP[1] & time <= biomet$TIMESTAMP[nrow(biomet)], !is.na(time))
m_utci <-as.numeric(1:nrow(poll)*0-999.)
m_poll <- cbind(poll,m_utci)
for (i in 1: nrow(poll)){
  if (sum(biomet$TIMESTAMP == poll$time[i]) == 0) {m_poll$m_utci[i] = NA}
  else{ m_poll$m_utci[i]<-  utci[which(biomet$TIMESTAMP == poll$time[i])]}  
}
```

```{r}
return(m_poll)
}
```

