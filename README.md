# random-letter-picker

A mini Vue application that picks a random letter and shows it after a 5 second countdown.

## Why?

### Stadt-Land-Fluss
I don't know if other countries have this, but in Europe we have a game called "Stadt-Land-Fluss" (city, country, river).

At the beginning, the players decide on the game categories. Originally: city, country and river. But it can be extended to any number of categories and can be more than 3. For example: food, celebrity, company, etc.

### Rounds
Each round goes as follows:
 - One player counts letters A-Z in their head
 - The player on the left of the first player says "stop" after a while
 - First player then says out loud the letter he was currently counting
 - Now the round starts!
 - Each player writes as fast as they can an item in each category, starting with the chosen letter
 - First player to fill in all categories says "stop" out loud
 - All players stop writing (variation: they can finish the word they were writing)

### Scores
For each category, scores are being added:
 - When one player is the only one who has a valid word of the category: 20 points
 - When multiple players have a valid word of the category: 10 points
 - **UNLESS**: More than one player have the same valid word, for those players: 5 points
 - When a player has no valid word for the category: 0 points

After all 26 rounds (1 per letter) are done, the points for each round is added per player.
The player with the highest score wins.

### Problems
This is a fun game once in a while, but it has two major flaws:
 - Cheating: The player counting in their head the letters can pre-think of a letter and prepare answers so he can finish fast
 - Unconvenience: The first couple of rounds it's all good. But soon the letters repeat. And the letter counting has to proceed until an unused letter is found

## Use

This little application eliminates both [problems](#Problems) of the game.

Using the app is easy:
 - Click `Pick letter`
 - The randomly chosen letter appears after 5 seconds

To delete a letter from the used letter pool, click that letter.

To restart the game, click `Restart`

## Demo

You can find a demo here:

https://letterpicker.marc.dev

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Run your tests
```
yarn run test
```

### Lints and fixes files
```
yarn run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
