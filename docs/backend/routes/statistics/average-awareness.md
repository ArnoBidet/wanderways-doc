# Average awareness


!!swagger average-awareness.yaml!!


## Typescript schema

```ts
interface AverageAwareness {
  play_count : number,
  data : {
    id_data : string,
    found_count : string
  }[]
}
```

### Example

```json
{
  "play_count" : 700,
  "data":[{
    "id_data":"FR-01",
    "found_count":40
  },{
    "id_data":"FR-02",
    "found_count":20
  },{
    "id_data":"FR-03",
    "found_count":150
  }]
}
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