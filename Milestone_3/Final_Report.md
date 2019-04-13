Final Report
================

## Introduction

Our study explores the relationship between a person’s level of
education prior to Master’s of Data Science and their overall
satisfaction of the program. Three potential confounders have been
determined and measured: sex, age and previous STEM background. All
variables are categorical to preserve some level of anoynmity; their
specificities can be viewed below. The analysis will be conducted with
GLM with poisson and ANOVA. These two models would show any variable
level differences as well as differences of categories within variables
if any is to be found. These two models together would be sufficient in
determining the effect of the predictor on the
response.

| sex    | age   | satisfaction | primary\_language | level\_education | STEM | Years\_off\_school |
| :----- | :---- | :----------- | :---------------- | :--------------- | :--- | :----------------- |
| Male   | 26-30 | very happy   | English           | Bachelors        | No   | 3-5                |
| Female | 21-25 | happy        | English           | Masters+         | Yes  | 0-2                |
| Male   | 21-25 | happy        | English           | Bachelors        | Yes  | 0-2                |
| Male   | 26-30 | happy        | English           | Bachelors        | Yes  | 3-5                |
| Male   | 26-30 | happy        | English           | Bachelors        | Yes  | 3-5                |
| Male   | 21-25 | okay         | English           | Bachelors        | Yes  | 0-2                |

Survey Data

## Overall Summary

#### The interaction between predictor and response

``` r
# data_sub
model_og <- glm(satisfaction_level ~ level_education, data = data_sub, family = 'poisson')
summary(model_og)
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

Very naively, we see from the glm output that there is not a significant
difference in people’s satisfaction of MDS between having a bachelors vs
masters or higher education. We recognize that Ordinal Linear Regression
is the better choice for model fitting, but within-function and
environment variable interactions in R prevented us from using `olr`
package further down in our analysis. Thus we made a conscious decision
to use GLM with poisson
assumption.

#### The interaction between predictor, confounder and response

``` r
model_overall <- glm(satisfaction_level ~ sex + age + level_education + STEM, data = data_sub, family = 'poisson')
summary(model_overall)
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

A little less naively and accounting for potential confounders, there
still is not a significant difference in people’s satisfaction of MDS
between having a bachelors vs masters or higher education.
Interestingly, we can see Simpson’s Paradox at play here with `Masters+`
having a negative relationship now, albeit very slightly, with respect
to the base case.

#### Anova

``` r
Anova(model_overall)
```

    ## Analysis of Deviance Table (Type II tests)
    ## 
    ## Response: satisfaction_level
    ##                 LR Chisq Df Pr(>Chisq)
    ## sex              0.08890  2     0.9565
    ## age              0.91904  3     0.8208
    ## level_education  0.00136  1     0.9706
    ## STEM             0.17516  1     0.6756

Type II ANOVA is used here because the model does not contain any
interactions. This test makes variable level comparisons about the level
of education as a whole. The ANOVA table confirms that there is not a
significant difference between the full model without `level_education`
and the full model with `level_education`. The confounders are also not
impactful to the point that they are significant.

## Confounders

#### Age

We first explore the interaction between the age and our predictor of
interest.

``` r
summary(model_og)
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

``` r
confint(model_og)
```

    ## Waiting for profiling to be done...

    ##                              2.5 %    97.5 %
    ## (Intercept)              0.8723036 1.1662907
    ## level_educationMasters+ -0.2907199 0.3431285

``` r
summary(glm(satisfaction_level ~ level_education + age, data = data_sub, family = 'poisson'))
```

    ## 
    ## Call:
    ## glm(formula = satisfaction_level ~ level_education + age, family = "poisson", 
    ##     data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.42538  -0.08884   0.18138   0.19408   0.59872  
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)              0.992034   0.103266   9.607   <2e-16 ***
    ## level_educationMasters+ -0.007604   0.170630  -0.045    0.964    
    ## age26-30                 0.086795   0.148057   0.586    0.558    
    ## age31-35                -0.103648   0.262982  -0.394    0.693    
    ## age35+                   0.157436   0.248803   0.633    0.527    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 34.316  on 80  degrees of freedom
    ## Residual deviance: 33.326  on 76  degrees of freedom
    ## AIC: 270.59
    ## 
    ## Number of Fisher Scoring iterations: 4

As we can observe from the regression estimates, age does seem to be a
confounder as it changes the estimate on our predictor. Although the
change is still within our confidence interval, so the confounding
effect is not very large.

#### Sex

We discover a much weaker relationship for `sex` as a confounding
variable.

``` r
summary(model_og)
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

``` r
confint(model_og)
```

    ## Waiting for profiling to be done...

    ##                              2.5 %    97.5 %
    ## (Intercept)              0.8723036 1.1662907
    ## level_educationMasters+ -0.2907199 0.3431285

``` r
summary(glm(satisfaction_level ~ level_education + sex, data = data_sub, family = 'poisson'))
```

    ## 
    ## Call:
    ## glm(formula = satisfaction_level ~ level_education + sex, family = "poisson", 
    ##     data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.36745   0.03527   0.11669   0.15027   0.70718  
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)               1.0106     0.1089   9.280   <2e-16 ***
    ## level_educationMasters+   0.0305     0.1657   0.184    0.854    
    ## sexMale                   0.0199     0.1368   0.145    0.884    
    ## sexOthers                 0.0676     0.3572   0.189    0.850    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 34.316  on 80  degrees of freedom
    ## Residual deviance: 34.221  on 77  degrees of freedom
    ## AIC: 269.49
    ## 
    ## Number of Fisher Scoring iterations: 4

#### STEM

We discover `STEM` as a confounding variable as well but not to the same
degree of impactfulness as `age`.

``` r
summary(model_og)
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

``` r
confint(model_og)
```

    ## Waiting for profiling to be done...

    ##                              2.5 %    97.5 %
    ## (Intercept)              0.8723036 1.1662907
    ## level_educationMasters+ -0.2907199 0.3431285

``` r
summary(glm(satisfaction_level ~ level_education + STEM, data = data_sub, family = 'poisson'))
```

    ## 
    ## Call:
    ## glm(formula = satisfaction_level ~ level_education + STEM, family = "poisson", 
    ##     data = data_sub)
    ## 
    ## Deviance Residuals: 
    ##      Min        1Q    Median        3Q       Max  
    ## -2.33364  -0.08322   0.16518   0.16518   0.72287  
    ## 
    ## Coefficients:
    ##                         Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)              1.09512    0.14951   7.325 2.39e-13 ***
    ## level_educationMasters+  0.05116    0.16390   0.312    0.755    
    ## STEMYes                 -0.09341    0.16914  -0.552    0.581    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 34.316  on 80  degrees of freedom
    ## Residual deviance: 33.968  on 78  degrees of freedom
    ## AIC: 267.24
    ## 
    ## Number of Fisher Scoring iterations: 4

## Results

Our analysis found no indication that the level of education one has
prior to attending MDS is associated with their satisfaction of the
program. In order to derive the role of the predictor on the response in
its purest form, we collected potential confounders: age, sex and
previous STEM degree. These three variables are all plausible in having
an effect on both the predictor and response variables. Although none of
them are actually significant as shown through our ANOVA analysis, they
all have varying effects that cannot be entirely excluded. Overall
`age`, `STEM` and `sex` had a decreasing level of impact with `age`
being the strongest confounder.

There are pros and cons with our approach to our first observational
study. We did well in making this study as causal as possible by
adhering to sound statistical procedures during the analysis phase. We
made sure each step in our model making decision is justified and
intentional. A good example of this includes using GLM instead of
Ordinal Linear Regression even though the latter is more logical in this
case; environment variable interactions in R prevented us from using the
newer `olr` package. The decision to use Type II ANOVA and GLM t-tests
to double check results is another example.

However, being the pilot study, there were mistakes on many fronts in
terms of experimental design and implementation. Most egregiously, we
made the very amateur mistake of posting the same link to our Slack
channel twice resulting in a survey participation much greater than our
classroom population. This failure in data collection could very well
have doomed our analysis right from the beginning. Due to potential
decline in social reputation, we did not ask our class to partake in our
survey a third time. A more serious shortcoming is that our initial
experimental design was not centered on a single predictive variable and
its potential confounders but based instead on collecting a host of
related variables with the expectation of performing ANOVA to determine
the true predictive variable post-hoc during the analytical phase. This
is fundamentally not a causal study. We made revisions to our initial
proposal upon realizing this but that was post data collection. And
therefore the effect of poor framing on our study conclusion is also
non-insignificant. A causal study does not inherently involve fancier
tests or advanced analysis, it is more determined during the
experimental setup. In a future study, we would like to clearly identify
a likely predictor and then framing around this predictor its potential
confounders. Only by being rigorous and testing a very specific
hypothesis can a direct causal relationship be established. Although
there are limitations for observational studies at our current level of
education, our analysis would benefit immensely from carrying out a
cleaner, more methodical experimental setup.
