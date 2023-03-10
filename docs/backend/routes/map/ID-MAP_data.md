# Map's data

Get all the datas for a given map

## Api endpoint

Method : `GET`

Url : `/api/map/:ID_MAP/data/`

## Input parameters

- Path : `ID_MAP` : The identifier of the map. E.g : `FRANCE_DEPARTMENTS`
- Body : *none*
- Query : *none*

## Output

### Schema
```ts
interface MapData{
    id: string,
    data_translation : string[],
    flag_url: string,
    group: {
        id: string,
        data_translation : string[]
        flag_url: string,
        group: null,
        capital: null,
        numeric_code: string
    } | null,
    capital:{
        id: string,
        data_translation : string[]
        flag_url: string,
        group: null,
        capital: null,
        numeric_code: string
    } | null,
    numeric_code: string
}
```

### Example
```json
{
    "id": "FR-01",
    "data_translation" : ["Ain"],
    "flag_url": "https://example...",
    "group": {
        "id": "FR-ARA",
        "data_translation" : ["Auvergne-Rhône-Alpes"],
        "flag_url": "https://example...",
        "group": null,
        "capital": null,
        "numeric_code": "FR-ARA"
    },
    "capital":{
        "id": "FR-BOURG-EN-BRESSE",
        "data_translation" : ["Bourg-en-Bresse"],
        "flag_url": "https://example...",
        "group": null,
        "capital": null,
        "numeric_code": "01012"
    },
    "numeric_code": "01"
}
```

## Associated SQL Request

```sql
SELECT d.*, l.id as id_language,
(SELECT GROUP_CONCAT(t.translation) FROM translations t WHERE t.language = l.id AND t.id_item = d.id)  as translation,
(SELECT GROUP_CONCAT(t.translation) FROM translations t WHERE t.language = l.id AND t.id_item = d.data_group)  as dg_translation,
(SELECT GROUP_CONCAT(t.translation) FROM translations t WHERE t.language = l.id AND t.id_item = d.data_capital)  as dc_translation
FROM data d, languages l -- use of language table here to avoid repetition above
WHERE d.id = 'FR-44'
and l.id = 'fr-FR'
```