
## Proposal
* The content is discussed among all team members and written by Arzan Irani

### Identify the question that your team in interested in answering with the survey. The aim of the survey should be to try to answer one specific and testable question. <br/>
<br/>

### Question of Interest

Does an MDS student’s academic background – prior to MDS – determine how satisfied they would be with the program?<br/>
<br/>
In order to investigate the above question, we would like to conduct a survey with questions and answers such as the following:<br/>
1. What is your level of satisfaction with the MDS program?
  * 5 ordinal levels (very unhappy, unhappy, okay, happy, very happy)
2. What is your primary language of communication (in all forms – speaking, reading, writing)?
  * English or other
3. What is your highest level of education prior to MDS?
  * Bachelors, Masters or higher (2 choices)
4. Was your highest level of education – prior to MDS - amongst the STEM (Science, Technology, Engineering and Mathematic) academic disciplines?
  * Yes or no
5. How many years ago was when you attained your highest level of education prior to MDS?
  * 0-2 years, 3-5 years, 5-10 years, 10+ years

### Identify the other questions you plan to ask in your survey to identify confounding variables and justify/explain why you plan to include them.
<br/>
Additionally, we would also like account for Gender and Age, as these might be confounding variables that might affect both the response variable (level of satisfaction with the MDS program) and certain explanatory variables, such as whether the individual chose a STEM related field because of their age or gender. Gender is chosen as a potential confounder because there is usually a gender disproportion in having previous STEM related experience. Age is also a confounder for level of education and year(s) since graduation. We should account for these variables in our survey to be able to determine the actual causal relationship in the downstream analysis.<br/>
<br/>

### Describe how you plan to analyze the survey results (e.g., what statistical test(s) do you plan to employ?).

### Analysis plan

<br/>
Exploratory data analysis (EDA) will be performed after we receive the raw data for the survey. Our hypothesis will be built by taking into considerations of visualizations.<br/>
<br/>
We would like to conduct one-way ANOVA tests to see whether any of the groups of our explanatory variables - (For example: For highest level of education we might have groups of Bachelors, Masters or higher) – have different levels of mean satisfaction with the MDS program. This would allow us to test whether any group(s) - of a particular explanatory variable - have a mean satisfaction that is statistically significant and different from the other groups i.e. being in a certain group of this explanatory variable has an effect on whether you will be satisfied with MDS.<br/>
<br/>
It is important to remember that the one-way ANOVA test simply tells us whether there is a difference of means between the groups and not which group(s) in particular can be considered as a predictor(s). Hence, for explanatory variables with more than two levels of categories/groups - like the years of graduation for highest level of education, which has fours groups – we would also have to conduct pair-wise t-tests in order to determine which categories/groups have a mean i.e. statistically different.<br/>
<br/>
At this stage of our analysis, we would also have to keep track of our degrees of freedom, while simultaneously being cognizant of the multiple comparisons and the possibility of Type 1 errors being introduced due to our significance (⍺) level. We could account for this by using the Bonferroni Adjustment which takes into account the Familywise Error Rate (FWER) or False Discovery Rate (FDR) based method such as the Benjamini-Hochberg (BH) procedure. <br/>
<br/>
Furthermore, we would also like to conduct two-way or 2-way ANOVA tests, time permitting, to check whether there are any pairs of our explanatory variables that exhibit main effects or interaction effects with other variables on the response variable. <br/>
<br/>
The idea of a main effect is that given the effect of our first variable, does the second variable (whose main effect we are measuring) still have a statistically significant effect on the mean satisfaction with MDS. Like with the one-way ANOVA tests, we would have to conduct pair-wise t-tests to determine which groups in particular had a statistically different mean from each other, and we would have to accommodate for multiple comparisons given that t-test have an ⍺ percentage or significance level percent chance of type-1 errors.<br/>
<br/>
Finally, the analysis results will be visualized and compared with our EDA at the beginning.<br/>
<br/>

### Research Ethics

Keeping in line with the UBC Office of Research Ethics document on Using Online Surveys, we have decided to not include any direct identifiers apart from serial numbers to identify the participants of our survey. This prevents us from collecting personal information such as a person’s name to identify them. We are also using groupings in our answer options to further preserve anonymity. In doing so, we prevent a person from being directly identified. <br/>
<br/>
However, since we are collecting personal information from our respondents we would require to use online survey tools that store the answers to our questions within Canada at a server. For this reason, we will use UBC-hosted version of Qualtrics, which is fully compliant with the BC Freedom of Information and Protection of Privacy Act (FIPPA) because the survey data is kept secure and is stored and backed up in Canada. <br/>
Under the FIPPA, “personal information” is defined as “recorded information about an identifiable individual other than contact information.” <br/>
<br/>
