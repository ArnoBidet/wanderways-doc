# End

<style>.scheme-container{display:none;}</style>

!!swagger end.yaml!!

## Associated SQL Request

```sql
UPDATE map_statistics
SET play_count = play_count + 1
WHERE id_map = :ID_MAP
AND id_lang = :ID_LANG;

UPDATE gamemode_statistics
SET play_count = play_count + 1
WHERE id_map = :ID_MAP
AND id_lang = :ID_LANG;

UPDATE game_statistics
SET found_count = found_count + 1
WHERE id_gamemode = :ID_GAMEMODE
AND id_lang = :ID_LANG
AND id_map = :ID_MAP
AND id_map_data IN(:ID_MAP_DATA, "FR_01", "FR_02", ...);

UPDATE success_or_give_up_statistics
SET play_count = play_count + 1
WHERE id_gamemode = :ID_GAMEMODE
AND id_lang = :ID_LANG
AND id_map = :ID_MAP;
```
