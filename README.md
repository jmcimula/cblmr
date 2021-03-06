#cblmr

The choice of the best linear model **(cblmr)**

Choosing the correct linear regression model can be difficult. After all, the world and how it works is complex. Let's make the evaluation based on predictions (PRESS : Prediction Sum of Squares) and goodness of fit (AIC, BIC, R Squared, Adj. Squared) to mathematically describe the relationship between some predictors and the response variable

## Installation

You can install cblmr from github with:

```R
# install.packages("devtools")
devtools::install_github("jmcimula/cblmr")
```

## Key functions

* `blm_choice()`: generate all combinatations and values

## Example 

``` r
library(cblmr) # for functions

>df <- mtcars[,c(1,2,3,4,5,6)]
>str(df)
#'data.frame':   32 obs. of  6 variables:
# $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
# $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
# $ disp: num  160 160 108 258 360 ...
# $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
# $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
# $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...

>x <- blm_choice(df,"mpg")
>knitr::kable(x)

#|reg_model                         | r_squared| adj_r_squared|      AIC|      BIC|    PRESS|    Ridge|    Lasso| ElasticNet|       Cp|
#|:---------------------------------|---------:|-------------:|--------:|--------:|--------:|--------:|--------:|----------:|--------:|
#|mpg ~ cyl                         | 0.7261800|     0.7170527| 169.3064| 173.7036| 358.6699| 0.000000| 0.000000|   0.000000| 0.000000|
#|mpg ~ disp                        | 0.7183433|     0.7089548| 170.2094| 174.6066| 365.8296| 0.000000| 0.000000|   0.000000| 0.000000|
#|mpg ~ hp                          | 0.6024373|     0.5891853| 181.2386| 185.6358| 552.1057| 0.000000| 0.000000|   0.000000| 0.000000|
#|mpg ~ drat                        | 0.4639952|     0.4461283| 190.7999| 195.1971| 680.8646| 0.000000| 0.000000|   0.000000| 0.000000|
#|mpg ~ wt                          | 0.7528328|     0.7445939| 166.0294| 170.4266| 328.0228| 0.000000| 0.000000|   0.000000| 0.000000|
#|mpg ~ cyl + disp                  | 0.7595658|     0.7429841| 167.1456| 173.0086| 326.4631| 8.460639| 8.460634|   8.460639| 3.000000|
#|mpg ~ cyl + hp                    | 0.7407084|     0.7228263| 169.5618| 175.4248| 361.7400| 9.124205| 9.124205|   9.124205| 2.624905|
#|mpg ~ cyl + drat                  | 0.7402482|     0.7223343| 169.6186| 175.4815| 351.8657| 9.140400| 9.140399|   9.140400| 2.570645|
#|mpg ~ cyl + wt                    | 0.8302274|     0.8185189| 156.0101| 161.8730| 236.0464| 5.974125| 5.974124|   5.974125| 3.000000|
#|mpg ~ disp + hp                   | 0.7482402|     0.7308774| 168.6186| 174.4815| 343.9581| 8.859170| 8.859170|   8.859171| 3.000000|
#|mpg ~ disp + drat                 | 0.7310094|     0.7124583| 170.7370| 176.5999| 359.4462| 9.465503| 9.465503|   9.465504| 2.365534|
#|mpg ~ disp + wt                   | 0.7809306|     0.7658223| 164.1678| 170.0307| 309.3015| 7.708834| 7.708828|   7.708833| 3.000000|
#|mpg ~ hp + drat                   | 0.7411716|     0.7233214| 169.5046| 175.3676| 360.8955| 9.107906| 9.107906|   9.107907| 3.000000|
#|mpg ~ hp + wt                     | 0.8267855|     0.8148396| 156.6523| 162.5153| 246.5063| 6.095243| 6.095242|   6.095243| 3.000000|
#|mpg ~ drat + wt                   | 0.7608970|     0.7444071| 166.9680| 172.8309| 332.8069| 8.413793| 8.413790|   8.413792| 1.978077|
#|mpg ~ cyl + disp + hp             | 0.7678877|     0.7430186| 168.0184| 175.3471| 329.2441| 8.167794| 8.167792|   8.167795| 3.003890|
#|mpg ~ cyl + disp + drat           | 0.7650941|     0.7399256| 168.4013| 175.7300| 328.9349| 8.266103| 8.266099|   8.266103| 2.658952|
#|mpg ~ cyl + disp + wt             | 0.8326070|     0.8146721| 157.5584| 164.8870| 242.6426| 5.890415| 5.890387|   5.890440| 2.398045|
#|mpg ~ cyl + hp + drat             | 0.7693992|     0.7446920| 167.8094| 175.1380| 339.6572| 8.114608| 8.114604|   8.114609| 4.000000|
#|mpg ~ cyl + hp + wt               | 0.8431500|     0.8263446| 155.4766| 162.8053| 230.0767| 5.519393| 5.519391|   5.519393| 4.000000|
#|mpg ~ cyl + drat + wt             | 0.8302283|     0.8120385| 158.0099| 165.3386| 247.5664| 5.974093| 5.974092|   5.974096| 2.000150|
#|mpg ~ disp + hp + drat            | 0.7750131|     0.7509073| 167.0207| 174.3494| 321.3138| 7.917062| 7.917059|   7.917062| 4.000000|
#|mpg ~ disp + hp + wt              | 0.8268361|     0.8082829| 158.6430| 165.9717| 261.3609| 6.093473| 6.093459|   6.093468| 2.008196|
#|mpg ~ disp + drat + wt            | 0.7835315|     0.7603385| 165.7856| 173.1143| 325.3466| 7.617311| 7.617304|   7.617309| 2.336429|
#|mpg ~ hp + drat + wt              | 0.8368791|     0.8194018| 156.7311| 164.0598| 245.8972| 5.740060| 5.740059|   5.740060| 3.732584|
#|mpg ~ cyl + disp + hp + drat      | 0.7825119|     0.7502914| 167.9360| 176.7304| 327.8762| 7.653193| 7.653185|   7.653194| 3.848634|
#|mpg ~ cyl + disp + hp + wt        | 0.8486348|     0.8262103| 156.3376| 165.1320| 234.8245| 5.326389| 5.326386|   5.326390| 3.978361|
#|mpg ~ cyl + disp + drat + wt      | 0.8326074|     0.8078085| 159.5583| 168.3527| 255.8151| 5.890399| 5.890373|   5.890434| 1.383891|
#|mpg ~ cyl + hp + drat + wt        | 0.8451439|     0.8222023| 157.0672| 165.8616| 239.9967| 5.449238| 5.449226|   5.449237| 3.347657|
#|mpg ~ disp + hp + drat + wt       | 0.8376289|     0.8135739| 158.5837| 167.3781| 265.6399| 5.713688| 6.827722|   5.713711| 2.803104|
#|mpg ~ cyl + disp + hp + drat + wt | 0.8513152|     0.8227219| 157.7659| 168.0260| 247.4323| 5.232081| 5.232066|   5.232085| 3.427820|

##number of expected combinations : 4

>x <- blm_choice(dataframe=df,response="mpg",exp.comb=4)
>knitr::kable(x)

#|reg_model                    | r_squared| adj_r_squared|      AIC|      BIC|    PRESS|    Ridge|    Lasso| ElasticNet|       Cp| nexp|
#|:----------------------------|---------:|-------------:|--------:|--------:|--------:|--------:|--------:|----------:|--------:|----:|
#|mpg ~ cyl + disp + hp + drat | 0.7825119|     0.7502914| 167.9360| 176.7304| 327.8762| 7.653193| 7.653185|   7.653194| 3.848634|    4|
#|mpg ~ cyl + disp + hp + wt   | 0.8486348|     0.8262103| 156.3376| 165.1320| 234.8245| 5.326389| 5.326386|   5.326390| 3.978361|    4|
#|mpg ~ cyl + disp + drat + wt | 0.8326074|     0.8078085| 159.5583| 168.3527| 255.8151| 5.890399| 5.890373|   5.890434| 1.383891|    4|
#|mpg ~ cyl + hp + drat + wt   | 0.8451439|     0.8222023| 157.0672| 165.8616| 239.9967| 5.449238| 5.449226|   5.449237| 3.347657|    4|
#|mpg ~ disp + hp + drat + wt  | 0.8376289|     0.8135739| 158.5837| 167.3781| 265.6399| 5.713688| 6.827722|   5.713711| 2.803104|    4|

##Choosing the best model from the combination of four (4) variables above

>x <- blm_choice(dataframe=df,response="mpg",exp.comb=4,choice=TRUE)
>knitr::kable(x)

#|reg_model                  | r_squared| adj_r_squared|      AIC|     BIC|    PRESS|    Ridge|    Lasso| ElasticNet|       Cp| nexp|
#|:--------------------------|---------:|-------------:|--------:|-------:|--------:|--------:|--------:|----------:|--------:|----:|
#|mpg ~ cyl + disp + hp + wt | 0.8486348|     0.8262103| 156.3376| 165.132| 234.8245| 5.326389| 5.326386|    5.32639| 3.978361|    4|
```

Regular R squared increases every time you add a predictor and can trick you into specifying an overly complex model. Unlike the case above, the number of predictors is predefined in the function. It's returned `mpg ~ cyl + disp + hp + wt` which implies the criteria of selection, namely max value of r.squared, adj.r.squared and  Mallows' Cp (which is a statistic specifically designed to help you manage the tradeoff between precision and bias.), and min vax of AIC, BIC , PRESS (Cross-validation determines how well your model generalizes to other data sets by partitioning your data), Ridge, Lasso (it enhances the prediction accuracy and interpretability of the statistical model it produces), Elasticnet

##Licence

GPL (>= 2)

### Author

Jean Marie Cimula
