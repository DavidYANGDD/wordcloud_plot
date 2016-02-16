
library(wordcloud)

#read doc from the directory that you set
data<-readLines("nba.txt")
#Then, split the doc into words, and count the frequency for each word.
words<-unlist(strsplit(data,"\\W"))
#Using "table" function to count the frequency of each word, and sort to the top 200.
x<-tail(sort(table(words)),200)
#set the result as a data frame, then extract the dimnames and the value to combine a new 2-column data frame.
x<-as.data.frame(x)
y<-dimnames(x)[[1]]
z<-x[x!=""]
y<-as.data.frame(y)
z<-as.data.frame(z)
xxx<-as.data.frame(cbind(y,z))
#define the "blacklist" of the words that are obviously irrelavant, such as "it","are" and so on.
blacklist<-c("and","And","or","The","the","a","A","an","are","he","his","she","it","t","s","you","than","that","on","in","of","to","with","said","was","what","how","if","is","this","")
#Delete those blacklist words from the 
blackrows<-match(blacklist,xxx$y)
blackrows<-subset(blackrows,!is.na(blackrows))
xxx<-xxx[-blackrows,]

#use the wordcloud package
mycolors <- brewer.pal(8,"Dark2")
wordcloud(xxx$y,xxx$z,,c(8,0.3),random.order=FALSE,random.color=FALSE,colors=mycolors)

