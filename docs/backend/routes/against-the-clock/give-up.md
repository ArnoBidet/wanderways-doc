# Give up

Tells the server that the player gave up.

## Api endpoint

Method : `POST`

Url : `/api/against-the-clock/give-up`

## Request headers

|Header name| Value |
|-|-|
|cookie|session-id|
### Input parameters

- Path : *none*
- Body : *none*
- Query : *none*

## Output

`HTTP 200 OK`

## Associated SQL Request

```sql
UPDATE success_or_give_up_statistics
SET play_count = play_count + 1, give_up_count = give_up_count +1
WHERE id_map = :MAP_ID
AND id_gamemode = :GAMEMODE_ID
AND lang_id = :LANG_ID;

UPDATE map_statistics
SET play_count = play_count + 1
WHERE id_map = :MAP_ID
AND lang_id = :LANG_ID;

UPDATE gamemode_statistics
SET play_count = play_count + 1
WHERE id_gamemode = :GAMEMODE_ID
AND lang_id = :LANG_ID;

UPDATE game_statistics
SET found_count = found_count + 1
WHERE  id_map = :MAP_ID
AND id_gamemode = :GAMEMODE_ID
AND lang_id = :LANG_ID
AND id_map_data = :ID_MAP_DATA;
```

<!-- @TODO create sequence diagram or sth

Séquence de traitements backend particuliers :
- Une requête arrive, elle a une id de session (si l’utilisateur envoie un cookie, c’est forcément qu’il est encore dans les temps, puisque max-age. mais dans le cas où il modifirait le max age, si il est après la durée max de la partie, alors on renvoie un 400)
- La session est récupéré
- On vérifie que pour la partie associée à la session, les temps semblent correct pour ne pas être de la triche
- En fonction de si les temps sont corrects, deux cas :
    - réponse 200 si correct
    - réponse 400 si incorrect, le frontend doit indiquer au joueur qu’il est suspecté de triche et que donc les données anonymisées ne seront pas sauvegarder
- si correct, alors on enregistre les données statistiques en bases
- Quoi qu’il arrive on ferme la session et on nettoie. -->