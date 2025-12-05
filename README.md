Promise Early Education: Tracking COVID-19 Impact Across Age and IEP StatuesProject title
================
by Gold Analyst (Mekkawy Mohamed, Razva Negru, Nisan Ozmert)

## Summary

Promise Early Education is a learning program in Central Maine dedicated to educating children (ages 0–5) from low-income backgrounds and preparing them for success in school and beyond. The program uses GOLD® Assessment data, which is collected through teachers’ observations during everyday classroom activities. Teachers gather documentation (notes, photos, work samples, etc.), match it to developmental progressions, and assign ratings throughout the year. Ratings are finalized at the fall, winter, and spring checkpoints/trimesters.
The activities are divided into six developmental categories, measuring how many children meet, exceed, or fall below expectations at each checkpoint. We used data from the 2018–2019 to 2024–2025 school years to understand the impact of the COVID-19 pandemic on student performance, focusing specifically on differences by IEP status and age group.
In total, the dataset includes 702 observations across 11 variables.

## Analysis
The first thing we did was clean the data provided by the organization using both Excel and R, where we created mainly six variables: category, #Children, Age, IEP, #Meeting/Exceeding, %Meeting/Exceeding, and Time Period. We also created four sub-variables that helped us create cleaner plots by establishing chronological order and relabeling the time period: year, season, label, and sort_number. We used the year 2018–2019 as pre-COVID, 2020–2021 as during the COVID-19 pandemic, and the school years up to 2024–2025 as post-COVID-19 years. We decided to use %Meeting/Exceeding (of children) as an indicator of their average success over the school year.
Once we had clean data, we first explored the overall impact of COVID without dividing students into different groups, using a line graph across the school years. We observed that after the COVID-19 pandemic, fewer children tended to perform well in the first trimester compared with the previous years in all categories. The growth over the school year also seemed to become more linear during the post-COVID-19 years, compared to a more steep linear increase in the pre- and during-COVID-19 years.
Later, we decided to concentrate on the impact of the COVID-19 pandemic by using a line graph faceted by category, with different lines representing different age groups. We observed almost no change in the earlier age groups, which could be explained by smaller classroom sizes in Promise Early Education for those age groups compared to the 3–5 age groups, or because some of those children were not yet born during the COVID-19 pandemic. Therefore, in our line graph we excluded those groups and concentrated only on the age groups 2–3, 3–4, and 4–5. Similar to the 0–2 year olds, we saw almost no change in the 2–3 year olds except in the Language category during and early post-COVID-19 years; however, they seemed to recover by the end of the fourth post-COVID-19 year (2024–2025).
When we looked at the 4–5 age group, we interestingly saw worse performance before COVID-19 but a gradual decrease in the post-COVID-19 years, especially in the Social-Emotional and Language categories. The trend in Social-Emotional outcomes has also been observed in other research. Finally, the age group 3–4 seemed to be the most impacted by COVID-19, as they showed a gradual decrease in %Meeting/Exceeding during the post-COVID-19 years similar to the 4–5 group, but in all categories except Physical.
For the IEP graph, we created an area plot and observed the gap between the % of children with IEP status who met or exceeded expectations and the % of children without IEP status who met or exceeded expectations. Our dataset did not include any data from pre-COVID-19, so we specifically focused on during and after the pandemic. Our first observation was that children with IEP status had a slightly lower %Meeting/Exceeding compared to students without IEP status during the pandemic, especially in the Cognitive, Mathematics, Literacy, and Physical categories. However, the gap between students with IEPs and those without IEPs increased during the post-COVID-19 years, with the largest declines for students with IEP status occurring in Language, Cognitive, and Mathematics. Even four years after the height of the pandemic, the performance gap between IEP and non-IEP students remains larger than it was during COVID-19.
 
## Conclusion
In the process of creating the data visualizations, we have come to the realization that the COVID-19 pandemic still impacts early education for children, especially in Promise Early Education. The impact of it still seems to be represented in overall student performance. We have concluded that its impact varies across different age groups, and some age groups are able to recover faster than others. We have also concluded that the education of children with IEP status has been impacted by the COVID-19 pandemic, and even after four years since the pandemic, they have not shown any clear signs of recovery.

## Limitations
To understand the success of the children, we summed the number of children meeting and exceeding expectations and took an average of it. However, while cleaning the data, we observed that different groups in different time periods have different ratios of meeting to exceeding. This generalization decreases our understanding of success, and it would be better in future research to separately examine the % of children meeting and the % of children exceeding expectations.
We also considered that one reason why some age groups were less impacted by the pandemic (such as the 0–2 age group) might be smaller class sizes. However, our research did not include class size as a factor, and in the future the impact of class size should be considered.
Finally, one limitation with the dataset is that the standards for meeting and exceeding expectations vary across age groups and categories.

## Handout

Our handout can be found [here](handout/handout.pdf). 

## Memo

A link to the code and how we created our graphics in our memo can be found [here](memo/memo.md).

## Data
Promise Early Education, 2018-2025. Child Outcome Data. 
https://github.com/ES-1085/f2025-ds1-project-gold/tree/828eae0672bc4ea7f62bfd1f8767e6c514839438/data/ignore

## References
“Impact of the Covid-19 Pandemic on Early Childhood Care and Education.” 2020. Early Childhood Education Journal 48 (5): 533–36. https://doi.org/10.1007/s10643-020-01082-0.
“Promise Early Education Center | Empower Your Child With Early Education.” n.d. https://promiseearlyeducation.org/.
Lambert, Richard, Ph.D. 2020. “Technical Manual for the Teaching Strategies GOLD® Assessment (2nd Edition): Birth Through Third Grade.” PDF. Technical Manual. Teaching Strategies GOLD® Assessment. 2nd ed. https://teachingstrategies.com/wp-content/uploads/2020/09/2020-Tech-Report_GOLD_B-3_V4.pdf.

