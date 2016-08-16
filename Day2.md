#Day 2 Problem Set

##Correlation

A. Calculate the pairwise correlations between genes. What are the dimensions of the output matrix? What would it be if we correlated samples instead of genes?
cor(my_data)
cor(t(my_data)


B. What is the range of values in this matrix? What are the highest and lowest values you would expect and why?
range(cor(t(my_data))
[1] -0.7469656  1.0000000

C. Find the pair of genes that are most correlated. Do you need to operate over the entire matrix to do this?
w <- my_data
w2 <- as.data.frame(as.table(w))
w2 <- w2$Var1
w2 <- w2[w2$Var1 != w2$Var2,]
w2 <- w2[w2$Var1 != w2$Var2,]
*Courtesy of Will Gordon*

Var1   Var2      Freq
1029802 COL4A1 COL4A2 0.9698228
2542732 COL4A2 COL4A1 0.9698228
237207  RPS4Y1  DDX3Y 0.9679781
984977   DDX3Y RPS4Y1 0.9679781
123677   DDX3Y  USP9Y 0.9678019
236712   USP9Y  DDX3Y 0.9678019

D. By default, the R function cor() uses the Pearson method for calculating correlation coefficients. If we change to using a rank-based method like Spearman’s rho, do we find a different pair of genes that are the most highly correlated?
Yes, there are different pairs of genes that are most higly correlated
Var1      Var2      Freq
787493  LOC339047 LOC440350 0.9679712
1761333 LOC440350 LOC339047 0.9679712
1073092   HLA-DMA      CD74 0.9597321

E. Plot a matrix of the top 20 most correlated genes (hint: consider using the library corrplot)
test <- w[unique(w2top$Var2),unique(w2top$Var1)]
corrplot(test, method="color")
![Corr Plot](/Corr Plot.png)

##Clustering
A. Cluster the top 20 most correlated genes using complete hierarchical clustering and visualize the output tree
clusters <- hclust(dist(test))
plot(clusters)
![Corr Plot](/Dendogram.png)

B. Try using different clustering methods and observe the effects upon how correlated genes are grouped together.
![Corr Plot](/Dendogram Average.png)

C. If we cluster these genes with complete hierarchical clustering and divide the tree into 4 groups, how many genes are in the largest group? The smallest?
clusterCut  <- cutree(clusters, 4)
 COL4A2    COL4A1     DDX3Y    RPS4Y1     USP9Y    EIF1AY LOC440350 LOC339047      CD74 
        1         1         2         2         2         2         3         3         4 
  HLA-DMA   JARID1D     ITGB2    LAPTM5 
        4         2         4         4 