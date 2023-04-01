# Map's data

!!swagger mapdata.yaml!!

Uses the header `Accepted-Language` to determine data translation.

## Typescript schema

```ts
interface MapData{
    id: string,
    label : string[],
    group: {
        id: string,
        label : string[]
    } | null,
    capital:{
        id: string,
        label : string[]
    } | null,
    numeric_code: string
}
```

### Example
```json
[
  {
    "id": "FR-01",
    "label": [
      "Ain"
    ],
    "group": {
      "id": "FR-ARA",
      "label": [
        "Auvergne-Rhône-Alpes"
      ]
    },
    "capital": {
      "id": "FR-BOURG-EN-BRESSE",
      "label": [
        "Bourg-en-Bresse"
      ]
    },
    "numeric_code": "01"
  },
  {
    "id": "FR-02",
    "label": [
    "Aisne"
    ],
    "group": {
      "id": "FR-HDF",
      "label": [
        "Hauts-de-France"
      ]
    },
    "capital": {
      "id": "FR-LAON",
      "label": [
        "Laon"
      ]
    },
    "numeric_code": "02"
  },
]
```

## Associated SQL Request

```sql
CREATE MATERIALIZED VIEW mv_geo_data AS
SELECT gd.id,
    l.id as id_lang,
    gd.geo_data_capital,
    gd.geo_data_group,
    gd.numeric_code,
    l.id as id_language,
    get_translations(l.id, gd.id) as geo_data_label,
    get_translations(l.id, gd.geo_data_capital) as geo_data_capital_label,
    get_translations(l.id, gd.geo_data_group) as geo_data_group_label
FROM geo_data gd,
    lang l

CREATE OR REPLACE FUNCTION f_map_geo_data (
	param_id_lang CHAR(5),
    param_id_map VARCHAR(50)
) 
RETURNS TABLE (
	id VARCHAR(50),
	data_label TEXT,
	id_group VARCHAR(50),
    group_label TEXT,
	id_capital VARCHAR(50),
    capital_label TEXT,
	numeric_code VARCHAR(50)
) 
language plpgsql
as $$
declare 
    var_r record;
begin
	for var_r in(
            SELECT mv_gd.id,
                mv_gd.geo_data_label,
                mv_gd.geo_data_group,
                mv_gd.geo_data_group_label,
                mv_gd.geo_data_capital,
                mv_gd.geo_data_capital_label,
                mv_gd.numeric_code
            FROM map_geo_data mgd, mv_geo_data mv_gd
            WHERE mv_gd.id_lang = param_id_lang
            AND mgd.id_map = param_id_map
            AND mv_gd.id = mgd.id_geo_data
        ) loop
        id := var_r.id;
        data_label := var_r.geo_data_label;
        id_group := var_r.geo_data_group;
        group_label := var_r.geo_data_group_label;
        id_capital := var_r.geo_data_capital;
        capital_label := var_r.geo_data_capital_label;
        numeric_code := var_r.numeric_code;
        return next;
	end loop;
end; $$

SELECT * FROM f_map_geo_data('fr-FR', 'FRANCE_DEPARTMENTS');
```