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
