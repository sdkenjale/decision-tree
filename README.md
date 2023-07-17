# decision-tree
install.packages("rpart.plot")
library("rpart")
library("rpart.plot")
setwd('F:/BDA') #ssimply create bda folder in desktop
getwd()
banktrain <- read.table("C:/Users/Vikrant/Downloads/bank-sample.csv",header=TRUE,sep=",")
View(banktrain)
summary(banktrain)
drops<-c("age", "balance", "day", "campaign", "pdays", "previous", "month")
banktrain <- banktrain [,!(names(banktrain) %in% drops)]
summary(banktrain)
fit <- rpart(subscribed ~ job + marital + education + default + housing + loan + contact + poutcome,
             method="class",
             data=banktrain,
             control=rpart.control(minsplit=1),
             parms=list(split='information'))
summary(fit)
rpart.plot(fit, type=4, extra=2, clip.right.labs=FALSE, varlen=0, faclen=3)
fit <- rpart(subscribed ~ job + marital + education + default + housing + loan + contact + duration + poutcome,
             method="class",
             data=banktrain,
             control=rpart.control(minsplit=1),
             parms=list(split='information'))
summary(fit)
rpart.plot(fit, type=4, extra=2, clip.right.labs=FALSE, varlen=0, faclen=3)
newdata <- data.frame(job="retired",
                      marital="married",
                      education="secondary",
                      default="no",
                      housing="yes",
                      loan="no",
                      contact = "cellular",
                      duration = 598,
                      poutcome="unknown")
newdata
predict(fit,newdata=newdata,type=c("class"))
