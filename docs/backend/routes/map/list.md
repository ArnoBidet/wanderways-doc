# Map's list


!!swagger list.yaml!!


## Typescript schema

```ts
interface Map {
   id_map : string,
   label : string,
   tags : string[],
   description : string,
   url_wiki : string,
   play_count : number // language agnostic by default for map list
}
```

### Example
```json
[{
   "id_map" : "FRANCE_DEPARTEMENT",
   "label" : "France - Département",
   "tags" : [
        "FRANCE",
        "EUROPE",
        "SUBDIVISIONS"
   ],
   "description" : "Départements de france métropolitaine et d’outre mer",
   "url_wiki" : "https://wikipedia.com/example",
   "play_count" : 700 // language agnostic by default for map list
   
}]
```

## Associated SQL Request

```sql
SELECT m.id as id_map,
(SELECT t.translation FROM translations t WHERE t.id_lang = l.id AND t.id_item = m.id)  as label,
(SELECT GROUP_CONCAT(tm.id_tag) FROM tag_map tm WHERE  tm.id_map = m.id)  as tags,
(SELECT t.translation FROM translations t WHERE t.id_lang = l.id AND t.id_item = m.id_description)  as description,
m.url_wiki,
ms.play_count
FROM map m, map_statistics ms, languages l 
WHERE ms.id_map = m.id 
AND l.id = "fr-FR"
```