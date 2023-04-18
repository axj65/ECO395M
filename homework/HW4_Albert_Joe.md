## 1. Clustering and PCA

### PCA

#### Wine Color

I want to first look at how PCA can help us distinguish white wines from
red wines.

As we can see, with 2 principle components, PCA can help us distinguish
most red wines from white wines.
![](HW4_Albert_Joe_files/figure-markdown_strict/wine3-1.png)

#### Wine Quality

With 2 principal components, it seems that as PC2 values get lower, the
quality increases. However, this is not very conclusive and PC1 is not
very informative regarding the wine quality.

![](HW4_Albert_Joe_files/figure-markdown_strict/wine5-1.png)

Now looking at the PC2 and PC3, we can see that wines generally score
better when PC2 and PC3 are both less than 0.

![](HW4_Albert_Joe_files/figure-markdown_strict/wine6-1.png)

This may not work on an .md file but the folowing is an interactive 3d
plot of the 3 principal components. This pretty much tells the same
story as the plot for PC2 and PC3.

### K-means

We can first create an elbow plot to see the optimal number of clusters.
I found this to be 5 clusters. For this portion, I want to focus on what
K-means can tell us about the quality.

![](HW4_Albert_Joe_files/figure-markdown_strict/wine8-1.png)

The plot below helps visualize the proportion of each wine quality
scores for each cluster. Although not particularly helpful in
distinguishing higher quality wines from lower quality ones, we can see
that cluster 2 offers a better chance of having a better wine score.

![](HW4_Albert_Joe_files/figure-markdown_strict/wine12-1.png)

In summary, looking at the first 2 principal components in PCA does a
terrific jobs in distinguishing red from white wines. Looking at the
first 3 components, it also helps us distinguish wine quality. Although
K-means clustering with 5 clusters does offer some insights, it is not
particularly helpful.

## 2. Market Segmentation

### NutrientH2O Report

K-means clustering often offers good, interpretable insights into
marketing segments. Based on the information from the elbow plot shown
below, I group followers into 5 segments and give the conclusions of
what advertising to the different segments might entail.

![](HW4_Albert_Joe_files/figure-markdown_strict/market3-1.png)

#### Marketing Segments

Using 5 clusters, I calculated the mean of each variable for each
cluster. Below, I show the heatmap of the means for reference along with
the market segment of each cluster based on the limited knowledge
gathered from the particular topics.

![](HW4_Albert_Joe_files/figure-markdown_strict/market6-1.png)

Cluster 1: photo\_sharing, cooking Cluster 2: sports, food, religion,
parenting, some photo sharing Cluster 3: Not very active on social media
or not particularly interested in just a few topics Cluster 4: travel,
politics, news Cluster 5: health\_nutrition, personal\_fitness, some
photo sharing

#### Interpreting the Segments

The following offers a generalization of what the clusters or market
segments may entail.

1.  Cluster 1 seems to consist of users who like to share photos of
    their food. These people gnerally like to take lots of pictures of
    their meals and post them.

2.  Cluster 2 seems to consist of the ‘traditional’ parents. Their kids
    may play sports, they may go to church on Sundays, they probably
    watch football on Sundays, and they may sometimes share photos of
    family and friends getting together to have a meal.

3.  Nothing particular stands out about Cluster 3. They most likely do
    not post much but could possibly scroll through their feed as a form
    of entertainment.

4.  Cluster 4 seems to consist of businessmen and businesswomen. They
    are into politics and the news and may travel for work, or atleast
    have the money to travel more often for leisure.

5.  Cluster 5 may be the health and fitness fanatics. They like going to
    the gym, eating healthy foods, and may post pictures of them at the
    gym, their choice of protein shake, pre-workout, or nutritious meal.

#### Recommendations on Advertising

Now that we have interpreted the market segments, we need to identify
the proportion of people in each segment as seen below. Based on these
numbers and the conclusions drawn above, I make the following
recommendations:

    ## # A tibble: 5 × 2
    ##   cluster     n
    ##     <dbl> <int>
    ## 1       1   785
    ## 2       2   934
    ## 3       3   709
    ## 4       4   601
    ## 5       5  4804

Cluster 1: If the company wants their drink to appear very often in
posts, this would be the segment to advertise to. This is because this
segment posts the most pictures of their food, in which drinks often
appear beside. The drawback is that many people do not look too closely
at their feed, and the company’s drink may not be noticed as people are
focused on the decorative food on these follower’s plates.

Cluster 2: This segment does not have many posts. However, this still
presents an interesting marketing opportunity as parents whose kids play
sports and have get-togethers will often buy sports drinks such as
NutrientH2O in bulk. Although they may not post as much, they could
potentially account for a good amount of profits.

Cluster 3: This segment likely represents the majority of the
population. Although not particularly interesting, advertising to this
segment most likely captures the greatest number of people. Whether they
are likely to buy the drink on based on the advertisement cannot be
determined.

Cluster 4: They account for a small proportion of the population and do
not offer any particular benefits. I do not recommend advertising to
this segment.

Cluster 5: This segment likely posts picture of their workout
supplements, in which NutrientH2O could be a part of especially during
their workout. These people may purchase drinks similar to NutrientH2O
to drink during their workouts and post pictures of the drink if they
like the taste and the perceived benefits. This segments posts seems to
offer more value than those in Cluster 1 as these followers would more
likely post NutrientH2O as the main attraction as opposed to those in
Cluster 1 whose post’s main attraction are probably the food.

## 3. Association Rules for Grocery Purchases

I played around with the confidence and lift values based on
observations from the plots below and the different results from a few
different combinations of confidence and lift.

In particular, by setting confidence to 0.5 and lift to 2, I found
strong associations between a variety of items and ‘other vehgetables’
or ‘whole milk’. On other words, it seems that when people buy other
things, they also tend to buy ‘other vegetanles’ and ‘whole milk’ as
well. For different values of confidence and lift, values made sense for
the most part. All seemd like combinations I would potentially buy based
on what I have or do not have at home.

However, one interesting rule I found was between ‘curd, tropical fruit’
and ‘yogurt’. This rule has a lift of 3.69 and a confidence of 0.51.
Although this was not an association I would typically expect, both the
lift and confidence are high relative to the remainder of the
associations.

    ##       lhs                            rhs                    support confidence    coverage     lift count
    ## [1]   {curd,                                                                                             
    ##        tropical fruit}            => {yogurt}           0.005287239  0.5148515 0.010269446 3.690645    52
    ## [2]   {citrus fruit,                                                                                     
    ##        root vegetables,                                                                                  
    ##        whole milk}                => {other vegetables} 0.005795628  0.6333333 0.009150991 3.273165    57
    ## [3]   {pip fruit,                                                                                        
    ##        root vegetables,                                                                                  
    ##        whole milk}                => {other vegetables} 0.005490595  0.6136364 0.008947636 3.171368    54
    ## [4]   {pip fruit,                                                                                        
    ##        whipped/sour cream}        => {other vegetables} 0.005592272  0.6043956 0.009252669 3.123610    55
    ## [5]   {onions,                                                                                           
    ##        root vegetables}           => {other vegetables} 0.005693950  0.6021505 0.009456024 3.112008    56
    ## [6]   {citrus fruit,                                                                                     
    ##        root vegetables}           => {other vegetables} 0.010371124  0.5862069 0.017691917 3.029608   102
    ## [7]   {root vegetables,                                                                                  
    ##        tropical fruit,                                                                                   
    ##        whole milk}                => {other vegetables} 0.007015760  0.5847458 0.011997966 3.022057    69
    ## [8]   {root vegetables,                                                                                  
    ##        tropical fruit}            => {other vegetables} 0.012302999  0.5845411 0.021047280 3.020999   121
    ## [9]   {butter,                                                                                           
    ##        whipped/sour cream}        => {other vegetables} 0.005795628  0.5700000 0.010167768 2.945849    57
    ## [10]  {tropical fruit,                                                                                   
    ##        whipped/sour cream}        => {other vegetables} 0.007829181  0.5661765 0.013828165 2.926088    77
    ## [11]  {butter,                                                                                           
    ##        tropical fruit}            => {other vegetables} 0.005490595  0.5510204 0.009964413 2.847759    54
    ## [12]  {fruit/vegetable juice,                                                                            
    ##        root vegetables}           => {other vegetables} 0.006609049  0.5508475 0.011997966 2.846865    65
    ## [13]  {root vegetables,                                                                                  
    ##        whipped/sour cream,                                                                               
    ##        whole milk}                => {other vegetables} 0.005185562  0.5483871 0.009456024 2.834150    51
    ## [14]  {onions,                                                                                           
    ##        whole milk}                => {other vegetables} 0.006609049  0.5462185 0.012099644 2.822942    65
    ## [15]  {root vegetables,                                                                                  
    ##        whole milk,                                                                                       
    ##        yogurt}                    => {other vegetables} 0.007829181  0.5384615 0.014539908 2.782853    77
    ## [16]  {fruit/vegetable juice,                                                                            
    ##        whole milk,                                                                                       
    ##        yogurt}                    => {other vegetables} 0.005083884  0.5376344 0.009456024 2.778578    50
    ## [17]  {pastry,                                                                                           
    ##        root vegetables}           => {other vegetables} 0.005897306  0.5370370 0.010981190 2.775491    58
    ## [18]  {margarine,                                                                                        
    ##        root vegetables}           => {other vegetables} 0.005897306  0.5321101 0.011082867 2.750028    58
    ## [19]  {pip fruit,                                                                                        
    ##        whole milk,                                                                                       
    ##        yogurt}                    => {other vegetables} 0.005083884  0.5319149 0.009557702 2.749019    50
    ## [20]  {root vegetables,                                                                                  
    ##        tropical fruit,                                                                                   
    ##        yogurt}                    => {whole milk}       0.005693950  0.7000000 0.008134215 2.739554    56
    ## [21]  {frozen vegetables,                                                                                
    ##        root vegetables}           => {other vegetables} 0.006100661  0.5263158 0.011591256 2.720082    60
    ## [22]  {chicken,                                                                                          
    ##        root vegetables}           => {other vegetables} 0.005693950  0.5233645 0.010879512 2.704829    56
    ## [23]  {citrus fruit,                                                                                     
    ##        whipped/sour cream}        => {other vegetables} 0.005693950  0.5233645 0.010879512 2.704829    56
    ## [24]  {pip fruit,                                                                                        
    ##        root vegetables}           => {other vegetables} 0.008134215  0.5228758 0.015556685 2.702304    80
    ## [25]  {newspapers,                                                                                       
    ##        root vegetables}           => {other vegetables} 0.005998983  0.5221239 0.011489578 2.698417    59
    ## [26]  {root vegetables,                                                                                  
    ##        shopping bags}             => {other vegetables} 0.006609049  0.5158730 0.012811388 2.666112    65
    ## [27]  {pork,                                                                                             
    ##        root vegetables}           => {other vegetables} 0.007015760  0.5149254 0.013624809 2.661214    69
    ## [28]  {curd,                                                                                             
    ##        tropical fruit}            => {other vegetables} 0.005287239  0.5148515 0.010269446 2.660833    52
    ## [29]  {whipped/sour cream,                                                                               
    ##        whole milk,                                                                                       
    ##        yogurt}                    => {other vegetables} 0.005592272  0.5140187 0.010879512 2.656529    55
    ## [30]  {butter,                                                                                           
    ##        root vegetables}           => {other vegetables} 0.006609049  0.5118110 0.012913066 2.645119    65
    ## [31]  {other vegetables,                                                                                 
    ##        pip fruit,                                                                                        
    ##        root vegetables}           => {whole milk}       0.005490595  0.6750000 0.008134215 2.641713    54
    ## [32]  {domestic eggs,                                                                                    
    ##        root vegetables}           => {other vegetables} 0.007320793  0.5106383 0.014336553 2.639058    72
    ## [33]  {domestic eggs,                                                                                    
    ##        whipped/sour cream}        => {other vegetables} 0.005083884  0.5102041 0.009964413 2.636814    50
    ## [34]  {curd,                                                                                             
    ##        root vegetables}           => {other vegetables} 0.005490595  0.5046729 0.010879512 2.608228    54
    ## [35]  {tropical fruit,                                                                                   
    ##        whole milk,                                                                                       
    ##        yogurt}                    => {other vegetables} 0.007625826  0.5033557 0.015149975 2.601421    75
    ## [36]  {rolls/buns,                                                                                       
    ##        root vegetables}           => {other vegetables} 0.012201322  0.5020921 0.024300966 2.594890   120
    ## [37]  {root vegetables,                                                                                  
    ##        whipped/sour cream}        => {other vegetables} 0.008540925  0.5000000 0.017081851 2.584078    84
    ## [38]  {root vegetables,                                                                                  
    ##        yogurt}                    => {other vegetables} 0.012913066  0.5000000 0.025826131 2.584078   127
    ## [39]  {butter,                                                                                           
    ##        whipped/sour cream}        => {whole milk}       0.006710727  0.6600000 0.010167768 2.583008    66
    ## [40]  {pip fruit,                                                                                        
    ##        whipped/sour cream}        => {whole milk}       0.005998983  0.6483516 0.009252669 2.537421    59
    ## [41]  {butter,                                                                                           
    ##        yogurt}                    => {whole milk}       0.009354347  0.6388889 0.014641586 2.500387    92
    ## [42]  {butter,                                                                                           
    ##        root vegetables}           => {whole milk}       0.008235892  0.6377953 0.012913066 2.496107    81
    ## [43]  {curd,                                                                                             
    ##        tropical fruit}            => {whole milk}       0.006507372  0.6336634 0.010269446 2.479936    64
    ## [44]  {other vegetables,                                                                                 
    ##        pip fruit,                                                                                        
    ##        yogurt}                    => {whole milk}       0.005083884  0.6250000 0.008134215 2.446031    50
    ## [45]  {domestic eggs,                                                                                    
    ##        pip fruit}                 => {whole milk}       0.005388917  0.6235294 0.008642603 2.440275    53
    ## [46]  {butter,                                                                                           
    ##        tropical fruit}            => {whole milk}       0.006202339  0.6224490 0.009964413 2.436047    61
    ## [47]  {domestic eggs,                                                                                    
    ##        margarine}                 => {whole milk}       0.005185562  0.6219512 0.008337570 2.434099    51
    ## [48]  {butter,                                                                                           
    ##        domestic eggs}             => {whole milk}       0.005998983  0.6210526 0.009659380 2.430582    59
    ## [49]  {other vegetables,                                                                                 
    ##        tropical fruit,                                                                                   
    ##        yogurt}                    => {whole milk}       0.007625826  0.6198347 0.012302999 2.425816    75
    ## [50]  {fruit/vegetable juice,                                                                            
    ##        other vegetables,                                                                                 
    ##        yogurt}                    => {whole milk}       0.005083884  0.6172840 0.008235892 2.415833    50
    ## [51]  {domestic eggs,                                                                                    
    ##        tropical fruit}            => {whole milk}       0.006914082  0.6071429 0.011387900 2.376144    68
    ## [52]  {other vegetables,                                                                                 
    ##        root vegetables,                                                                                  
    ##        whipped/sour cream}        => {whole milk}       0.005185562  0.6071429 0.008540925 2.376144    51
    ## [53]  {other vegetables,                                                                                 
    ##        root vegetables,                                                                                  
    ##        yogurt}                    => {whole milk}       0.007829181  0.6062992 0.012913066 2.372842    77
    ## [54]  {bottled water,                                                                                    
    ##        butter}                    => {whole milk}       0.005388917  0.6022727 0.008947636 2.357084    53
    ## [55]  {domestic eggs,                                                                                    
    ##        root vegetables}           => {whole milk}       0.008540925  0.5957447 0.014336553 2.331536    84
    ## [56]  {curd,                                                                                             
    ##        rolls/buns}                => {whole milk}       0.005897306  0.5858586 0.010066090 2.292845    58
    ## [57]  {other vegetables,                                                                                 
    ##        sugar}                     => {whole milk}       0.006304016  0.5849057 0.010777834 2.289115    62
    ## [58]  {curd,                                                                                             
    ##        yogurt}                    => {whole milk}       0.010066090  0.5823529 0.017285206 2.279125    99
    ## [59]  {citrus fruit,                                                                                     
    ##        whipped/sour cream}        => {whole milk}       0.006304016  0.5794393 0.010879512 2.267722    62
    ## [60]  {pip fruit,                                                                                        
    ##        root vegetables}           => {whole milk}       0.008947636  0.5751634 0.015556685 2.250988    88
    ## [61]  {curd,                                                                                             
    ##        other vegetables}          => {whole milk}       0.009862735  0.5739645 0.017183528 2.246296    97
    ## [62]  {butter,                                                                                           
    ##        other vegetables}          => {whole milk}       0.011489578  0.5736041 0.020030503 2.244885   113
    ## [63]  {tropical fruit,                                                                                   
    ##        whipped/sour cream}        => {whole milk}       0.007930859  0.5735294 0.013828165 2.244593    78
    ## [64]  {domestic eggs,                                                                                    
    ##        whipped/sour cream}        => {whole milk}       0.005693950  0.5714286 0.009964413 2.236371    56
    ## [65]  {other vegetables,                                                                                 
    ##        root vegetables,                                                                                  
    ##        tropical fruit}            => {whole milk}       0.007015760  0.5702479 0.012302999 2.231750    69
    ## [66]  {curd,                                                                                             
    ##        root vegetables}           => {whole milk}       0.006202339  0.5700935 0.010879512 2.231146    61
    ## [67]  {root vegetables,                                                                                  
    ##        tropical fruit}            => {whole milk}       0.011997966  0.5700483 0.021047280 2.230969   118
    ## [68]  {curd,                                                                                             
    ##        whipped/sour cream}        => {whole milk}       0.005897306  0.5631068 0.010472801 2.203802    58
    ## [69]  {root vegetables,                                                                                  
    ##        yogurt}                    => {whole milk}       0.014539908  0.5629921 0.025826131 2.203354   143
    ## [70]  {sausage,                                                                                          
    ##        whipped/sour cream}        => {whole milk}       0.005083884  0.5617978 0.009049314 2.198679    50
    ## [71]  {bottled beer,                                                                                     
    ##        yogurt}                    => {whole milk}       0.005185562  0.5604396 0.009252669 2.193364    51
    ## [72]  {brown bread,                                                                                      
    ##        root vegetables}           => {whole milk}       0.005693950  0.5600000 0.010167768 2.191643    56
    ## [73]  {citrus fruit,                                                                                     
    ##        other vegetables,                                                                                 
    ##        root vegetables}           => {whole milk}       0.005795628  0.5588235 0.010371124 2.187039    57
    ## [74]  {butter,                                                                                           
    ##        citrus fruit}              => {whole milk}       0.005083884  0.5555556 0.009150991 2.174249    50
    ## [75]  {frankfurter,                                                                                      
    ##        yogurt}                    => {whole milk}       0.006202339  0.5545455 0.011184545 2.170296    61
    ## [76]  {root vegetables,                                                                                  
    ##        whipped/sour cream}        => {whole milk}       0.009456024  0.5535714 0.017081851 2.166484    93
    ## [77]  {domestic eggs,                                                                                    
    ##        other vegetables}          => {whole milk}       0.012302999  0.5525114 0.022267412 2.162336   121
    ## [78]  {chicken,                                                                                          
    ##        root vegetables}           => {whole milk}       0.005998983  0.5514019 0.010879512 2.157993    59
    ## [79]  {other vegetables,                                                                                 
    ##        whipped/sour cream,                                                                               
    ##        yogurt}                    => {whole milk}       0.005592272  0.5500000 0.010167768 2.152507    55
    ## [80]  {pork,                                                                                             
    ##        rolls/buns}                => {whole milk}       0.006202339  0.5495495 0.011286223 2.150744    61
    ## [81]  {citrus fruit,                                                                                     
    ##        domestic eggs}             => {whole milk}       0.005693950  0.5490196 0.010371124 2.148670    56
    ## [82]  {frankfurter,                                                                                      
    ##        tropical fruit}            => {whole milk}       0.005185562  0.5483871 0.009456024 2.146195    51
    ## [83]  {chicken,                                                                                          
    ##        rolls/buns}                => {whole milk}       0.005287239  0.5473684 0.009659380 2.142208    52
    ## [84]  {frozen vegetables,                                                                                
    ##        other vegetables}          => {whole milk}       0.009659380  0.5428571 0.017793594 2.124552    95
    ## [85]  {hygiene articles,                                                                                 
    ##        other vegetables}          => {whole milk}       0.005185562  0.5425532 0.009557702 2.123363    51
    ## [86]  {fruit/vegetable juice,                                                                            
    ##        root vegetables}           => {whole milk}       0.006507372  0.5423729 0.011997966 2.122657    64
    ## [87]  {domestic eggs,                                                                                    
    ##        yogurt}                    => {whole milk}       0.007727504  0.5390071 0.014336553 2.109485    76
    ## [88]  {margarine,                                                                                        
    ##        rolls/buns}                => {whole milk}       0.007930859  0.5379310 0.014743264 2.105273    78
    ## [89]  {frozen vegetables,                                                                                
    ##        root vegetables}           => {whole milk}       0.006202339  0.5350877 0.011591256 2.094146    61
    ## [90]  {rolls/buns,                                                                                       
    ##        whipped/sour cream}        => {whole milk}       0.007829181  0.5347222 0.014641586 2.092715    77
    ## [91]  {long life bakery product,                                                                         
    ##        other vegetables}          => {whole milk}       0.005693950  0.5333333 0.010676157 2.087279    56
    ## [92]  {brown bread,                                                                                      
    ##        tropical fruit}            => {whole milk}       0.005693950  0.5333333 0.010676157 2.087279    56
    ## [93]  {cream cheese ,                                                                                    
    ##        yogurt}                    => {whole milk}       0.006609049  0.5327869 0.012404677 2.085141    65
    ## [94]  {pip fruit,                                                                                        
    ##        yogurt}                    => {whole milk}       0.009557702  0.5310734 0.017996950 2.078435    94
    ## [95]  {whipped/sour cream,                                                                               
    ##        yogurt}                    => {whole milk}       0.010879512  0.5245098 0.020742247 2.052747   107
    ## [96]  {rolls/buns,                                                                                       
    ##        root vegetables}           => {whole milk}       0.012709710  0.5230126 0.024300966 2.046888   125
    ## [97]  {other vegetables,                                                                                 
    ##        rolls/buns,                                                                                       
    ##        yogurt}                    => {whole milk}       0.005998983  0.5221239 0.011489578 2.043410    59
    ## [98]  {beef,                                                                                             
    ##        yogurt}                    => {whole milk}       0.006100661  0.5217391 0.011692933 2.041904    60
    ## [99]  {coffee,                                                                                           
    ##        yogurt}                    => {whole milk}       0.005083884  0.5208333 0.009761057 2.038359    50
    ## [100] {pip fruit,                                                                                        
    ##        sausage}                   => {whole milk}       0.005592272  0.5188679 0.010777834 2.030667    55
    ## [101] {pastry,                                                                                           
    ##        root vegetables}           => {whole milk}       0.005693950  0.5185185 0.010981190 2.029299    56
    ## [102] {sausage,                                                                                          
    ##        tropical fruit}            => {whole milk}       0.007219115  0.5182482 0.013929842 2.028241    71
    ## [103] {other vegetables,                                                                                 
    ##        pip fruit}                 => {whole milk}       0.013523132  0.5175097 0.026131164 2.025351   133
    ## [104] {tropical fruit,                                                                                   
    ##        yogurt}                    => {whole milk}       0.015149975  0.5173611 0.029283172 2.024770   149
    ## [105] {pastry,                                                                                           
    ##        yogurt}                    => {whole milk}       0.009150991  0.5172414 0.017691917 2.024301    90
    ## [106] {citrus fruit,                                                                                     
    ##        root vegetables}           => {whole milk}       0.009150991  0.5172414 0.017691917 2.024301    90
    ## [107] {root vegetables,                                                                                  
    ##        sausage}                   => {whole milk}       0.007727504  0.5170068 0.014946619 2.023383    76
    ## [108] {other vegetables,                                                                                 
    ##        yogurt}                    => {whole milk}       0.022267412  0.5128806 0.043416370 2.007235   219

Plot of all the rules in (support, confidence) space

    ## To reduce overplotting, jitter is added! Use jitter = 0 to prevent jitter.

![](HW4_Albert_Joe_files/figure-markdown_strict/unnamed-chunk-2-1.png)
Two-key plot: coloring is by size of item set.

    ## To reduce overplotting, jitter is added! Use jitter = 0 to prevent jitter.

![](HW4_Albert_Joe_files/figure-markdown_strict/unnamed-chunk-3-1.png)
