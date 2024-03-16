# lol_role_analysis
By Zening Wang and Chenxi Li
## Introduction
Our dataset comprises the entire professional match statistics for the game League of Legends throughout 2023. Each match is represented by 12 rows, including one for each player and one for each team, with over 100 columns capturing various dimensions of data. Our primary question is focused on determining which role carries the most impact in professional matches during 2023, specifically between Mid and Bot players.
We have narrowed down our investigation to these two roles because, in professional matches, they are typically regarded as the primary carrying positions, while other roles such as Top, Jungle, and Support intentionally allocating resources such as minions and kills to them. 

It's important to note that there are numerous ways to define "carry" in League of Legends like vision score, damage taken, crowd control etc.. For this analysis, we will use the straightforward metric of "damage dealt". However, to provide a more comprehensive evaluation considering the resources acquired by each role, we will compare using the metric "damage per gold." This approach aims to assess which role, whether the mage (often found in Mid) or AD carry (Bot), is more efficient in dealing damage to the enemy team relative to the resources invested. Through this analysis, players and teams might be able to reconsider resources distribution and tactical priority of among the 5 roles.

After cleaning and filtering the original dataset, we keep 9 columns in total: *patch*, *split*, *position*, *champion*, *result*, *damagetochampions*, *damageshare*, *visionscore*, *totalgold* and one added column *damagepergold*. We choose these columns because basically these consist of all measurements of "carrying" and we also keep record of the patch and time data for further anlysis. After excluding team data rows, we have 104920 rows remaining.

Explanation of columns:
- *patch* is the game patch of this match take place at
- *position* is the specfic role of the player
- *champion* is the champion selection of the player
- *result* is the boolean result of this match(1 for win, 0 for lose)
- *damagetochampions* is the damage of the player deals to enemy champions
- *damageshare* is the ratio proportion of the damage the player has to the whole team
- *visionscore* is the vision of the team this player has influenced
- *totalgold* is the total gold of the player gained in teh whole match

## Data Cleaning and Exploratory Data Analysis

## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis


