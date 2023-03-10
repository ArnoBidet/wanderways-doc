# Average awareness

By game mode and map, for each element X, on the sum of played game, the number of player that found X element.

## Api endpoint

Method : `GET`

Url : `/api/statistics/average-awareness/:GAME_MODE/:ID_MAP?lang=:ID_LANG`

## Input parameters

- Path :
  - GAME_MODE : the gamemode's id. E.g :  `GAMEMODE_AGAINST-CLOCK`
  - ID_MAP : The map's id
- Body : *none*
- Query : `ID_LANG` : The language id. If not present, then takes all languages.

## Output

### Schema
```ts

```

### Example
```json

```

## Associated SQL Request

```sql
SELECT gs.id_map_data, gs.found_count
FROM gamemode_statistics gs
WHERE gs.id_gamemode = :ID_GAMEMODE
AND gs.id_map = :ID_MAP [AND gs.id_lang = :ID_LANG];

SELECT SUM(sogus.play_count)
FROM success_or_give_up_statistics sogus
WHERE sogus.id_gamemode = :ID_GAMEMODE
AND sogus.id_map = :ID_MAP [AND sogus.id_lang = :ID_LANG];
```