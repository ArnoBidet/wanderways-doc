# Map's list


!!swagger map.yaml!!


**If you don't see an OpenApi like display upon this message, this means an error occured, please reload page to see it.**

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

Uses the header `Accepted-Language` to determine map translation.

### Example
```json
[
  {
    "id_map": "FRANCE_REGIONS",
    "map_label": [
      "Régions françaises"
    ],
    "tags": [
      "TAG_FRANCE",
      "TAG_SUBDIVISIONS",
      "TAG_EUROPE"
    ],
    "map_description": [
      "Chefs-lieux des 13 régions de France métropolitaine"
    ],
    "url_wiki": "",
    "play_count": 0
  },...
]
```

## Associated SQL Request

```sql
CREATE OR REPLACE FUNCTION get_translations(in lang_id CHAR(5), in item_id VARCHAR(50), out result text)
    AS $$ SELECT string_agg(t.translated_value, '||')
        FROM translation t
        WHERE t.id_lang = lang_id
        AND t.id_item = item_id $$
    LANGUAGE SQL;


CREATE OR REPLACE FUNCTION map_list (
	id_lang char(5)
) 
RETURNS TABLE (
	id_map VARCHAR(50),
	map_label TEXT,
	map_description TEXT,
	tags TEXT,
	url_wiki VARCHAR(250),
	play_count INT
) 
language plpgsql
as $$
declare 
    var_r record;
begin
	for var_r in(
            SELECT m.id as id_map,
            get_translations(l.id, m.id) as map_label,
            get_translations(l.id, m.id_description) as map_description,
            (SELECT string_agg(tm.id_tag, '||') FROM tag_map tm WHERE  tm.id_map = m.id)  as tags,
            m.url_wiki,
            COALESCE(ms.play_count,0) as play_count
            FROM map m
            LEFT JOIN lang l
            ON l.id = id_lang
            LEFT JOIN map_statistic ms
            ON ms.id_map = m.id
        ) loop
        id_map := var_r.id_map;
        map_label := var_r.map_label;
        map_description := var_r.map_description;
        tags := var_r.tags;
        url_wiki := var_r.url_wiki;
        play_count := var_r.play_count;
           return next;
	end loop;
end; $$

SELECT * FROM map_list('fr-FR')
```