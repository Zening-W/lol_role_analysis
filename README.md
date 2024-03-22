# League of Legends carrying analsysis
By Zening Wang and Chenxi Li
## Introduction
Our dataset comprises the entire professional match statistics for the game League of Legends throughout 2023. Each match is represented by 12 rows, including one for each player and one for each team, with over 100 columns capturing various dimensions of data. Our primary question is focused on determining which role carries the most impact in professional matches during 2023, specifically between Mid and Bot players.
We have narrowed down our investigation to these two roles because, in professional matches, they are typically regarded as the primary carrying positions, while other roles such as Top, Jungle, and Support intentionally allocating resources such as minions and kills to them. 

It's important to note that there are numerous ways to define "carry" in League of Legends like vision score, damage taken, crowd control etc.. For this analysis, we will use the straightforward metric of "damage dealt". However, to provide a more comprehensive evaluation considering the resources acquired by each role, we will compare using the metric "damage per gold." This approach aims to assess which role, whether the mage (often found in Mid) or AD carry (Bot), is more efficient in dealing damage to the enemy team relative to the resources invested. Through this analysis, players and teams might be able to reconsider resources distribution and tactical priority of among the 5 roles.

After cleaning and filtering the original dataset, we keep 9 columns in total: *patch*, *split*, *position*, *champion*, *result*, *damagetochampions*, *damageshare*, *visionscore*, *totalgold* and one added column *damagepergold*. We choose these columns because basically these consist of all measurements of "carrying" and we also keep record of the patch and time data for further anlysis. After excluding team data rows, we have 104920 rows remaining.

Explanation of columns:
- *patch*: is the game patch of this match take place at
- *position*: is the specfic role of the player
- *champion*: is the champion selection of the player
- *result*: is the boolean result of this match(1 for win, 0 for lose)
- *damagetochampions*: is the damage of the player deals to enemy champions
- *damageshare*: is the ratio proportion of the damage the player has to the whole team
- *visionscore*: is the vision of the team this player has influenced
- *totalgold*: is the total gold of the player gained in the whole match

## Data Cleaning and Exploratory Data Analysis
After loading the dataset, we need to first select the above columns from the original dataset by specifying the column neams. Then we need filter out all rows of team data from the dataset by slicing the "postion" columns. After this, we check all none values in each column to make sure they are in explainable extent(notice that it is common that there are many none values in "split" column because certain  matches hold only once a year so they have no splits definitions). Finally, we add one more column called "damage per gold" by dividing the "total damage" by the "total gold" as the most direct anaylyzing factor. After cleaning, here is the head of our dataset:

|    |   patch | split   | position   | champion   |   result |   damagetochampions |   damageshare |   visionscore |   totalgold |   damagepergold |
|---:|--------:|:--------|:-----------|:-----------|---------:|--------------------:|--------------:|--------------:|------------:|----------------:|
|  0 |   13.01 | Spring  | top        | Jax        |        1 |               14283 |     0.150027  |            49 |       18855 |        0.757518 |
|  1 |   13.01 | Spring  | jng        | Poppy      |        1 |                6219 |     0.0653236 |            61 |       12082 |        0.514733 |
|  2 |   13.01 | Spring  | mid        | Taliyah    |        1 |               27028 |     0.283899  |            49 |       15722 |        1.71912  |
|  3 |   13.01 | Spring  | bot        | Ezreal     |        1 |               42005 |     0.441215  |            47 |       17332 |        2.42355  |
|  4 |   13.01 | Spring  | sup        | Karma      |        1 |                5668 |     0.0595359 |           106 |        8816 |        0.642922 |


Univariate Analysis:
This is the distribution of our new variable "damage per gold'. We can see the majority of the players have such ratio between 0.7 to 1.1.
<iframe
  src="assets/dis_damagepergold.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Bivariate Analysis:
We can see that Mid and Bot players have highest two distributions with Mid seem to be a little bit higher while Jungle and Support have lowest ones.
<iframe
  src="assets/damage_per_gold_by_position.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
However, when we ignore the effect of gold, we would find that although the highest two positions are still Mid and Bot, Bot players seem to have higher damage share within the team. But this also means Bot players are taking the most amount of resources among the team proved by next graph.

<iframe
  src="assets/damage_Share_by_position.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/gold_by_position.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Interesting Aggregates:
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">damagetochampions</th>
      <th colspan="2" halign="left">damageshare</th>
      <th colspan="2" halign="left">visionscore</th>
      <th colspan="2" halign="left">totalgold</th>
      <th colspan="2" halign="left">damagepergold</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>std</th>
      <th>mean</th>
      <th>std</th>
      <th>mean</th>
      <th>std</th>
      <th>mean</th>
      <th>std</th>
      <th>mean</th>
      <th>std</th>
    </tr>
    <tr>
      <th>position</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bot</th>
      <td>20255.536409</td>
      <td>10277.401933</td>
      <td>0.277289</td>
      <td>0.074256</td>
      <td>38.183759</td>
      <td>16.453017</td>
      <td>13878.810904</td>
      <td>3367.200924</td>
      <td>1.410548</td>
      <td>0.471036</td>
    </tr>
    <tr>
      <th>jng</th>
      <td>11065.111514</td>
      <td>5963.557908</td>
      <td>0.154736</td>
      <td>0.057444</td>
      <td>47.420559</td>
      <td>18.922462</td>
      <td>10654.791937</td>
      <td>2267.763845</td>
      <td>1.008848</td>
      <td>0.404042</td>
    </tr>
    <tr>
      <th>mid</th>
      <td>18907.717022</td>
      <td>8449.390670</td>
      <td>0.264420</td>
      <td>0.069147</td>
      <td>34.942528</td>
      <td>14.211116</td>
      <td>12604.231414</td>
      <td>2901.886989</td>
      <td>1.466783</td>
      <td>0.446632</td>
    </tr>
    <tr>
      <th>sup</th>
      <td>5618.570959</td>
      <td>3334.636185</td>
      <td>0.080283</td>
      <td>0.038679</td>
      <td>92.301849</td>
      <td>31.921205</td>
      <td>7587.098361</td>
      <td>1540.391167</td>
      <td>0.727243</td>
      <td>0.346715</td>
    </tr>
    <tr>
      <th>top</th>
      <td>15722.323437</td>
      <td>6903.761283</td>
      <td>0.223272</td>
      <td>0.067161</td>
      <td>31.541651</td>
      <td>12.214691</td>
      <td>12040.812190</td>
      <td>2769.132188</td>
      <td>1.287362</td>
      <td>0.406557</td>
    </tr>
  </tbody>
</table>


From this aggregated table, we could see the results from the graphs we concluded above more clearly. While bot players have highest damage to the enemy among the team, they also have highest total gold meaning they have taken the most resources in the team. However, when we talk about damaging effciency, mid players have higher damage per gold. Something interesting is that while support players have far highest visison score, they have both lowest damage to enemy and gold gained, indicating they have spent all gold on placing wards(such greatness of sacrificing!)

## Assessment of Missingness
Let's first recall the proportion of missingness of data in our cleaned dataset:
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NA Count</th>
    </tr>
    <tr>
      <th>Column Name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>patch</th>
      <td>0.000953</td>
    </tr>
    <tr>
      <th>split</th>
      <td>0.226839</td>
    </tr>
    <tr>
      <th>position</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>champion</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>result</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>damagetochampions</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>damageshare</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>visionscore</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>totalgold</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>damagepergold</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>split_missing</th>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>

And I claim that the missingness of 'patch' to be NMAR for the following reason:
When I scroll to the certain rows with missing patches, I find that from original dataset that they are all LPL spring split matches. Moreover, they are during the patch between 13.4 and 13.5. Then I go to pedia page and and find that Tencent postpone the release of patch 13.5 in China region because of technical issues. Similarly, LPL also uses 13.4 patch for extra long time until Mar.9th. But they update the yummi rework and to keep it balanced so they basically use a hybrid patch with contents both from 13.4 and 13.5 since Mar.15th till LPL spring split ends. Resources:

https://liquipedia.net/leagueoflegends/LPL/2023/Spring
https://lol.qq.com/gicp/news/410/37023581.html

As a result, the patch information here is missing is due to the value itself is not a standard patch, resulting NMAR in the dataset.

Now we suspect the missingness of split column is dependent on column patch. So we will perform a permuatation test to see if analyze the dependency of the missingness of split column.

Null Hypothesis (H0): The missingness of the split column is independent of the patch column.

Alternative Hypothesis (H1): The missingness of the split column is dependent on the patch column.

As the pvalue is 0, we definitely need to reject the null hypothesis, there is very strong dependency between split column and patch column.
Here is the empirical distribution of the test statistic, along with the observed statistic.
<iframe
  src="assets/tvd_split_patch.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
And here is the distribution of split when patch is or is not missing. We can see there are great difference between the two pictures. For exmaple, there are much more  more proprotions of splits at 13.12 when patch is not misssing and there are much more proprotions of splits from 13.17-13.19 when patch is missing.
<iframe
  src="assets/fig_missing_split_patch.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig_nonmissing_split_patch.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Now we suspect the missingness of split column is also dependent on column result.(Some teams might not report their results when they lose?) So we will perform a permuatation test to see if analyze the dependency of the missingness of split column.

Null Hypothesis (H0): The missingness of the split column is independent of the result column.

Alternative Hypothesis (H1): The missingness of the split column is dependent on the result column.

As the pvalue is 1, we definitely fail to reject the null hypothesis, there is little dependency between split column and result column, meaning that split missing is not related to result.
Here is the empirical distribution of the test statistic, along with the observed statistic.
<iframe
  src="assets/tvd_split_result.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
And here is the distribution of result when patch is or is not missing. We can see there are almost no difference in proprotions of winning and losing from the pictures no matter split is missing or not. 
<iframe
  src="assets/fig_missing_split_result.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig_nonmissing_split_result.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Hypothesis Testing
Question:Do mid and bot players have similiar damage per gold in general?(Use significance level of 1%)

Null hypothesis(H0):There is no significant difference in average damage per gold between Bot and Mid players. 

Alternative hypothesis(H1):There is significant difference in average damage per gold between Bot and Mid players. 

Test statistic : Kolmogorov–Smirnov statistic(As we want to measure the similarity between two distributions.)

ks_statistic, p_value: (0.06991040792985126, 4.9269803170380824e-45)
The p-value is far smaller than 0.01, indicating that we are sure to reject the null: it is very likely that there is significant difference in average damage per gold between Mid and Bot players. Specfically, as the statistic is negative, mid players tend to have higher damage per gold than bot players.
<iframe
  src="assets/mid_bot_compare.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
We can see that Mid laners generally have higher damage per gold than Bot laners, especially in 1.5-2 area. So finally we can conclude that Mid laners have higher damaging effciency.

## Framing a Prediction Problem

From here, we would measure the word "carry" in another way by doing a regression prediction problem. 
We aim to predict the impact score of players in League of Legends esports matches based on various in-game performance indicators. The impact score is another variable we introduce: a composite metric derived from individual performance metrics, including kills, assists, total creep score (CS), towers taken down, and damage dealt. This complex variable only takes the multiple indicators of resoruces of a player from first 15 minutes of the match. In other words, we only know the data(introduced below) of first 15 minutes at the time of prediction.

## Baseline Model

Our baseline model incorporates two predictive models: Linear Regression and Random Forest Regressor. These models provide a comparative basis for assessing the potential for performance improvement and model refinement.

**Linear Regression:** This model assumes a linear relationship between the features and the target variable, impact score. Linear Regression is less prone to overfitting compared to more complex models, making it a suitable choice for establishing a performance benchmark. It serves as an excellent comparison point for other, more advanced models due to its simplicity and interpretability.

**Random Forest Regressor:** As a supervised learning algorithm, Random Forest leverages ensemble learning methods for regression tasks. It is particularly adept at capturing non-linear relationships between features and the target variable. The Random Forest Regressor can efficiently handle both categorical and continuous variables, and it has built-in mechanisms for dealing with missing values, many of which may have been imputed during data cleaning and feature engineering processes.

The features selected for these baseline models include:
- **Champion:** The character played, encoded categorically.
- **Early Game Performance Indicators:** Kills, assists, and CS at the 15-minute mark, along with gold and experience (XP) at the same timestamp and use specific formula [log(kills) + log(assists) + log(0.1*cs) + log(0.5*towers) + log(0.2*dragons)] to convert to numerical variable.
- **Damage to Champions:** Total damage dealt to enemy champions, indicating player aggressiveness and contribution to team fights, numerical varaible.

These features were preprocessed using one-hot encoding for categorical variables and imputation for missing numerical values. The dataset was split into training and testing sets, with models trained on the former and evaluated on the latter.

Our model's performance was assessed using the Root Mean Square Error (RMSE), which offers a measure of the prediction accuracy by quantifying the difference between the predicted and actual impact scores. A lower RMSE indicates a model with higher accuracy. Additionally, we considered the $R^2$ (coefficient of determination), Mean Absolute Error (MAE), and Explained Variance scores to provide a comprehensive evaluation of the model's predictive capability.

Here is our result:

Linear Regression Cross-Val MSE:  0.7076808594891522
Random Forest Cross-Val MSE:  0.6219073190521505
Linear Regression RMSE: 0.8328190121163178
Random Forest RMSE: 0.7870945837869731
Linear Regression R^2: 0.6773935785157854
Random Forest R^2: 0.711845375606756
Linear Regression MAE: 0.6666462434234882
Random Forest MAE: 0.6175121574361448
Linear Regression Explained Variance: 0.6774424359664726
Random Forest Explained Variance: 0.711898694342655

For MSE and RMSE, the Random Forest model outperforms the Linear Regression model, as it has lower values for both metrics. This indicates that the Random Forest model has better predictive performance in terms of error.

For R-squared and Explained Variance, the Random Forest model also performs slightly better, with higher values indicating that it explains more variance in the dependent variable compared to Linear Regression.

In terms of MAE, the Random Forest model again has a lower value, indicating that it makes predictions that are closer to the actual values on average compared to the Linear Regression model.

The Random Forest model, in particular, demonstrated superior performance over Linear Regression, suggesting that the relationship between our selected features and the target variable might not be linear. However, the overall accuracy is not desired as good as variables like rmse is too large. We need to find ways to reduce it.

## Final Model
### Hyperparameter Tuning

To mitigate overfitting risks and improve model performance, we undertook hyperparameter tuning using cross-validation. For the Random Forest Regressor, tuning parameters to `max_depth = 10` and `n_estimators = 600` yielded a significant reduction in RMSE to 6.82.

### Feature Engineering

We introduced two new features based on early game performance:

- *Early Game Efficiency:* A combination of early kills, assists, and a portion of the CS by the 15-minute mark.
- *Gold-XP Ratio at 15:* The ratio of gold to XP at the 15-minute mark, highlighting resource management efficiency.

The first variable is easy to understand, just another measurement of indiactor but with different proportions of compoenents. For the second one, notice that in League of Legends, getting same amount of gold and XP at the same time is very important for carrying roles like Mid and Bot. The reason is that besides cs(minions), another important way to get XP is getting kills. When a team gets a kill, all the team members nearby would get a very large amount of XP. However, only the one who get the kill would get the majority of the gold and rest only share a very small portion of gold. So such a Gold-XP Ratio would reflect not only if a player's preset at the team kill, but also show whether this player gets a kill or just share the assist gold. In professoinal matches, when carrying positions like Mid and Bot only take assists but not kills, even if they are high in XP, it is still very difficult for them to carry due to lack of gold to purchase better equipments. That is why we add this feature.

### One-Hot Encoding:

One-hot encoding is crucial when dealing with machine learning models that cannot inherently handle categorical data. By converting categories into a binary matrix, we ensure that the algorithm treats each category with equal importance, without any bias towards categories due to their order or position in the dataset. For example, in our dataset:

Champion: Ahri -> [1, 0, 0, ..., 0]
Champion: Zed -> [0, 0, 0, ..., 1]

This process, however, increases the dimensionality of the dataset, which could lead to issues such as the curse of dimensionality. Hence, it's often paired with techniques to reduce overfitting and ensure the model's generalizability. Our approach ensures only categories (champions) represented in more than 100 observations are included, minimizing sparse columns and focusing on features with sufficient data representation.

### Model Optimization

Through iterative feature selection and engineering, we evaluated the performance impact of each addition. Notably, integrating one-hot encoded genres and release year data significantly enhanced model performance. Our explorations into combining features based on genre preferences and production details further refined the model's accuracy.

Here is our result:
Random Forest RMSE: 0.7609615873987088
Random Forest R^2: 0.7306622579452193
Random Forest MAE: 0.6003176789080994
Random Forest Explained Variance: 0.7306841023775656
Linear Regression RMSE: 0.6333429747871597

Ultimately, the combination of rigorous hyperparameter tuning and strategic feature engineering yielded optimized models with substantially improved accuracy, as evidenced by the decreased RMSE scores.

## Fairness Analysis

High Early Game Efficiency: Players with "early_game_efficiency" above or equal to the median.
Low Early Game Efficiency: Players with "early_game_efficiency" below the median.
We want to see if our model performs worse for individuals in Group of High Early Game Efficiency than it does for individuals in Group Low Early Game Efficiency?

Null Hypothesis (H0): The model is fair. The RMSE for the high early game efficiency group and the low early game efficiency group are roughly the same, and any differences are due to random chance.

Alternative Hypothesis (H1): The model is unfair. The RMSE for the high early game efficiency group is significantly different from the RMSE for the low early game efficiency group.

Test statistic: difference in RMSE between groups

Significance level: 1%

We get P-value = 1.0: This means that the permutation test did not produce any permuted dataset differences in RMSE that were less extreme than the observed difference. Every permutation resulted in a difference that was equal to or greater than what was observed in my actual data.

Implications for the Null Hypothesis: With such a high p-value, I do not have evidence to reject the null hypothesis. This suggests that the difference in RMSE between the high and low early game efficiency groups can indeed be attributed to random chance, indicating that our model does not show unfairness based on the metric and groups tested.

graph

Given that the observed difference is less than most of the permuted differences, this supports the p-value of 1.0. It suggests that the observed difference in RMSE between the high and low early game efficiency groups is well within the range of what could occur by chance alone. There doesn't appear to be evidence of unfairness in the model between these two groups based on this metric, as the observed disparity in performance is not significantly different from the disparities in the permuted samples.

tables

Finally, these three tables are the mean value of Impact Score of different postions from orginal dataset, test-split dataset and our predictions, repectively. Recall what we explore at problem1-4, Bot has higher score than Mid this time: the metirc we use in 5-8 has a different way of defining carry even though these two roles are still proved to be most impactful roles. And interestingly, although with some defect and unfairness, our model predict the roles' overall impact score more accurately.

