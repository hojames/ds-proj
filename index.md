---
title: Understanding Recent Life Expectancy Declines in the United States through Exploratory Data Analysis & Principal Component Analysis
---

## Project Site Outline:
1. Overview (embed screencast here?)
2. Related Work for Motivation/Inspiration (links to relevant articles)
3. Initial Research Questions
4. Data
5. Relevant EDA
6. Final Analysis
7. Summarizing Conclusions

### Motivation
We are interested in exploring domestic health policy through the lens of county-level health rankings, mortality data, and other relevant determinants of health. Across the United States, there is broad diversity and variation in health status, access to care, and health outcomes. 

![Alt Text](/web_image/US_LE_motivation.jpg)

We are curious about the decline of life expectancy in the US (for the first time since the 1990s), and which groups of people (by location, race, income level, or other factors) experienced different changes in mortality and by what cause of death. This analysis could provide insights that could guide targeted health interventions for specific communities in the US. 

### Related Work
As we embarked on this project, we found that we weren't the only ones interested in exploring disparities in life expectancy/determinants of health at the county level. Some previous work that helped to guide our project development is below:
- [35 Years of Death, via 538](https://projects.fivethirtyeight.com/mortality-rates-united-states/)
- [Article Summarizing New Findings, via 538](https://fivethirtyeight.com/features/how-americans-die-may-depend-on-where-they-live/)
  - Cardiovascular disease strongly impacts health in Appalachia and Southern regions of United States
  - [Death rates are rising for middle age whites](https://www.nytimes.com/2015/11/03/health/death-rates-rising-for-middle-aged-white-americans-study-finds.html)
  - [Increased vehicle deaths in rural areas/longer distances to ERs](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1448517/)
  - [Self harm in Western states](https://fivethirtyeight.com/features/suicide-in-wyoming/)
  - [Self harm data masking violence deaths](http://www.nytimes.com/2016/12/10/opinion/sunday/violence-and-division-on-chicagos-south-side.html)
  - Existence of garbage codes: useless codes and ambiguous death causes

### Sources for Data Analysis:
For this project, we used the following data sources (all open access!):  
  [US county health rankings](https://www.rwjf.org/en/how-we-work/grants-explorer/featured-programs/county-health-ranking-roadmap.html)  
  [US county-level mortality data](https://www.kaggle.com/IHME/us-countylevel-mortality)

### Project Development
We wanted to dive further into mortality and attempt to understand the factors that contribute to high mortality rates in certain counties. With this in mind, we were curious about performing [Principal Component Analysis (PCA) for mortality](https://academic.oup.com/heapol/article/21/6/459/612115). We found other literature where this method had been employed to understand [mortality in developing countries](https://www.ncbi.nlm.nih.gov/pubmed/12311007), [cardiovascular deaths among Native Americans](https://www.ncbi.nlm.nih.gov/pubmed/11839627), and [malaria cases in Ghana](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2914064/).

Research Questions:
1. Can we use PCA to understand the dominating factors that drive county-level mortality rates in the United States?
2. Can applying PCA help to inform trends in mortality rates at the county level that can be used to tailor context-specific interventions?

### Exploratory Analysis of Mortality Rates and Health Rankings:
In order to get a better understanding of where the most serious decline in life expectancy from 2010 to 2014 is happening in the U.S., we used the below code to generate the list of counties with the largest decrease in life expectancy.

![Alt Text](/web_image/top10_change.jpg)

While the above exploratory analysis is interesting, we decided that it would be more interesting to look at the states as a whole. There could be large outliers within each state with life expectancy and we didn't want our data to be skewed by such outliers. So, we asked the question, "which state had the largest decline in life expectancy during this same time period?"" 

![Alt Text](/web_image/top10_state.jpg)

From the above output, both Mississippi and West Virginia had the largest decline in life expectancy (-0.04 years) from 2010-2011. We decided to then do the rest of our analysis using these two states. 

Going back to the county level, we wanted to check what the range of change in life expectancy was during this time period in each state. What percent of counties had a decline in life expectancy compared to an increase? 

![Alt Text](/web_image/change_in_le.jpg)

We can see from the graphs above that there were quite a few counties that had a decline in life expectancy. There were exactly 55 out of 82 counties in Mississippi that had negative changes in life expectancy. There were exactly 34 out of 55 counties in West Virginia that had negative changes in life expectancy. 

The above exploration caused us to want to look at the all cause mortality rates in these two states. We assume that with a decline in life expectancy that we would see an increase in cause mortality.  

![Alt Text](/web_image/all_cause_mort.jpg)

This graph above shows that both West Virginia and Mississippi demonstrated an increase in all cause mortality rates, which corroborates our findings in our life expectancy decline exploration. 

We did notice, however, that it is difficult to judge how these two states differ from the rest of the country. The y axis all cause mortality ranges from 980 - 1040, which is not a large gap contrary to what it looks like visually. We decided we needed a reference state to compare our two states to. We picked Hawaii, which had the highest life expectancy in 2014. 

![Alt Text](/web_image/all_cause_incHI.jpg)

We can now see that West Virginia and Mississippi had very similar trends in all cause mortality rates and that Hawaii, the state with the highest life expectancy, had a much lower all cause mortality rates throughout the five years of data. It is important in these types of graphs to have a reference category to compare to in order not to draw false inferences. 

Next, we wanted to see how life expectancy decline and the County Health Rankings (CHR) compared to each other. How did the county with the largest decrease in life expectancy fare in CHR?  
-In Mississippi, Grenada County ranked 49th in 2011, and 51st in 2015 out of 55 counties in the state.
-In West Virginia, Logan Country ranked 54th in 2013 and 51st in 2015 out of 82 counties in the state. 

### Principal Component Analysis
We continue to study the determinants of declines in life expectancy in Mississippi and West Virginia through Principal Component Analysis. We faced a limitation due to missing data, but we were able to replace missing values with 0 (because we were using standardized z-scores, so 0 would be the mean).

In Mississippi:

![Alt Text](/web_image/ms_pca.jpg)  
From our summary of PCA for health factors in Missisippi, we see that the first PC accounts for 27.25% of variance. If we wanted to use four components, like the four fous areas that the CHR currently uses, then we would account for 54.7% of total variance. We would need 8 PCs to get to 71%, 11 to get to 80%, and 16 to get to 90%. At 16 PCs, it would be very difficult to keep track of 16 domains for something like the County Health Rankings, and even at 8 it is still unwieldly. Perhaps we should focus on a smaller number of components, but consider what each component is trying to tell us and also try the 'rule of 1' when looking at a scree plot. 

Let's look at the loadings on the first four PCs:
![Alt Text](/web_image/ms_pc1.jpg)  

For the first principal component, we see that there is positive loadings for several measures in the Social and Economic Environment factor. They include child poverty, children in single-parent households, and unemployment. This could perhaps be interpreted as growing up poor. Then, the next three heights weights come from adult obesity, STIs, and teen births. Could this be interpreted as risky or non-healthy behavior? The following highest weights are inadequate social support, physical inactivity, housing problems, violent crime, and injury deaths -- suggesting unsafe neighborhoods and poor social networks. Finally, the smallest positive weights come from being uninsured, preventable hospital stays, alcohol impaired driving deaths, rinking water violations, and adult smoking. There is a theme, again, of risky behaviors. THe financial aspect may be telling of the inability to account for risky contexts and behaviors. 

For the negative weights, being above average in having adequate food, education, preventive behavior, having physicians within distance, exercise opportunities, all point to having better health. 

We might name this context, resource-dependent risk behaviors?

![Alt Text](/web_image/ms_pc2.jpg) 

Access to providers, education, crime (?), exercise opportunities, housing issues, STIs, single-parent households, illustrate those who have access to resources but may live in urbn areas? Density of providers and access to things, but high crime, high rates of infection, and single parent house holds. The urban element? 

![Alt Text](/web_image/ms_pc3.jpg) 

Preventative care.

![Alt Text](/web_image/ms_pc4.jpg) 

Rural areas. 

Weights are constructed with the percent of variance each PC accounts for divided by the total amount of variance the chosen PCs account for.

![Alt Text](/web_image/weights_pc.jpg) 

The weights are 0.319 for F1, 0.292 for F2, 0.115 for F3, and 0.097 for F4.

### Conclusions

