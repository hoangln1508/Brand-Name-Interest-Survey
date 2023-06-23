# Brand-Name-Interest-Survey
## PART 1: DATASET OVERVIEW

This report aims to present the findings and evaluation outcomes derived from the dataset titled "Brand Name Interest Survey." The dataset encompasses valuable information concerning user interest and ratings pertaining to prominent brands and categories within the industry. To facilitate a comprehensive analysis, this report will be organized into distinct sections dedicated to specific industry assessments.

Throughout the analysis of the "Brand Name Interest Survey" dataset, various factors influencing consumer interest in brands and products have been identified and examined. Additionally, insightful trends pertaining to brand operations within the industry have been revealed. Building upon these insights, this report will offer valuable insights and recommendations to the industry regarding sales strategies and the effective allocation of investment capital.

## PART 2: ANALYSIS METHODS AND PROCEDURES
### Dataset Description

This dataset is a survey of 10,000 customers in 5 states in the US about their preferences, feedback, and overall evaluations of companies in many different industries. 

### Data Importing & Transforming
#### Data quality

- Total number of tables: 01
- Total line: 100,000
- Total number of columns: 20
- Number of columns with missing data: 02 (Interest Coefficient and Marketing Expense)
- Number of columns containing survey information: 04 (Participant ID, Age, Gender, Household Income)
- Number of columns containing other information about the surveyors: 01 (Interest Level)
- Number of columns containing information about the survey: 04 (Survey City; Survey State; Survey Date; Survey Zip)
- Number of columns containing brand information: 01 (Brand)
- Number of columns containing questions and survey results: 09

| No | Questions | 
|--------------|-------|
| 1 | What is your first reaction to the brand products? | 
| 2 | How would you rate the quality of this brand of products? |
| 3 | How innovative is this brand? | 
| 4             | When you think about the brand, do you think of it as something you need or don't need? |
| 5             | How would you rate the value for money of their products? |
| 6             | How likely would you be to try new products of this brand? |
| 7             | How likely are you to replace a current brand with this brand? |
| 8             | How likely is it that you would recommend new products from this brand to a friend or colleague? |

#### Data Transforming
##### Surveyors Information

Regarding surveyor information, I divide the age and income groups of surveyors into specific groups for analysis. First of all, they divided into 5 groups in terms of the age of survey participants, including Children (from 0 to 9 years old); Teenagers (from 10 to 19 years old); Adults (from 20 to 39 years old), Middle-aged (from 40 to 59 years old) and Elders (over 60 years old).

|Age| Age Group|
|--------------|-------|
|0-9| Children|
|10-19 |Teenager|
|20-39| Adults|
|40-59 |Middle-aged|
|60+ |Elder|

Regarding the income of survey participants, it is divided into 4 groups as follows: Low group (from $50k/year to $75k/year); Medium Low group (from $75k/year to $100k/year); Medium High group (from $100k/year to $125k/year) and High group (over $125k/year).

|Income |Income level|
|--------------|-------|
|50k-75k| Low|
|75k-100k| Medium Low|
|100k-125k| Medium High|
|>125k| High|

##### Survey Information
The survey was conducted in the following 5 states of the United States. The table below shows the names and initials of the surveyed states.
| State | In-short State |
|--------------|-------|
| PA | Pennsylvania| 
| NY | New York| 
| DC | Washington D.C| 
| VA | Virginia| 
| DE | Delaware| 

##### Brand and Industry Information

To facilitate the practical results, I divided 10 brands into 6 major industries as follows:

|Industry |Brand |
|--------------|-------|
|Automobile | Mercedes-Benz|
|Automobile | Toyota|
| Entertainment | Disney| 
|Food and beverage (F&B) | McDonalds |
|Food and beverage (F&B) | Coca|
| Retail | Amazon |
| Devices | Samsung|
| Devices | Apple |
|Technology |Google|
|Technology | Microsoft |

##### Survey Results

In order to facilitate convenient data analysis, I have shortened the names of the questions/answers from the survey. The shortened names are listed in the table below:

| Original Names | In-short Names|
|--------------|-------|
|What is your first reaction to the brand products? |First Impression|
|How would you rate the quality of this brand of products?| Quality Score|
|How innovative is this brand?| Innovative Score|
| When you think about the brand, do you think of it as something you need or don't need?| Necessity Score|
|How would you rate the value for money of their products? | Product Value|
|How likely would you be to try new products of this brand? |Trial Rate|
|How likely are you to replace a current brand with this brand? |Replaceability Risk|
|How likely is it that you would recommend new products from this brand to a friend or colleague?| Recommendation Level|

#### Data Modeling

Splitting and forming 03 main tables from the data table, including:
- Participant: creates separate tables for the characteristics of survey participants, including Age Group, Gender, Income
- Survey Results: The group is divided into 3 tables including Survey Date, Survey State, Survey ID
- Brand

![image](https://github.com/hoangln1508/Brand-Name-Interest-Survey/assets/136893356/ecdd15c8-4bf4-4f5b-8ae5-dfbc1fe8ac2c)

These tables are joined to the Participant table in a **one-to-many** relationship.

In the Participant table, in addition to primary keys and foreign keys of the other tables, I classify the surveyed people into Promote Type categories according to Recommended Level.

Regarding the Survey Results table, in addition to primary keys and foreign keys from other tables, I convert the answers from the survey question into numbers according to the available scale of each question as follows:

|Name| Scale Type|
|--------------|-------|
|First Impression |1-5|
|Innovative Score| 1-5|
|Necessity Score| 1-5|
|Product Value| 1-5|
|Quality Score |1-5|
|Recommend Level| 1-10|
|Trial Rate| 1-4|
|Replaceability Risk| 1-4|

In addition, I create DAXs that calculate metrics for analysis, including:
* Customer Satisfaction Score (CSAT)
* Net Promoter Score (NPS): Distractor; Passive and Promoter

The DAX formula is shown in the table below:
|Index Name| DAX |
|--------------|-------|
| CSAT | CSAT = DIVIDE(CALCULATE(COUNTROWS('Survey Results'), OR('Survey Results'[Quality Score]=4, 'Survey Results'[Quality Score]=5)), CALCULATE(COUNTROWS('Survey Results'), 'Survey Results'[Quality Score]))
| NPS | NPS Score = VAR _promoters = CALCULATE( COUNTROWS('Survey Results'), 'Survey Results'[Recommend Level] >= 9 ) VAR _detractors = CALCULATE( COUNTROWS('Survey Results'), 'Survey Results'[Recommend Level] <= 6 ) VAR _totalResponses = CALCULATE( COUNTROWS('Survey Results' ) ) RETURN DIVIDE( _promoters, _detractors, _totalResponses ) |

Using responses that are quantified on scales and metrics calculated by DAX, I analyze the data using the following dashboards:
1. Respondent General Information
2. Respondent Interest
3. Firm Performance
4. NPS Analysis

## PART 3: ANALYSIS RESULTS

### Dashboard 1: Respondent General Information

![image](https://github.com/hoangln1508/Brand-Name-Interest-Survey/assets/136893356/40dfc06b-9a32-486c-b6c9-3b0c54d66eac)

The dashboard provides an overview of the participants involved in the interviews, thus outlining the scope of the report's findings.

Regarding the gender distribution of the respondents, the survey encompassed a sample size of 10,000 participants, with 49.6% identified as male and 50.4% as female. The slight disparity in the number of male and female respondents is not statistically significant, ensuring the survey results remain objective.

The survey also considered the representation of different age groups to capture consumption patterns across various age demographics. Notably, the adult and middle-aged age groups were given particular attention as they represent the primary income-earning segments. Consequently, the majority of respondents fall into these categories, with adults comprising 34% and middle-aged individuals accounting for 33% of the total participants. The remaining participants were divided between teenagers and elders, each constituting 17% of the overall sample.

Income groups were also considered in the analysis, as mentioned earlier. The results demonstrate that a significant portion of survey participants belongs to low, middle, and high-income brackets, each comprising approximately 2,700 individuals. The low-income group represented a smaller proportion, with fewer than 1,000 respondents.

In terms of geographical distribution, the survey was conducted across five states: Pennsylvania, New York, Washington D.C, Virginia, and Delaware. Pennsylvania recorded the highest number of respondents, followed closely by New York with a slightly smaller but comparable figure. The remaining states, namely Washington D.C, Virginia, and Delaware, had a significantly lower number of participants.

### Dashboard 2: Marketing Expense and Interest Coefficient

![image](https://github.com/hoangln1508/Brand-Name-Interest-Survey/assets/136893356/7b7c197a-c412-46f6-a43d-d151ca3edadf)

#### Marketing Expense and Interest Coefficient By Income Coefficient

The Interest Coefficient is a metric that quantifies the relationship between marketing expenditures and consumer interest. A higher interest coefficient indicates greater effectiveness in marketing efforts.

The Dashboard provides insights into the level of marketing interest and costs for brands categorized by industry and income groups, namely Low, Medium Low, Medium High, and High. Analysis of the data reveals that car and appliance brands exhibit relatively similar and suboptimal marketing effectiveness. Income groups with higher marketing expenditures also demonstrate a greater degree of consumer interest compared to those with lower marketing expenditures. This finding suggests a positive correlation between marketing costs and their effectiveness.

The automotive and equipment industries exhibit relatively stable and favorable marketing effects. Similarly, the entertainment industry demonstrates satisfactory marketing performance when marketing costs are positively associated with the interest coefficient. However, the marketing effectiveness for the elderly age group is suboptimal compared to other age groups, primarily due to their significantly lower preference coefficient despite relatively higher marketing costs. This pattern is also observed in the F&B industry, where the marketing expenditures for the elderly age group are substantial but fail to yield optimal results. Conversely, the F&B industry proves successful in targeting the teenage demographic, given their low allocation of marketing expenditures. Consequently, concerns regarding marketing effectiveness span across different age groups.

The retail and technology sectors also fall short in terms of marketing effectiveness, as their marketing efforts primarily cater to specific age groups rather than encompassing a broader range. Nevertheless, these industries have successfully achieved effective marketing outcomes for potential customers within the targeted age groups. In the case of the technology industry, marketing proves highly effective for both adults and adolescents, characterized by low marketing costs and significantly higher interest coefficients compared to other age groups.

#### Average of Marketing Expense and Interest Coefficient by Age group

A comprehensive survey was conducted to examine the relationship between manufacturing and business sectors, including the Automobile, Devices, Entertainment, F&B, Retail, and Technology industries, with various customer segments based on age. The findings demonstrate that these industries have achieved relative effectiveness in marketing endeavors, leading to increased customer engagement and sales. However, intriguingly, certain age groups do not respond favorably to these industries, while others exhibit a clear positive correlation between Marketing Expenses and Interest Coefficient.

Significant disparities arise when comparing the preference coefficients of the Elder and Teenager age groups across most categories. Specifically, within the Entertainment, F&B, and Retail sectors, the Elder age group demonstrates a notably low consumer preference coefficient, whereas the Teenager age group exhibits high popularity. This suggests that the marketing strategies employed by these industries are ineffective for the Elder age group but highly successful for the Teenager age group. Conversely, the Automobile industry boasts a high preference coefficient among the Elder age group but lacks popularity among Teenagers. Notably, despite allocating substantial Marketing Expenses to target the Elder age group, this industry maintains a stable and relatively effective marketing impact within its potential customer segment.

The Technology and Devices industries showcase a relatively stable correlation coefficient of interest across age groups, with no age group falling below the threshold of a significantly low Interest Coefficient. Moreover, these industries have proven effective for specific age groups. It can be concluded that these industries are successfully utilizing Marketing Expenses and implementing appropriate strategies to achieve their marketing objectives.

#### Average of Marketing Expense by Survey State and Gender

The findings of the analysis indicate that the majority of marketing expenditures are concentrated in the states of Pennsylvania and New York. Comparatively, the remaining states, including Delaware, Washington D.C., and Virginia, receive only a small portion of the total marketing costs. The distribution of marketing costs among male and female customers is relatively balanced, although there is a general inclination to allocate higher marketing expenses towards women across various categories. Industries that attract greater interest from women, such as F&B and Retail, recognize this trend and increase their marketing investments in this customer segment. On the other hand, in the electronics and technology sectors, including Device and Technology, there is a tendency for higher marketing costs to be directed toward male customers in the respective states.

Interestingly, an unexpected result emerged in the Automobile industry, where companies decided to allocate significant marketing expenditures towards female audiences despite men displaying greater interest in this industry. This pattern holds true across all states. This contradicts the conventional wisdom that suggests men are generally more interested in the Automobile industry.

### Dashboard 3: Firm Performance

![image](https://github.com/hoangln1508/Brand-Name-Interest-Survey/assets/136893356/4657f23a-9e48-4880-ad0f-ef6410ebe257)

#### Necessity Score and Replaceability Risk by Industry

This graphical representation employs a dual-axis line chart to illustrate key insights. The horizontal axis corresponds to the industry column, while the vertical axes depict two metrics: Necessity Score and Replaceability Risk. The chart facilitates a comparative analysis of industry groups in terms of their necessity and susceptibility to substitution. Overall, a clear inverse relationship is observed between these two factors. Industries characterized by a high necessity index tend to exhibit a lower degree of replaceability.

#### Innovative Score by Industry

For visual representation, a line chart is utilized with the horizontal axis representing the industry column, and the vertical axis depicting the Innovative Score index. This chart enables a comparative analysis of the Innovation index among different industry groups. The findings indicate that the majority of industries exhibit relatively high ratings in terms of innovation. However, two industry groups, namely Food & Beverages and Retail, stand out significantly with notably lower Innovation scores.

#### Quality Score and Product Value by Industry

In this analysis, a scatter chart is employed, featuring two axes: the horizontal axis represents the Quality Score index, while the vertical axis represents the Product Value index. The aim is to examine the relationship between product quality indicators and the assessment of product value, specifically addressing whether the product justifies its cost. The overall findings indicate that there is no distinct correlation between these two indicators.

Certain industry groups, such as Automobile, Devices, Entertainment, and F&B, demonstrate high ratings in terms of value for money. Conversely, Retail and F&B are recognized for their superior product quality. Notably, the Food & Beverages sector receives high ratings on both indicators when compared to the other industry groups surveyed.

#### Trial Rate and First Impression by Industry

A scatter chart is utilized in this study, featuring two axes: the horizontal axis represents the Trial Rate index, while the vertical axis represents the First Impression index. The objective is to examine the correlation between indicators of customers' willingness to try new products and their initial impressions of the industry groups under investigation. The overall findings suggest that a clear correlation between these two indicators is not evident within the surveyed industry groups.

However, several industry groups, namely Devices, Retail, F&B, and Technology, have successfully made a positive first impression on the surveyed customers. Moreover, Technology and Entertainment stand out as industry groups with a high index of customers expressing a desire to experience new products. Notably, Technology emerges as an industry group that not only leaves a favorable impression on customers but also sparks their interest in trying new products.

### Dashboard 4: NPS Analysis

![image](https://github.com/hoangln1508/Brand-Name-Interest-Survey/assets/136893356/99374440-f5a5-4ed5-b47d-5e1aaf748b39)

In the realm of customer satisfaction measurement, the Net Promoter Score (NPS) serves as an indicator of customers' satisfaction with a brand and their likelihood of recommending it to friends and relatives. NPS responses can be categorized into three groups:

* Promoters: Customers who rate their willingness to recommend the brand with a score of 9 to 10. These individuals are enthusiastic and loyal, actively advocating for the brand and attracting new customers through word-of-mouth.
* Passives: Customers who give a score of 7 to 8. They do not actively promote the brand and may potentially become brand promoters or switch to a competitor's product.
* Detractors: Customers who rate their willingness to recommend with a score of 0 to 6. These individuals are dissatisfied customers who not only pose a risk of customer loss for the brand but can also negatively impact the brand by sharing negative experiences with the company or their acquaintances.

The NPS is calculated using the following formula:

NPS = Percentage of Promoters - Percentage of Detractors

Furthermore, Customer Satisfaction (CSAT) pertains to the level of satisfaction customers experience during their interactions with a brand and the quality of its products or services. This metric is crucial in gauging the brand's ability to retain customers and cultivate loyalty among them.

#### Overview

The NPS data analysis dashboard will incorporate the following visualizations:
* Filter bar (Slicer): This feature allows data to be filtered based on the brand and industry, providing focused insights.
* Line and Clustered column chart: This chart illustrates the relationship between NPS groups and the CSAT index for specific age groups, enabling a comparative analysis.
* Stacked Area chart: By representing NPS groups, this chart highlights the correlation among different income groups, offering insights into customer satisfaction.
* Gauge chart: This chart provides a precise representation of the NPS and CSAT indices, offering a visual indication of their respective values.
* Card: Displaying the exact counts for each NPS group, including Detractors, Promoters, and Passives, this chart provides specific numerical information for quick reference.

#### Promote Type

In Dashboard 4, three cards were specifically designed to obtain precise data regarding Promoters, Passives, and Detractors based on brand and category. Generally, there is a relatively balanced distribution of Promoters and Passives across all brands, with approximately 1800 respondents in each category. The number of Detractors falls within the range of 6300 to 6500 across brands. The survey utilized an 11-point scale, ranging from 0 to 10, to gauge responses, and it was observed that the response rates were relatively consistent across different selection levels, with minimal variation among brands and categories. These findings suggest that all major brands should focus on reducing the number of Detractors and enhancing customer satisfaction and positive impressions.

Regarding the number of Promoters, Apple stands out with the highest count (1883 out of 1000 respondents), while Google has the lowest count with 1762 out of 1000 Promoters. Additionally, Google has the highest number of Detractors (6462 individuals), whereas Coca-Cola has the fewest Detractors (6328 individuals). These results indicate that, in terms of NPS-related metrics, Google's performance is not optimal, as it exhibits the highest percentage of individuals unwilling to recommend the brand among the ten brands analyzed.

#### NPS and CSAT

Based on the bar chart, it is evident that the Automobile industry exhibits one of the lowest levels of customer satisfaction, as indicated by its NPS and CSAT scores. The NPS score for this industry stands at -47.04%, indicating a significant proportion of customers expressing a negative likelihood to recommend the brand. Furthermore, the CSAT score of 39.57% places the Automobile industry in the second lowest position in terms of customer satisfaction. These findings highlight the ineffectiveness of the sales strategy employed within this category, as it fails to generate substantial positive feedback from customers compared to the other five categories analyzed.

In contrast, the Devices industry demonstrates a competitive advantage in terms of its ability to attract customers. It obtains the highest NPS and CSAT scores among the categories, with NPS at -44.72% and CSAT at 40.43%. However, it is worth noting that there are significant variations in the NPS and CSAT scores across the aviation industries, ranging from -44% to -47% for NPS and from 38% to 41% for CSAT. Overall, these results suggest that the marketing strategies implemented by the ten brands analyzed have not yielded desired outcomes, as evidenced by the negative NPS results. Furthermore, the findings indicate that the overall customer experience is average and falls short of being truly satisfactory, making customers more prone to switching to alternative products offered by other brands that deliver superior experiences.

#### NPS and CSAT by age group 

When examining the NPS scores categorized by age groups, it is observed that the Middle-Aged and Adult segments yield nearly identical scores. Specifically, the Detractors index falls within the range of 4200 to 4300, while the Passives and Promoters index ranges from 1100 to 1300. Similar trends are noticed for the Elderly and Teenagers age groups, where their respective NPS scores align closely. In terms of the CSAT index filtered by category, the youth age group exhibits a preference for products in the Automotive, Appliance, and Entertainment industries, as reflected in their higher index values of 40.84%, 40.72%, and 40.72% respectively. On the other hand, the elderly demographic demonstrates greater satisfaction with products in the Food and Beverage industry, recording a CSAT index of 41.57%. However, the elderly do not exhibit a particular preference for the Automotive (39.58%), Appliance (38.37%), Retail (39.21%), and Technology (39.55%) industries. Among the Middle-Aged age group, the Retail industry obtains the highest CSAT index compared to other age groups, reaching 40.5%. Conversely, the Technology, Automotive, and Food and Beverage sectors fare less favorably. Lastly, the CSAT indicators for the Adult age group indicate a preference for products and services in the Equipment industry (40.43%) and Technology (40.25%), while Entertainment (38.58%) and Food and Beverage (39.89%) receive comparatively lower scores, ranking the lowest among all age groups.

#### NPS Score by Income Group

In general, the NPS scores across all income groups range from -44% to -48%. Specifically, the Automotive industry displays minimal fluctuations, hovering around the -46% mark. On the other hand, the Entertainment and Technology sectors demonstrate higher NPS scores among customers with higher income levels. Conversely, the Automotive and Equipment industries exhibit divergent NPS trends. Unlike the Equipment industry, the low-middle income group shows relatively lower support for the Automotive industry compared to the other three customer groups. In the retail industry, NPS scores are notably higher for the low-income group, surpassing those of all other groups by 2%. Additionally, the upper-middle and upper-income groups display higher NPS scores in the Food & Beverage industry.

#### CSAT by Income Group

The survey results indicate that the overall CSAT score among the 10,000 participants remains relatively stable, with satisfaction levels for product quality across income groups and industries fluctuating between 38% and 42%. This suggests a consistent distribution of scores on the rating scale, highlighting the need for brands to enhance their performance to achieve more noteworthy data. Similar to the NPS graph for income groups, the low-income group exhibits the highest CSAT score (41.5%) and shows a decrease as the income level of participants increases. Furthermore, the Food and Technology industries receive high CSAT scores from both the high and low income groups, while the Equipment industry demonstrates high satisfaction scores for product quality among the low and middle income groups (approaching 41%). In the Entertainment industry, only the lower middle income group shows a high CSAT score, while the Automotive industry experiences an increase in CSAT levels corresponding to the income level of respondents. Dashboard 5 reveals that the two indicators, NPS and CSAT, exhibit limited correlation with each other.

## CONCLUSION

In conclusion, the aforementioned report partially presents the findings of consumer surveys regarding products and brands. These surveys serve as essential tools for businesses and potential investors, offering insights into the preferences and desires of customers. By understanding customer satisfaction with their products and brands, businesses can make improvements to enhance the quality of their offerings and services. Moreover, the report provides an overview of firms and industries, equipping investors with information to analyze and make informed investment decisions.

Specifically, consumer survey reports on products and brands deliver crucial information to businesses regarding customer needs and desires. This allows businesses to enhance product quality, refine their marketing strategies, and increase customer satisfaction, thus reinforcing their brand vision and values. The survey results reveal that consumers primarily consider factors such as first impressions, product quality, reasonable pricing, after-sales service, and brand value when evaluating their satisfaction. Among these factors, product quality emerges as the most significant determinant of consumer satisfaction.

To enhance customer satisfaction, businesses should prioritize improving product quality, enhancing after-sales service, and developing a clear and consistent brand vision and values. Additionally, the report provides investors with a foundational understanding of pertinent information to evaluate the potential of the product and business. It furnishes investors with insights into consumer opinions on product satisfaction, quality, and other factors. Furthermore, the report offers information on consumer trends and market forecasts, enabling investors to make well-informed and effective investment decisions. This information aids in assessing the potential for future revenue growth, profitability, and market competition, facilitating the development of appropriate investment plans.
