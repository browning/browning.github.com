---
layout: post
title: "NBA MVP Logistical Regression"
description: ""
category: 
tags: []
---
{% include JB/setup %}

I'm taking the mlclass from coursera right now and decided to apply a logistical regression classification on nba players to try and determine who will be voted the MVP. The model looked at the common individual stats as well as the team winning percentage. Obviously this model tries to model the voters opinions on who should be the mvp and doesn't necessarily classify the *best* player.

I looked at the past 30 years of MVPs and ran the model on each season. 

In R, here is a definition of the model:


    > mvpmodel
    
    Call:  glm(formula = MVP ~ GAMES + PPG + RPG + APG + SPG + BPG + WINPCT, 
        family = binomial(link = "logit"))

    Coefficients:
    (Intercept)        GAMES          PPG          RPG          APG          SPG 
             BPG       WINPCT  
     -32.919831     0.004281     0.369791     0.365068     0.541685     0.364045     
            0.505713    19.610476  
    
    Degrees of Freedom: 16611 Total (i.e. Null);  16604 Residual
    Null Deviance:      562.2 
    Residual Deviance: 158.2  AIC: 174.2 
    > 

After the model was created, I ran it on every player over the past 30 years to find the likelihood that they would be choosen MVP. Then I sorted the list and found the top 10 most dominant MVP-esque seasons over the past 40 years:

    1) Kareem Abdul-jabbar 1971 9.805001e-01
    2) Shaquille O'neal 1999 9.585589e-01
    3) Artis Gilmore 1971  9.331693e-01
    4) Kareem Abdul-jabbar 1970  9.279581e-01
    5) Larry Bird 1984 8.509291e-01
    6) Kareem Abdul-jabbar 1973 8.455859e-01
    7) Michael Jordan 1995 8.435103e-01
    8) LeBron James 2008 8.339901e-01
    9) Magic Johnson 1986 8.267087e-01
    10) Michael Jordan 1991 8.180643e-01

The only one of those guys to not actually win the MVP was Artis Gilmore. Its a shame because his numbers in 1971 were ridiculous! 24 points 18 rebounds 5 blocks on a team that won 80+% of their games.

Next I ran the model on each year of performances to find out who the model thinks should have been voted for MVP. Then I compared it to who actually was voted MVP. Its kind of interesting because it highlights the years when the voting might have been controversial. Like the steve nash MVPs of recent years.

    YEAR  ACTUAL_MVP      MODEL_PREDICTED_MVP
    1970  Kareem          Kareem
    1971  Kareem          Kareem
    1972  Dave Cowens     Kareem  
    1973  Kareem          Kareem
    1974  Bob Mcadoo      Julius Erving
    1975  Kareem          Julius Erving
    1976  Kareem          Kareem
    1977  Bill Walton     Bill Walton
    1978  Moses Malone    Kareem
    1979  Kareem          Kareem
    1980  Julius Erving   Julius Erving
    1981  Moses Malone    Larry Bird
    1982  Moses Malone    Moses Malone
    1983  Larry Bird      Larry Bird
    1984  Larry Bird      Larry Bird
    1985  Larry Bird      Larry Bird
    1986  Magic Johnson   Magic Johnson
    1987  Michael Jordan  Larry Bird
    1988  Magic Johnson   Magic Johnson
    1989  Magic Johnson   Michael Jordan
    1990  Michael Jordan  Michael Jordan
    1991  Michael Jordan  Michael Jordan
    1992  Charles Barkley Charles Barkley
    1993  Olajuwon        David Robinson
    1994  David Robinson  David Robinson
    1995  Michael Jordan  Michael Jordan
    1996  Karl Malone     Michael Jordan
    1997  Michael Jordan  Shaq
    1998  Karl Malone     Karl Malone
    1999  Shaq            Shaq
    2000  Iverson         Shaq
    2001  Tim Duncan      Tim Duncan
    2002  Tim Duncan      Tim Duncan
    2003  Kevin Garnett   Kevin Garnett 
    2004  Steve Nash      Dirk Nowitzki
    2005  Steve Nash      Lebron James
    2006  Dirk Nowitzki   Dirk Nowitzki
    2007  Kobe Bryant     Kobe Bryant
    2008  Lebron James    Lebron James
    2009  Lebron James    Lebron James

I only had data up until 2009 for this*

Finally I wanted to see if the MVP has changed meaning over the years. Like today the mvp is usually given to the best player on the best team, but in the past maybe it was given to the best player even if they were on a really bad team. If anything, the opposite is true, but really there isn't much trend to speak of. Here is a chart of the MVP's team rank over the past 50 years ( 1 is the best ). Also keep in mind the league has added teams over these years.

<img src ="/assets/images/mvpranks.png"
alt="MVPS by year" width='337' height='350' ></img>

Chart of MVP team ranks by year