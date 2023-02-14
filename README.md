# Methodology

In this section, I will be using "new" data that was not seen in the exploratory analyses prior to this. I will be using simulation methods in an attempt to answer the hypotheses that were previously stated. Using this type of method will allow for more accurate results since there are different factors that play into the intervals and not everything has an equal opportunity of happening. 

```{r}
nyc_squirrels2 <- nyc_squirrels %>%
  filter(age!="NA") %>%
  filter(age != "?") %>%
  filter(above_ground_sighter_measurement != FALSE) %>%
  mutate(above_ground_sighter_measurement= as.numeric(above_ground_sighter_measurement)) %>%
  mutate(age= ifelse(age=="?", NA, age))

p_meds <- nyc_squirrels2 %>%
  group_by(age) %>%
  summarize(med= median(above_ground_sighter_measurement))
nyc_squirrels %>%
  filter(age!="NA") %>%
  filter(age != "?") %>%
  filter(above_ground_sighter_measurement != FALSE) %>%
  mutate(above_ground_sighter_measurement= as.numeric(above_ground_sighter_measurement)) %>%
  mutate(age= ifelse(age=="?", NA, age)) %>%
  ggplot() +
  geom_boxplot(mapping = aes(x = above_ground_sighter_measurement, y = age)) +
  labs(title = "Climbing Potential Based on Age",
       x = "Above Ground Measurement",
       y = "") + 
  geom_text(data = p_meds, aes(x= med+5, y = age, label= med))
```

Here, we are looking at the distribution of location in trees height wise based on squirrel ages through a box plot. Our y-axis variable consists of age which is not a numerical variable and is rather categorical with the two main categories being juvenile and adult. Our x-axis variable is a numerical variable that measures how high up off of the ground squirrels were spotted. 
In terms of this plot, we can see that the median in both data sets is 10, but the outliars shown in the adult box plot are indicative of a much higher climbing range.

```{r}
nyc_squirrels %>%
  filter(age!="NA") %>%
  filter(age != "?") %>%
  mutate(age= ifelse(age=="?", NA, age)) %>%
   filter(primary_fur_color!="NA") %>%
  ggplot() +
  geom_bar(mapping = aes(x = age, fill = primary_fur_color)) +
  labs(title = "Age by Fur Color",
       x = "Age",
       y = "Fur Color")
```

In this bar plot, we are looking at the distribution of fur color based on age. Each bar is representative of the age of the squirrel. In our data set, age is not a numerical variable and is rather categorical with only the options "adult," "juvenile, "?," and "NA." In this data set, we got rid of the "juvenile" and "NA" categories in order to focus on the data that was age-specific. The three fur colors are only representative of the primary fur color which is not to be confused with other data sets that show highlight fur colors or the set that includes both. The three primary colors that were noted are black, cinnamon, and gray.
If we look at each bar, though there are significantly move adults compared to juveniles, the distribution of color within each age category is pretty evenly distributed. The majority of squirrels in this data are gray squirrels with the next most common fur color being cinnamon and the least common being black. 
