# Tag's list

Get the tags and tag groups.

## Api endpoint

Method : `GET`

Url : `/api/tag/list`

## Input parameters

- Path : *none*
- Body : *none*
- Query : *none*

## Output

### Schema
```ts
interface Tag{
    id_tag_group : string,
    label : string,
    tags : {
        id_tag : string,
        label : string
    }[],
}
```

### Example
```json
[{
   "id_tag_group" : "CONTINENTS",
   "label" : "Continents",
   "tags" : [{
      "id_tag" : "EUROPE",
      "label" : "Europe"
   },{
      "id_tag" : "ASIA",
      "label" : "Asie"
   },{
      "id_tag" : "AFRICA",
      "label" : "Afrique"
   }],
}]
```

## Associated SQL Request

```sql
SELECT DISTINCT tg.id as id_group, t.id as id_tag, tr.translation as tag_label, tr2.translation as tag_group_label
FROM tag t, tag_group tg, languages l , translations tr, translations tr2
WHERE l.id = "fr-FR"
AND t.id_group = tg.id
AND tr.id_lang = l.id
AND tr.id_item = t.id
AND tr2.id_item = tg.id
ORDER BY tg.id;
```