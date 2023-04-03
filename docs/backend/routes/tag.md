# Tag's list

!!swagger tag.yaml!!

The label translations follows the given `Accepted-Language` http header.

## Typescript schema

```ts
interface Tag{
    id : string,
    label : string,
    tags : {
        id : string,
        label : string
    }[],
}
```

### Example
```json
[{
   "id" : "CONTINENTS",
   "label" : "Continents",
   "tags" : [{
      "id" : "EUROPE",
      "label" : "Europe"
   },{
      "id" : "ASIA",
      "label" : "Asie"
   },{
      "id" : "AFRICA",
      "label" : "Afrique"
   }],
}]
```

## Associated SQL Request

```sql
CREATE MATERIALIZED VIEW mv_tag_list AS
SELECT l.id as id_lang,
    t.id as id_tag,
    t.id_group,
    get_translations(l.id, t.id) as label,
    get_translations(l.id, t.id_group) as group_label
FROM tag t,
    lang l
ORDER BY l.id,
    t.id_group,
    group_label,
    label;

SELECT * FROM mv_tag_list;
```