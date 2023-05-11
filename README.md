
# Monty Hall Problem

The Monty Hall problem is a famous probability puzzle in AI, named after the host of a game show called "Let's Make a Deal", which was hosted by Monty Hall. The problem involves a contestant, three doors, and a prize behind one of the doors.

## The game proceeds as follows:

1. The contestant is asked to choose one of three doors, without knowing which door has the prize behind it.
2. After the contestant has made their choice, the host, who knows which door has the prize, opens one of the other two doors to reveal that it does not have the prize behind it.
3. The host then gives the contestant the option to switch their choice to the remaining unopened door, or to stick with their original choice.

## The question is: Is it better for the contestant to switch their choice or to stick with their original choice?

The answer is counterintuitive and often surprises people who are not familiar with probability theory. The optimal strategy is to switch, as this gives the contestant a higher probability of winning the prize. The probability of winning if the contestant switches is 2/3, while the probability of winning if the contestant sticks with their original choice is only 1/3. This is because when the contestant switches, they effectively choose the door that was not opened by the host, which has a 2/3 probability of having the prize behind it.


### Solution
```
import random
import matplotlib.pyplot as plt
```
Defining a function to simulate the game:
```
def monty_hall(switch=False):
    # Initializing the doors as 0,1,2
    doors = [0, 1, 2]
    # Randomly selecting the door with the prize
    prize_door = random.choice(doors)
    # Person selects a door
    chosen_door = random.choice(doors)
    # Host revealing one of the other doors without the prize
    revealed_door = random.choice([door for door in doors if door != prize_door and door != chosen_door])
    if switch:
        # Person switches to the other unopened door
        chosen_door = [door for door in doors if door != chosen_door and door != revealed_door][0]
    # Determine if the person won
    return chosen_door == prize_door
```
Running the simulation for a large number of trials, and keep track of the number of wins and losses for both switching and not switching:
```
# Let Number of trials
n = 10000

# Initializing counters
switch_wins = 0
switch_losses = 0
stay_wins = 0
stay_losses = 0

# Simulate the game n times
for i in range(n):
    # Switch
    if monty_hall(switch=True):
        switch_wins += 1
    else:
        switch_losses += 1
    # Don't switch
    if monty_hall(switch=False):
        stay_wins += 1
    else:
        stay_losses += 1
```
Finally, printing out the results and creating a bar chart to visualize them:
```
# Printing results
print(f"Switching wins: {switch_wins/n:.2%}")
print(f"Switching losses: {switch_losses/n:.2%}")
print(f"Not switching wins: {stay_wins/n:.2%}")
print(f"Not switching losses: {stay_losses/n:.2%}")

# Creating bar chart
fig, ax = plt.subplots()
ax.bar(["Switching Wins", "Switching Losses", "Not Switching Wins", "Not Switching Losses"],
       [switch_wins/n, switch_losses/n, stay_wins/n, stay_losses/n])
ax.set_ylabel("Probability")
ax.set_title("Monty Hall Problem")
plt.show()
```
#### Output

Switching wins: 67.37%\
Switching losses: 32.63%\
Not switching wins: 33.89%\
Not switching losses: 66.11%

## Barchart

![](https://github.com/i-amritpal/Monty-Hall-Problem/blob/main/download.png)
