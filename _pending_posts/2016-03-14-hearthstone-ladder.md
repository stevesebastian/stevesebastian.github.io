---
layout: post
title: Reaching Legend in Hearthstone
description: On the ladder
---

Hearthstone: Heros of Warcraft is an online card game where players build decks and play via the internet. In Hearthstone, players compete in head-to-head matches in order to advance up a ranked ladder. To advance to the next rank, a player must win a certain number of stars. Each win gains the player a star, and each loss removes a star. Win streaks of 3 or more give bonus stars, but only below rank 5. One of the main goals of Hearthstone is to climb from rank 25 to 1, and then ascend into the "Legend" rank, a goal which only about [0.5% of players worldwide achive](http://us.battle.net/hearthstone/en/blog/15955974/hearthside-chat-youre-better-than-you-think-9-18-2014). 

Given that such a small number of players reach Legend rank, is the dream of Legend realistic for an average player?

## Simulating the Hearthstone ladder in Python

In order to answer the question of reaching Legend in Hearthstone, I wrote a simple Monte Carlo simulation using Python to simulate a player advancing up the ladder. In this simulation the player



{% highlight python %}
def simulate_ladder(numSimulations, maxGames, winRateSub5, winRateAt5):

    gameArray = []
    
    for s in range(0,numSimulations):
        starArray = []
        gameIndex = 0
        numStars = 0
        winStreak = 0
        
        while gameIndex < maxGames and numStars < 95:
            if(numStars < 70):
                winRate = winRateSub5
            else:
                winRate = winRateAt5

            win = np.random.binomial(1, winRate)
            if(win):
                numStars += 1
                winStreak += 1
                if(winStreak >= 3 and numStars < 70):
                    numStars += 1
            elif(numStars > 10):
                numStars -= 1
                winStreak = 0
            else:
                winStreak = 0    
            gameIndex += 1
            starArray.append(numStars) 
        
        gameArray.append(gameIndex)

    return gameIndex, gameArray, starArray  
{% endhighlight %}



## Win rate and reaching Legend

Because of the [random nature](http://hearthstone.gamepedia.com/Random_effect) of Hearthstone and the ever evolving meta game, even the best players struggle to achive a win rate of greater than 60%. However, it is theoretically possible to reach Legend rank with an overall win rate as low as 50% (escpeially given the win streak bonus at lower ranks). 

An average Hearthstone game lasts around 10 minutes, so a casual player who plays a few hours at a time can expect to play 10-15 games per day, or around 400 games per month.  Given this, what  win percenta


## Win rate and game time

The Hearthstone ladder resets at the beginning of each month, so it is important for players climb the ladder as quickly as possbile if they want to reach Legend. 

The cards in Hearthstone support a number of deck types. Some focus on ending the game quickly, while others seek to win the long game. Because of this, the average time per game can vary widely based on the deck you choose. Would a player who wants to reach legend be better off with a deck that finishes games quickly, even if the win rate wasn't as high? In other words, what is the trade off between time and win percentage?

Data on average game length by deck type are difficult to find. 