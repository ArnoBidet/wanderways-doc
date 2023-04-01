# Games

On this page, you will have more hindsights on the games we implemented or want to implement.

## Discussion on games

Wanderways revolves around games to learn maps. But, choosing and defining what is good or not can be quite difficult. Here is a short description of the game that are planned for V1.

- Against the clock : There is a map and a timer displayed. The player must type as fast as they can the geographical datas relative to the map they are on.
- Quizz : Could be of many types. Adapted to learn flags, but also another mean to learn maps. Could also be a funny quizz with exotic questions.

To parralel this method with other :

|Method|Benefits<span class="good">↗</span>|Flaws<span class="bad">↘</span>|
||-|-|
|Tapping|- Teaches countries spelling.<br>- Teaches countries neighbours (useful to understand geopolitical issues)<br>- Ordered learning. You can go the way you want, beginning with south africa, going upwards the west coast ? That's your choice.<br>- Challenging (can be good depending on the user)|- Hard, you need to be determined. Though, maps can be splitted in sub-regions, making it more friendly.<br>- **Unfit for mobile devices**<br>- How to deal with close names ? E.g : "Loire" and "Loiret"|
|Quizz|- If you don't know, you've got 25% chance of randomly be right.<br>- Beginner friendly|- Player doesn't learn what neighbours a country has.<br>- Unordered learning|
|User pin|- Good location memorisation |- Player doesn't learn what neighbours a country has.<br>- Unordered learning|

***Quizz guided method - A short description***

The user has a map displayed. A country gets colored. 4 cards appear, each containing a potential answer. The user has to choose which one corresponds to the colored country.

***User pin on the map method - A short description***

The user has a map displayed. A country name appears. The user has to click on the map at the location where they think the country is located at.



## Against the clock

This is the main game of Wanderways.

A map, a text input, a list of found responses, a timer and a progress bar are displayed.


### Rules

- Once the game starts, the timer cannot be stopped.
- A give-up button allows the player to quit early.
- Leaving the page is considered giving-up (if page unload event caught normally).


### Technical details and point of interest

#### How do you know the user's answer is good ?

A user answer is good as long as it matches one of the data in the data list.

If only it was that easy. Let's see what triggers data validation and list special cases.

A data validation process is triggered when a user tap a character in the input. That's the only thing that trigger validation.

Now, let's see what could go wrong :

- A data can have accentuated character (diacritics) depending on the language : `Côte d'or`. Though, depending on the keyboard, they can be quite complicated to perform.
- A sequence of character can match a data too early. E.g : `Loire` and `Loiret`. You wanted to type `Loiret` and it instantly validates `Loire`. Well, that's okay. But now we don't want it to tell us `data already found` when we type `loire` to then tap `Loiret`
- A data can have multiple names. Such as `Birmanie`, also known as `Myanmar` in french.

So, let's schematize !

```mermaid
---
title: Flowchart describing the data validation process
---
flowchart LR
    user_input(User input) --> normalize_input
    subgraph Validation
      normalize_input(Normalize input) --> is_valid_data{Is valid<br>data ?}
      is_valid_data -->|Yes| is_already_found{Is already<br>found ?}
      is_already_found -->|No| longer_data_exists{Does a data that<br>is not found exists with<br>the same base ?}
    end
    is_valid_data -->|No| no_match[No match]
    is_already_found -->|Yes| no_match[No match]
    longer_data_exists -->|No| no_match[No match]
    longer_data_exists -->|Yes| match[Match]
```

Details :

- `Normalize input` means going from `Côte d'or` to `cote-d-or`. This normalization process is also applied to all the data that we compare to.
- `Is valid data` does multiples loops. The main on all data, then on each data translations.

#### How do we know which kind of end the player reached ?


```mermaid
---
title: State diagram descrbing game end status tree 
---
stateDiagram-v2
    state "In game" as in_game
    state "Success screen" as success_screen
    state "Fail screen" as fail_screen

    state if_give_up <<choice>>

    [*]--> in_game :Game starts
    in_game --> if_give_up

    if_give_up --> fail_screen : gives up
    if_give_up --> fail_screen: did not find all
    if_give_up --> success_screen: found all

    fail_screen --> [*]
    success_screen --> [*]
```

### Concerns about cheating

We can't stop player from having a list of data open in another window. That's a fact, there is no point fighting it.

But, we want to stop people that would try to bypass normal rules of typing to finish the game quicker than humanly possible.

The first thing is to ensure that the control on the game isn't client sided. All along the game, when a good response (evaluated by the client) is found, it is send to the server for validation. The server has the autorithy on wether or not the data was valid, and if the game has ended or not.

But a player could still automate calls to send X requests for each data in a loop. Protection against that is achieved through average time between key stroke verification. If on the total number of data, we find that the user typed faster than the work record, then it will be considered cheating and won't be stored as statistics of any kind.


### Design

#### Zonning



<style>
  .container{
    width:100%;
    aspect-ratio:16/9;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(8, 1fr);
    grid-column-gap: 15px;
    grid-row-gap: 15px;
  }
  .map, .input, .sidemenu{display:flex; align-items:center;justify-content:center;}
  .map { grid-area: 1 / 1 / 9 / 4; background-color:#FF000088;}
  .input { grid-area: 7 / 2 / 7 / 3; background-color:#00FF0088; }
  .sidemenu { grid-area: 1 / 4 / 9 / 5; background-color:#0000FF88; gap:1rem; flex-direction:column; padding:0.5rem;}
  input{padding:0.5rem;}
  button{background-color:white; padding : 0.5rem;}
  .result-container{display:flex; flex-direction:column;width: 100%;padding: 0.5rem; color:white; max-height:6rem; overflow: auto;}
  .result-container div{ height:2rem;}
</style>

<div class="container">
  <div class="map">Map</div>
  <div class="input">
    <input type="text" placeholder="User responses">
  </div>
  <div class="sidemenu">
    <span>Timer</span>
    <span>Current score <br>/ max score</span>
    <button>Give up</button>
    <div class="result-container">
      <span>Result list</span>
      <div>Result line 1</div>
      <div>Result line 2</div>
      <div>Result line 3</div>
      <div>Result line 4</div>
      <div>Result line 5</div>
    </div>
  </div>
</div>

*Note : Does not correspond to final game zonnning, this is for visualization purpose*


#### Mockups

More on mockup on [frontend section](@TODO)

Latest version : 

<img src="assets/games/against-clock-latest-mockup.png">

Old versions :

*One of the very first versions, when the project was named "Learn your maps"*

<img src="assets/games/against-clock-old-mockup.png">

