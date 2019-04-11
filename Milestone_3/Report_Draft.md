Report Draft
================

## Overall Summary

#### The interaction between predictors and response

``` r
# data_sub
model_overall <- glm(satisfaction_level ~ level_education, data = data_sub, family = 'poisson')
summary(model_overall)
```

    ## 
    ## Call:
    ## glm(formula = satisfaction_level ~ level_education, family = "poisson", 
    ##     data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.35850   0.06883   0.12950   0.12950   0.68531  
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)              1.02290    0.07495  13.647   <2e-16 ***
    ## level_educationMasters+  0.03571    0.16133   0.221    0.825    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 34.316  on 80  degrees of freedom
    ## Residual deviance: 34.268  on 79  degrees of freedom
    ## AIC: 265.54
    ## 
    ## Number of Fisher Scoring iterations: 4

#### The interaction between predictor, confonder and response

``` r
model_overall_conf <- glm(satisfaction_level ~ sex + age + level_education + STEM, data = data_sub, family = 'poisson')
summary(model_overall_conf)
```

    ## 
    ## Call:
    ## glm(formula = satisfaction_level ~ sex + age + level_education + 
    ##     STEM, family = "poisson", data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.40336  -0.16582   0.09389   0.21809   0.62996  
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)              1.049514   0.181516   5.782 7.38e-09 ***
    ## sexMale                 -0.005601   0.140889  -0.040    0.968    
    ## sexOthers                0.105525   0.366422   0.288    0.773    
    ## age26-30                 0.089475   0.149293   0.599    0.549    
    ## age31-35                -0.112378   0.266672  -0.421    0.673    
    ## age35+                   0.155645   0.260735   0.597    0.551    
    ## level_educationMasters+ -0.006716   0.182241  -0.037    0.971    
    ## STEMYes                 -0.072797   0.172832  -0.421    0.674    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 34.316  on 80  degrees of freedom
    ## Residual deviance: 33.018  on 73  degrees of freedom
    ## AIC: 276.29
    ## 
    ## Number of Fisher Scoring iterations: 4

#### Anova

## Confonders vs. Predictor

#### Age

We first explore the interaction between the age and our predictor of
interest.

``` r
Visualization(data_sub, "age", "predictor")
```

    ## Joining, by = "conf"

![](Report_Draft_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

As we can observe from the EDA, different age group has distinct pattern
for the proportion distribution of its own education level. For older
people, they are intended to have master degree than yourger ones.
However, we want to explore these pattern are significantly unique based
on the hypothesis that **if age can significantly influence the
predictor as a confunder**. Given that hypothesis, we set the age lower
than 26 being the control group and there is no significant different
between different age groups given the
p-value.

``` r
m <- glm_reg(data = data_sub, mode = "predictor", conf = "age", output = "summary")
m
```

    ## 
    ## Call:
    ## glm(formula = above_bachelor ~ confonder, family = "poisson", 
    ##     data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.0690  -0.7184  -0.4714  -0.4714   1.6176  
    ## 
    ## Coefficients:
    ##                Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)     -2.1972     0.5000  -4.394 1.11e-05 ***
    ## confonder26-30   0.8427     0.6124   1.376   0.1688    
    ## confonder31-35   0.2513     1.1180   0.225   0.8221    
    ## confonder35+     1.6376     0.7071   2.316   0.0206 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 53.082  on 80  degrees of freedom
    ## Residual deviance: 47.619  on 77  degrees of freedom
    ## AIC: 89.619
    ## 
    ## Number of Fisher Scoring iterations: 6

#### Sex

We discover similar results in the sex
variable.

``` r
Visualization(data_sub, "sex", "predictor")
```

    ## Joining, by = "conf"

![](Report_Draft_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
m <- glm_reg(data = data_sub, mode = "predictor", conf = "age", output = "summary")
m
```

    ## 
    ## Call:
    ## glm(formula = above_bachelor ~ confonder, family = "poisson", 
    ##     data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.0690  -0.7184  -0.4714  -0.4714   1.6176  
    ## 
    ## Coefficients:
    ##                Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)     -2.1972     0.5000  -4.394 1.11e-05 ***
    ## confonder26-30   0.8427     0.6124   1.376   0.1688    
    ## confonder31-35   0.2513     1.1180   0.225   0.8221    
    ## confonder35+     1.6376     0.7071   2.316   0.0206 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 53.082  on 80  degrees of freedom
    ## Residual deviance: 47.619  on 77  degrees of freedom
    ## AIC: 89.619
    ## 
    ## Number of Fisher Scoring iterations: 6

#### STEM

``` r
Visualization(data_sub, "STEM", "predictor")
```

    ## Joining, by = "conf"

![](Report_Draft_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
m <- glm_reg(data = data_sub, mode = "predictor", conf = "STEM", output = "summary")
m
```

    ## 
    ## Call:
    ## glm(formula = above_bachelor ~ confonder, family = "poisson", 
    ##     data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -0.6963  -0.6963  -0.6963  -0.3651   1.8840  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)   
    ## (Intercept)    -2.708      1.000  -2.708  0.00677 **
    ## confonderYes    1.291      1.031   1.252  0.21041   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 53.082  on 80  degrees of freedom
    ## Residual deviance: 50.762  on 79  degrees of freedom
    ## AIC: 88.762
    ## 
    ## Number of Fisher Scoring iterations: 6
