# Data harvest strategy

## Definitions

|Game end label|Description|
|-|-|
|Success| Indicates the player found all responses before the end of the timer. |
| Unfinished | Indicates the player went up to the timer end, but did not have the time to find all the reponses. |
| Giving up | Indicates the player gave up before timer ends. This can be done by either clicking on "Give up" button or leaving the website (unloading page event) |
 

## General rules

Unexpected end of sessions does not trigger data gathering. Only call-to-actions are accounted.

The current language is always taken into account. If the language received is unknown (in case of external misuse of our API) then default to english.

## Map statistics

At the end of a game, successful or given up, regardless of the game mode, increments its value for the given map type

## Gamemode statistics

At the end of a game, successful or given up, regardless of the game mode, increments its value for the given gamemode type

## Success or give up statistics

At the end of a game, successful or given up, increments the `play_count` value for each game played and increments `give_up_count` when the player gives up, taking into account the user's language for the game mode and the given map.

The value `unfinished_count` is computed with the values
```
(play_count - ( give_up_count + success_count ))
```



## Game statistics

At the end of a game, successful or given up, for each data concerned by the type of map, increments or not the value "found_count" according to if the data was found by the player, and increments the value "play_count" anyway.