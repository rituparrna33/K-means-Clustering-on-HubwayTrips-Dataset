# K-means-Clustering-on-HubwayTrips-Dataset

#####R Script File for K-means Clustering in R where normalization is required

getwd()

hubwaytrip = read.csv("HubwayTrips.csv")

str(hubwaytrip)


###### Normalization
install.packages("caret")
library(caret)
preproc = preProcess(hubwaytrip)
preproc
hubwaytripNorm = predict(preproc, hubwaytrip)
hubwaytripNorm
mean(hubwaytripNorm$Duration)
sd(hubwaytripNorm$Duration)
mean(hubwaytripNorm$Age)
sd(hubwaytripNorm$Age)
mean(hubwaytripNorm$Afternoon)
sd(hubwaytripNorm$Afternoon)
mean(hubwaytripNorm$Evening)
sd(hubwaytripNorm$Evening)
mean(hubwaytripNorm$Night)
sd(hubwaytripNorm$Night)
mean(hubwaytripNorm$Weekday)
sd(hubwaytripNorm$Weekday)
mean(hubwaytripNorm$Weekend)
sd(hubwaytripNorm$Weekend)
mean(hubwaytripNorm$Male)
sd(hubwaytripNorm$Male)
mean(hubwaytripNorm$Age)
sd(hubwaytripNorm$Age)


#### K-means clustering with 10 clusters
set.seed(1234)
KmeansClustering = kmeans(hubwaytripNorm, centers = 10)


##### Examination of results
table(KmeansClustering$cluster)
tapply(hubwaytrip$Duration, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Morning, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Afternoon, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Evening, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Night, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Weekday, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Weekend, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Male,KmeansClustering$cluster, mean)
tapply(hubwaytrip$Age, KmeansClustering$cluster, mean)

#####Visualiseing the clusters
install.packages('ggpubr')
library(ggpubr)
install.packages('factoextra')
library(factoextra)
fviz_cluster(KmeansClustering, data = hubwaytrip,
             geom = "point",
             ellipse.type = "convex", 
             ggtheme = theme_bw()
)

fviz_cluster(KmeansClustering, data = hubwaytrip,
             geom = "point",
             ellipse.type = "euclid", 
             ggtheme = theme_bw()
)



