Get some information
========================================================

How about Sex?

```{r}
poll<-op14_read_poll_func(filepath)
```


```{r}
test<-table(poll$Geschlecht,poll$Praeferenz.Temp..Frage.2.)
#percent male
sum(test[1,1:3])/((sum(test[1,1:3])+sum(test[2,1:3]))/100)
#percent female
sum(test[2,1:3])/((sum(test[1,1:3])+sum(test[2,1:3]))/100)
```

total persentage see oficial statistict TU Berlin


```{r}
frage1 <- table(poll$Temperaturempfinden..Frage1.,poll$Geschlecht)
barplot(frage1[,1])
barplot(frage1[,2])
barplot(frage1,beside = TRUE)
frage1_m_percent <- sapply(frage1[,1],function(x) x*100/sum(frage1[,1]))
frage1_w_percent <- sapply(frage1[,2],function(x) x*100/sum(frage1[,2]))
frage1_percent <- cbind(frage1_m_percent,frage1_w_percent)
barplot(frage1_percent,beside=TRUE)
```


