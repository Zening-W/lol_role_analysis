# League of Legends role carrying analsysis
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

## Baseline Model

## Final Model

## Fairness Analysis


