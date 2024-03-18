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
| position   |   ('damagetochampions', 'mean') |   ('damagetochampions', 'std') |   ('damageshare', 'mean') |   ('damageshare', 'std') |   ('visionscore', 'mean') |   ('visionscore', 'std') |   ('totalgold', 'mean') |   ('totalgold', 'std') |   ('damagepergold', 'mean') |   ('damagepergold', 'std') |
|:-----------|--------------------------------:|-------------------------------:|--------------------------:|-------------------------:|--------------------------:|-------------------------:|------------------------:|-----------------------:|----------------------------:|---------------------------:|
| bot        |                        20255.5  |                       10277.4  |                 0.277289  |                0.0742564 |                   38.1838 |                  16.453  |                 13878.8 |                3367.2  |                    1.41055  |                   0.471036 |
| jng        |                        11065.1  |                        5963.56 |                 0.154736  |                0.0574443 |                   47.4206 |                  18.9225 |                 10654.8 |                2267.76 |                    1.00885  |                   0.404042 |
| mid        |                        18907.7  |                        8449.39 |                 0.26442   |                0.0691469 |                   34.9425 |                  14.2111 |                 12604.2 |                2901.89 |                    1.46678  |                   0.446632 |
| sup        |                         5618.57 |                        3334.64 |                 0.0802834 |                0.0386786 |                   92.3018 |                  31.9212 |                  7587.1 |                1540.39 |                    0.727243 |                   0.346715 |
| top        |                        15722.3  |                        6903.76 |                 0.223272  |                0.0671611 |                   31.5417 |                  12.2147 |                 12040.8 |                2769.13 |                    1.28736  |                   0.406557 |

From this aggregated table, we could see the results from the graphs we concluded above more clearly. While bot players have highest damage to the enemy among the team, they also have highest total gold meaning they have taken the most resources in the team. However, when we talk about damaging effciency, mid players have higher damage per gold. Something interesting is that while support players have far highest visison score, they have both lowest damage to enemy and gold gained, indicating they have spent all gold on placing wards(such greatness of sacrificing!)

## Assessment of Missingness
Let's first recall the proportion of missingness of data in our cleaned dataset:
-patch                0.000953
-split                0.226839
-position             0.000000
-champion             0.000000
-result               0.000000
-damagetochampions    0.000000
-damageshare          0.000000
-visionscore          0.000000
-totalgold            0.000000
-damagepergold        0.000000
And I claim that the missingness of 'patch' to be NMAR for the following reason.
https://liquipedia.net/leagueoflegends/LPL/2023/Spring
## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis


