# CableTVsubscriptionDATA-project-
CableTVsubscriptionDATA project 
Mahbubul Hasan (mhasan1)
Elizabeth James (enjames)
Omer Khan (oakhan)
Jennifer Tichenor (jtchnor2)


Predicting Cable Subscriptions
Using information regarding an individual’s age, gender, income, home ownership, class segment, and number of children, we plan to predict whether or not the individual will subscribe to cable. 
https://www.kaggle.com/amansaxena/cabletv-subscriber-data
Report:
This data contains information on people who have subscribed to a certain kind of Cable TV service. The data contains just 300 observations and 7 variables.
The 7 variables are: 
Age - the age of the TV subscriber 
Gender - the gender of the TV subscriber 
Income - the income of the TV subscriber 
kids - the number of kids the TV subscriber has 
ownHome - if the TV subscriber owns the home or not 
subscribe - if they have subscribed to the TV services or not 
segment - the segment of the TV subscriber's subscription
Source: Udemy course on Data Analytics
Preliminary Analysis of the Data
The data is based on 300 observations of people subscribed to cable TV. Cable subscribers range in age from 19 to 80. The median age is 39, while the average age is 41, so the ages skew just a little higher. Income has a minimum of $-5,183 and a maximum of $114,278. We may need to dig into why some incomes report as being negative to understand whether the data is valid or not. The median income is $52,014 while the average income is $50,937. The number of children range from 0 to 7 per subscriber, with the median being 1, while the mean is 1.27. A majority of subscribers have 1 child or no children at all.  Additional observations include:
•	Slightly more subscribers are women (52%).
•	87% of people polled have not subscribed to cable.
•	53% of people say they do not own their home. 
•	Given the options to categorize their lifestyle as suburb, urban, travelers, or transitioning,
o	26% surveyed identified themselves as travelers,
o	17% selected urban,
o	23% chose transitioning or “moving up,” and
o	33% selected suburb.
 
R code:
rm(list=ls())

library(readr)

#read/import csv file into R
CT <- read.csv('/Users/mhasan1/Desktop/CableTVSubscribersData.csv',header=TRUE)
CT
summary(CT)
nrow(CT)
CT2<- na.omit(CT)
nrow(CT2)
library(expss)
install.packages("expss")
library(expss)
Percent_Male <- count_if("Male", CT$gender)/nrow(CT)
Percent_Male
Percent_Female <- 1 - Percent_Male
Percent_Female

#determine number of rows
nrow(CT)

#nrow < 2500; no volume restriction needed

summary(CT)

#summary shows no NA values
#double check by running na.omit and recounting rows

CT2 <- na.omit(CT)
nrow(CT2)

#new data is same as original data
#no NA values confirmed
#use original CableTVSubscriberData for further calculations

#percentages for character types
#check factors

factor(CableTVSubscribersData$gender)
#returns levels Male Female
#omitted from output report below
factor(CableTVSubscribersData$ownHome)
#returns ownNo ownYes
#omitted from output report below
factor(CableTVSubscribersData$subscribe)
#returns subNo subYes 
#subNo subYes will be our on/off end goal for categories
#omitted from output report below
factor(CableTVSubscribersData$Segment)
#returns "Moving up" "Suburb mix" "Travelers" "Urban hip"
#omitted from output report below

library(expss)
#run percentages
Percent_Male <- count_if("Male", CableTVSubscribersData$gender)/nrow(CableTVSubscribersData)
Percent_Male
Percent_Female <- 1 - Percent_Male
#only 2 factors makes “1 – “ work
Percent_Female

Percent_Own <- count_if("ownYes", CableTVSubscribersData$ownHome)/nrow(CableTVSubscribersData)
Percent_Own
Percent_OwnNo <- 1 - Percent_Own
#only 2 factors makes “1 – “ work
Percent_OwnNo

Percent_Sub <- count_if("subYes", CableTVSubscribersData$subscribe)/nrow(CableTVSubscribersData)
Percent_Sub
Percent_SubNo <- 1 - Percent_Sub
#only 2 factors makes “1 – “ work
Percent_SubNo

Percent_SegMovUp <- count_if("Moving up", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
Percent_SegSuburb <- count_if("Suburb mix", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
Percent_SegTrav <- count_if("Travelers", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
Percent_SegUrban <- count_if("Urban hip", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)

#more than two factors; reason not “1 – “
Percent_SegMovUp
Percent_SegSuburb
Percent_SegTrav
Percent_SegUrban
Output:
> rm(list=ls())
> library(readr)
> CableTVSubscribersData <- read_csv("CableTVSubscribersData.csv")
Parsed with column specification:
cols(
  age = col_double(),
  gender = col_character(),
  income = col_double(),
  kids = col_double(),
  ownHome = col_character(),
  subscribe = col_character(),
  Segment = col_character()
)
> nrow(CableTVSubscribersData)
[1] 300
> summary(CableTVSubscribersData)
age	gender	income	kids	ownHome
Min.:	19.26	Length:	300	Min.:	-5183	Min.:	0	Length:	300
1stQu.:	33.01	Class:	character	1stQu.:	39656	1stQu.:	0	Class:	character
Median:	39.49	Mode:	character	Median:	52014	Median:	1	Mode:	character
Mean:	41.2	 	 	Mean:	50937	Mean:	1.27	 	 
3rdQu.:	47.9	 	 	3rdQu.:	61403	3rdQu.:	2	 	 
Max.:	80.49	 	 	Max.:	114278	Max.:	7	 	 

subscribe	Segment
Length:	300	Length:	300
Class:	character	Class:	character
Mode:	character	Mode:	character

> CableTVSubscriber2 <- na.omit(CableTVSubscribersData)
> nrow(CableTVSubscriber2)
[1] 300
> 


> library(expss)
> #run percentages
> Percent_Male <- count_if("Male", CableTVSubscribersData$gender)/nrow(CableTVSubscribersData)
> Percent_Male
[1] 0.4766667
> Percent_Female <- 1 - Percent_Male
> Percent_Female
[1] 0.5233333
> 
> Percent_Own <- count_if("ownYes", CableTVSubscribersData$ownHome)/nrow(CableTVSubscribersData)
> Percent_Own
[1] 0.47
> Percent_OwnNo <- 1 - Percent_Own
> Percent_OwnNo
[1] 0.53
> 
> Percent_Sub <- count_if("subYes", CableTVSubscribersData$subscribe)/nrow(CableTVSubscribersData)
> Percent_Sub
[1] 0.1333333
> Percent_SubNo <- 1 - Percent_Sub
> Percent_SubNo
[1] 0.8666667
> 
> Percent_SegMovUp <- count_if("Moving up", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
> Percent_SegSuburb <- count_if("Suburb mix", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
> Percent_SegTrav <- count_if("Travelers", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
> Percent_SegUrban <- count_if("Urban hip", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
> 
> Percent_SegMovUp
[1] 0.2333333
> Percent_SegSuburb
[1] 0.3333333
> Percent_SegTrav
[1] 0.2666667
> Percent_SegUrban
[1] 0.1666667
> 
#Part 2 

Appendix - R
rm(list=ls())

library(readr)

#read/import csv file into R
CableTVSubscribersData <- read_csv("CableTVSubscribersData.csv")

#determine number of rows
nrow(CableTVSubscribersData)

#nrow < 2500; no volume restriction needed

summary(CableTVSubscribersData)

#summary shows no NA values
#double check by running na.omit and recounting rows

CableTVSubscriber2 <- na.omit(CableTVSubscribersData)
nrow(CableTVSubscriber2)

#new data is same as original data
#no NA values confirmed
#use original CableTVSubscriberData for further calculations

#percentages for character types
#check factors

factor(CableTVSubscribersData$gender)
#returns levels Male Female
factor(CableTVSubscribersData$ownHome)
#returns ownNo ownYes
factor(CableTVSubscribersData$subscribe)
#returns subNo subYes 
#subNo subYes will be our on/off end goal for categories
factor(CableTVSubscribersData$Segment)
#returns "Moving up" "Suburb mix" "Travelers" "Urban hip"

library(expss)
#run percentages
Percent_Male <- count_if("Male", CableTVSubscribersData$gender)/nrow(CableTVSubscribersData)
Percent_Male
Percent_Female <- 1 - Percent_Male
Percent_Female

Percent_Own <- count_if("ownYes", CableTVSubscribersData$ownHome)/nrow(CableTVSubscribersData)
Percent_Own
Percent_OwnNo <- 1 - Percent_Own
Percent_OwnNo

Percent_Sub <- count_if("subYes", CableTVSubscribersData$subscribe)/nrow(CableTVSubscribersData)
Percent_Sub
Percent_SubNo <- 1 - Percent_Sub
Percent_SubNo

Percent_SegMovUp <- count_if("Moving up", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
Percent_SegSuburb <- count_if("Suburb mix", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
Percent_SegTrav <- count_if("Travelers", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)
Percent_SegUrban <- count_if("Urban hip", CableTVSubscribersData$Segment)/nrow(CableTVSubscribersData)

Percent_SegMovUp
Percent_SegSuburb
Percent_SegTrav
Percent_SegUrban

CableTVSubscriber3 <- CableTVSubscriber2
#assign numbers to levels
#1 = moving up
#2 = suburb mix
#3 = travelers
#4 = urban hip
group_seg <- factor(CableTVSubscriber3$Segment)
#group_seg -> moving up = 1, suburb mix = 2, travelers = 3, urban hip = 4
levels(group_seg) <- c(1,2,3,4)
CableTVSubscriber3$Segment <- group_seg

#begin cluster with age, income, kids, segment
#cannot plot list
library(stats)
library(cluster)
inputs_age_inc_kid_seg <- c("age", "income", "kids", "Segment")
newCable <- CableTVSubscriber3[inputs_age_inc_kid_seg]
plot(newCable)
newCable3 <- kmeans(newCable, 3)
newCable4 <- kmeans(newCable, 4)
newCable5 <- kmeans(newCable, 5)
newCable6 <- kmeans(newCable, 6)
newCable7 <- kmeans(newCable, 7)
newCable8 <- kmeans(newCable, 8)
newCable9 <- kmeans(newCable, 9)
newCable10 <- kmeans(newCable, 10)
newCable11 <- kmeans(newCable, 11)
newCable12 <- kmeans(newCable, 12)
newCable13 <- kmeans(newCable, 13)
newCable14 <- kmeans(newCable, 14)
newCable15 <- kmeans(newCable, 15)
newCable16 <- kmeans(newCable, 16)
newCable17 <- kmeans(newCable, 17)

#run elbow method
k_values <- 3:17
ss_values <- c(newCable3$tot.withinss, newCable4$tot.withinss, newCable5$tot.withinss, newCable6$tot.withinss, 
               newCable7$tot.withinss, newCable8$tot.withinss, newCable9$tot.withinss, newCable10$tot.withinss, 
               newCable11$tot.withinss, newCable12$tot.withinss, newCable13$tot.withinss, newCable14$tot.withinss, 
               newCable15$tot.withinss, newCable16$tot.withinss, newCable17$tot.withinss)
plot(k_values, ss_values, type="b", frame=FALSE, main = "Elbow Method", xlab = "Number of Cluster (k)", ylab = "Total within cluster SS")



#all the pretty colors - plotting clusters
#run one at a time
plot(newCable, col=newCable3$cluster)
plot(newCable, col=newCable4$cluster)
plot(newCable, col=newCable5$cluster)
plot(newCable, col=newCable6$cluster)
plot(newCable, col=newCable7$cluster)
plot(newCable, col=newCable8$cluster)
plot(newCable, col=newCable9$cluster)
plot(newCable, col=newCable10$cluster)
plot(newCable, col=newCable11$cluster)
plot(newCable, col=newCable12$cluster)
plot(newCable, col=newCable13$cluster)
plot(newCable, col=newCable14$cluster)
plot(newCable, col=newCable15$cluster)
plot(newCable, col=newCable16$cluster)
plot(newCable, col=newCable17$cluster)

#silhouette method
sil_newCable3 <- mean(silhouette(newCable3$cluster, dist(newCable))[,3])
sil_newCable4 <- mean(silhouette(newCable4$cluster, dist(newCable))[,3])
sil_newCable5 <- mean(silhouette(newCable5$cluster, dist(newCable))[,3])
sil_newCable6 <- mean(silhouette(newCable6$cluster, dist(newCable))[,3])
sil_newCable7 <- mean(silhouette(newCable7$cluster, dist(newCable))[,3])
sil_newCable8 <- mean(silhouette(newCable8$cluster, dist(newCable))[,3])
sil_newCable9 <- mean(silhouette(newCable9$cluster, dist(newCable))[,3])
sil_newCable10 <- mean(silhouette(newCable10$cluster, dist(newCable))[,3])
sil_newCable11 <- mean(silhouette(newCable11$cluster, dist(newCable))[,3])
sil_newCable12 <- mean(silhouette(newCable12$cluster, dist(newCable))[,3])
sil_newCable13 <- mean(silhouette(newCable13$cluster, dist(newCable))[,3])
sil_newCable14 <- mean(silhouette(newCable14$cluster, dist(newCable))[,3])
sil_newCable15 <- mean(silhouette(newCable15$cluster, dist(newCable))[,3])
sil_newCable16 <- mean(silhouette(newCable16$cluster, dist(newCable))[,3])
sil_newCable17 <- mean(silhouette(newCable17$cluster, dist(newCable))[,3])
silhouette_values <- c(sil_newCable3, sil_newCable4, sil_newCable5, sil_newCable6, sil_newCable7, 
                       sil_newCable8, sil_newCable9, sil_newCable10, sil_newCable11, sil_newCable12, 
                       sil_newCable13, sil_newCable14, sil_newCable15, sil_newCable16, sil_newCable17)
plot(k_values, silhouette_values, type = "b", frame = FALSE, main  = "Silhouette Method", xlab = "Number of Cluster (k)", ylab = "Silhouette Values")
#appears that 3 clusters is best using this method

#best fit using between/within
ratioNewCable3 <- newCable3$betweenss/newCable3$tot.withinss
ratioNewCable4 <- newCable4$betweenss/newCable4$tot.withinss
ratioNewCable5 <- newCable5$betweenss/newCable5$tot.withinss
ratioNewCable6 <- newCable6$betweenss/newCable6$tot.withinss
ratioNewCable7 <- newCable7$betweenss/newCable7$tot.withinss
ratioNewCable8 <- newCable8$betweenss/newCable8$tot.withinss
ratioNewCable9 <- newCable9$betweenss/newCable9$tot.withinss
ratioNewCable10 <- newCable10$betweenss/newCable10$tot.withinss
ratioNewCable11 <- newCable11$betweenss/newCable11$tot.withinss
ratioNewCable12 <- newCable12$betweenss/newCable12$tot.withinss
ratioNewCable13 <- newCable13$betweenss/newCable13$tot.withinss
ratioNewCable14 <- newCable14$betweenss/newCable14$tot.withinss
ratioNewCable15 <- newCable15$betweenss/newCable15$tot.withinss
ratioNewCable16 <- newCable16$betweenss/newCable16$tot.withinss
ratioNewCable17 <- newCable17$betweenss/newCable17$tot.withinss

ratioNewCable3
ratioNewCable4
ratioNewCable5
ratioNewCable6
ratioNewCable7
ratioNewCable8
ratioNewCable9
ratioNewCable10
ratioNewCable11
ratioNewCable12
ratioNewCable13
ratioNewCable14
ratioNewCable15
ratioNewCable16
ratioNewCable17
#ratio calls for 3 clusters

#create information for shopping basket rules -> may not be useful
#create binary kids vectors
kids0 <- ifelse(CableTVSubscriber2$kids == 0, 1,0)
kids1 <- ifelse(CableTVSubscriber2$kids == 1, 1,0)
kids2 <- ifelse(CableTVSubscriber2$kids == 2, 1,0)
kids3 <- ifelse(CableTVSubscriber2$kids == 3, 1,0)
kids4 <- ifelse(CableTVSubscriber2$kids == 4, 1,0)
kids5 <- ifelse(CableTVSubscriber2$kids == 5, 1,0)
kids6 <- ifelse(CableTVSubscriber2$kids == 6, 1,0)
kids7 <- ifelse(CableTVSubscriber2$kids == 7, 1,0)
#create kids matrix for binding later
kidsmatrix <- cbind(kids0, kids1, kids2, kids3, kids4, kids5, kids6, kids7)

#create binary from binary
#male = 1, female = 0
#ownYes = 1, no = 0
#subscribeYes = 1, no = 0
group_Male <- ifelse(CableTVSubscriber2$gender == "Male",1,0)
group_Female <- ifelse(CableTVSubscriber2$gender == "Feale",1,0)
group_ownYes <- ifelse(CableTVSubscriber2$ownHome == "ownYes",1,0)
group_ownNo <- ifelse(CableTVSubscriber2$ownHome == "ownNo",1,0)
group_subsYes <- ifelse(CableTVSubscriber2$subscribe == "subYes",1,0)
group_subsNo <- ifelse(CableTVSubscriber2$subscribe == "subNo",1,0)
#create matrix for later
groupmatrix <- cbind(group_Male, group_Female, group_ownYes, group_ownNo, group_subsYes, group_subsNo)

#create binary from segment
group_seg_MovingUp <- ifelse(CableTVSubscriber2$Segment == "Moving up",1,0)
group_seg_SubMix <- ifelse(CableTVSubscriber2$Segment == "Suburb mix",1,0)
group_seg_Travelers <- ifelse(CableTVSubscriber2$Segment == "Travelers",1,0)
group_seg_UrbanHip <- ifelse(CableTVSubscriber2$Segment == "Urban hip",1,0)
#create matrix for later
segmatrix <- cbind(group_seg_MovingUp, group_seg_SubMix, group_seg_Travelers, group_seg_UrbanHip)

#create bins for binary age
ageUnder25 <- ifelse(CableTVSubscriber2$age <= 25, 1,0)
age25to35 <- ifelse(CableTVSubscriber2$age >25 & CableTVSubscriber2$age <= 35, 1,0)
age35to45 <- ifelse(CableTVSubscriber2$age >35 & CableTVSubscriber2$age <= 45, 1,0)
age45to55 <- ifelse(CableTVSubscriber2$age >45 & CableTVSubscriber2$age <= 55, 1,0)
age55to65 <- ifelse(CableTVSubscriber2$age >55 & CableTVSubscriber2$age <= 65, 1,0)
ageOver65 <- ifelse(CableTVSubscriber2$age > 65, 1,0)
#age matrix
agematrix <- cbind(ageUnder25, age25to35, age35to45, age45to55, age55to65, ageOver65)

#create bins for binary income
incomeUnder10K <- ifelse(CableTVSubscriber2$income <=10000,1,0)
income10to40K <- ifelse(CableTVSubscriber2$income >10000 & CableTVSubscriber2$income <= 40000,1,0)
income40to70K <- ifelse(CableTVSubscriber2$income >40000 & CableTVSubscriber2$income <= 70000,1,0)
income70to100K <- ifelse(CableTVSubscriber2$income >70000 & CableTVSubscriber2$income <= 100000,1,0)
incomeOver100K <- ifelse(CableTVSubscriber2$income >100000,1,0)
#income matrix
incomeMatrix <- cbind(incomeUnder10K, income10to40K, income40to70K, income70to100K, incomeOver100K)
library(arules)
library(arulesViz)

matrixCableSubscriber <- cbind(groupmatrix, agematrix, incomeMatrix, segmatrix, kidsmatrix)
logicalBasket <- apply(matrixCableSubscriber,2,as.logical)
matrixCableSubRules <- as(as.matrix(logicalBasket), "transactions")

#run shopping basket

summary(matrixCableSubRules)

rules <- apriori(matrixCableSubRules, parameter = list(support = .03, confidence = .8))
#manipulate support & confidence as desired
rules
inspect(head(rules, n=10, by = "lift"))

#apply rules to dataframe to sort by RHS -> easy to read results of givens
rules_info <-
  data.frame(
    LHS = labels(lhs(rules)), 
    RHS = labels(rhs(rules)),          
    quality(rules),
    stringsAsFactors = FALSE
  )
rules_info[order(rules_info$RHS),] #change after $ to column title to reorder

#subscriberYes rules
subscriberYesRules <- rules_info[rules_info$RHS == "{group_subYes}"]
#there are no rules for Yes subscribers (no rules for no Subscribers, either)




