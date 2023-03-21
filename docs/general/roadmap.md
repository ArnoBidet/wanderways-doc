# Roadmap

## V1

Below, the defined perimeter of the first version of the website.

### Games

### Statistics

One of the added values of the site are the statistics.
By playing on our site, a user must agree to have anonymized data collected for statistical purpose.

To know more, check [data harvesting stategy](./backend/data-harvest-strategy.md).

These data will then serve as a mean to do the following :

- When a player fails (or succeeds, but this is less interesting), we collect what he has found or not. So, when you finish a game, you can see if what you found, the other players find it or not.<br>We decided to call this type of statistic "**Average awareness**".

### Maps

WanderWay is a website with the main purpose of learning maps.
Those maps are of the following types : 

|Type|Definition|
|-|-|
|Countries| We are where space is mainly divided between sovereign country. Those coutries are divided in groups, be it by continents, politic/economics (Europe, Mercosur, NATO...) and others|
|Subdivisions|These countries are often divided in subdivisions. Some times at multiple level.|
|Cities|Cities can be of many kinds. In wanderways, we treat main cities by level of subdivision. To take a concrete example : In france there is 2 level of subdivisions. Each have their capitals. Thus, Maine-et-Loire has Angers as its capital. But Maine-et-Loire is a department from the region Pays de la loire whose capital is Nantes. And finally Pays de la loire is a region of the country france whose capital is Paris.<br>And some countries even have 2 capitals or more. This topic is discussed on [game page](./games.md)|

As for V1, the following maps are meant to be available :

|Type|Name|
|-|-|
|Subdivision - Lvl 1|French regions|
|Cities of Subdivision - Lvl 1|French regions' capital|
|Subdivision - Lvl 2|French departments|
|Cities of Subdivision - Lvl 2|French departments' capital|
|Subdivision - Lvl 1|Japan regions|
|Cities of Subdivision - Lvl 1|Japan regions' capital|
|Subdivision - Lvl 2|Japan prefectures|
|Cities of Subdivision - Lvl 2|Japan prefectures' capital|
|Countries|UN Countries|
|Capital of Countries|UN Countries' capital|
|Countries|ISO3166 Countries|
|Capital of Countries|ISO3166 Countries' capital|


### FAQ

The site has a will to answer to questions that arise with maps.

Indeed, after spending time on our games, people will ask themselves questions such as :

- How the maps are chosen ?
- How did they decide what is a country or not ?
- Why such a country has such a capital (e.g. Bouvet Island which has no capital, still has Bouvet in capital, while the island is completely deserted),
- On political subjetcs such as Israel, or Western Sahara.

That's why it is planned that a FAQ page will be created. 


## Later

### User account
A nice aspect for those who like to have a trace of what they have succeeded or not, we allow the creation of accounts:
- For a logged-in user (see next part), retrieve the time taken to finish a map, and record whether he won or not. As well as other statistics mentioned below
- Earn badges (e.g.: "Cocorico" when the player finishes the France map, all maps combined, or "Good player" when the player has played more than 20 times)
- Be able to bookmark maps
- Be able to bookmark game modes (limited interest)
- To have a follow-up of the successful maps according to the mode of play (interest to not have OR too many modes of play OR too many maps, history not to give an impression of submersion (while doing, to limit the number of mode of play is the simplest and the most interesting in term of interest for the player. What's the point of making a map in 30 game modes when you've done it in the main version?))


### New gamemode

### More maps
