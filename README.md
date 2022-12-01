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


# K-means clustering
set.seed(1234)
KmeansClustering = kmeans(hubwaytripNorm, centers = 10)

# Examination of results
table(KmeansClustering$cluster)
tapply(hubwaytrip$Duration, KmeansClustering$cluster, mean)
tapply(hubwaytrip$Age, KmeansClustering$cluster, mean)
