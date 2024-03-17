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
- *totalgold*: is the total gold of the player gained in teh whole match
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Data Cleaning and Exploratory Data Analysis
After loading the dataset, we need to first select the above columns from the original dataset by specifying the column neams. Then we need filter out all rows of team data from the dataset by slicing the "postion" columns. After this, we check all none values in each column to make sure they are in explainable extent(notice that it is common that there are many none values in "split" column because certain  matches hold only once a year so they have no splits definitions). Finally, we add one more column called "damage per gold" by dividing the "total damage" by the "total gold" as the most direct anaylyzing factor. After cleaning, here is the head of our dataset:

| # | Patch | Split | Position | Champion | Result | Damage to Champions | Damage Share | Vision Score | Total Gold | Damage per Gold |
|---|-------|-------|----------|----------|--------|---------------------|--------------|--------------|------------|-----------------|
| 0 | 13.01 | Spring | Top | Jax | 1 | 14283 | 0.150027 | 49 | 18855 | 0.757518 |
| 1 | 13.01 | Spring | Jungle | Poppy | 1 | 6219 | 0.065324 | 61 | 12082 | 0.514733 |
| 2 | 13.01 | Spring | Mid | Taliyah | 1 | 27028 | 0.283899 | 49 | 15722 | 1.719120 |
| 3 | 13.01 | Spring | Bot | Ezreal | 1 | 42005 | 0.441215 | 47 | 17332 | 2.423552 |
| 4 | 13.01 | Spring | Support | Karma | 1 | 5668 | 0.059536 | 106 | 8816 | 0.642922 |


Univariate Analysis:
<iframe
  src="assets/damage_Share_by_position.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Bivariate Analysis:
## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis


