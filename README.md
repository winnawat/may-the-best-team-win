# may-the-best-team-win
Statistical take on how can we conclude that one team is better than the other in a competitive sports match.

At which point does winning a sport match becomes more about luck than skill? Making 1-2 mistakes too many at a critical point of a game can make a difference between Olympic gold and silver medals. Thus, watching Tokyo Olympic Games made me curious, **are gold medalists really better than silver or bronze medalists?** If so, how can we prove/test that?

## Using Statistics To Conclude Which Team Is Better - The Plan

The rough idea is to view each point in the match as a Bernoulli trial with the probability of team A winning the point as p while that of team B is (1-p).

### Hypothesis Testing
The next step will then be performing a binomial test on the total score of each team in the game. In this case, the H_0 is p = 0.5 or claiming that both teams are equally good. The H_1 is thus p != 0.5 or claiming that one team being better than the other.

The binomial test is equivalent to checking the probability of having the match score value be equal or more extreme than the value observed **given that p = 0.5** or P(observation|p=0.5)

And if this probability is less than the threshold, we cannot reject the hypothesis that p=0.5
As for the threshold, some reasonable number such as 20% would suffice. This would be equivalent to stating that we can afford to falsely crown one team as the winner 20% of the time despite both teams being equally good.

### Assumptions
1. Both teams play their best for evey single point, regardless of the point difference or the set they play in.
2. The probability of winning a point is constant throughout the game even as both teams get more exhausted.

## A Really Close Game

I will first pick one match to work on before trying to extend the idea to other matches.

The sample match used here is: https://olympics.com/tokyo-2020/olympic-games/en/results/badminton/results-mixed-doubles-fnl-000100-.htm

This is a badminton Mixed Doubles Gold Medal Match where the scores and competitors are:

|team|origin|player_name|match|game_1|game_2|game_3|
|---|---|---|---|---|---|---|
|A|CHN|ZHENG Si Wei, HUANG Ya Qiong|1|17|21|19|
|B|CHN|WANG Yi Lyu, HUANG Dong Ping|2|21|17|21|

Team A scored a total of 57 points while team B managed to score 59 points.

### Simulation
Simulating 500 matches. The red dotted line denotes the frequency that we observe team A scoring 57 points. We can see that the observed 57 points is quite close to the center of the distribution.

<img src="https://github.com/winnawat/may-the-best-team-win/blob/main/figures/chn_chn_hist.png" width="600" height="400">

### CDF
Next, we calculate the probability of observing team A getting 57 points or less. P(X <= 57) = 0.46

#### Verifying with R's built in binomial test
Running `binom.test(57, 116, 0.5, alternative = "less")` gives similar result.

## Another Game

The sample match used here is: https://olympics.com/tokyo-2020/olympic-games/en/results/badminton/results-men-s-doubles-qfnl-000100-.htm

This is a badminton Men's Doubles Quarterfinal Match where the scores and competitors are:
|team|origin|player_name|match|game_1|game_2|
|---|---|---|---|---|---|
|A|INA|GIDEON Marcus Fernaldi, SUKAMULJO Kevin Sanjaya|0|14|17|
|B|MAS|CHIA Aaron, SOH Wooi Yik|2|21|21|

### Simulation

Simulating 500 matches. The red dotted line denotes the frequency that we observe team A scoring 14 + 17 = 31 points out of 73 points played. We can see that the observed 31 points is further to the left than the previous example.

<img src="https://github.com/winnawat/may-the-best-team-win/blob/main/figures/ina_mas_hist.png" width="600" height="400">

### CDF

Now we look at the probability of observing team A getting 31 points or less if they played 73 points and the two teams are equally good. P(X <= 31) is 0.12

### Plotting the PDF
<img src="https://github.com/winnawat/may-the-best-team-win/blob/main/figures/ina_mas_pdf.png" width="600" height="400">

# So How Many Points Should They Play?
