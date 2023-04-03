# Average awareness


!!swagger statistics.yaml!!


## Typescript schema

```ts
interface AverageAwareness {
  play_count : number,
  data : {
    id : string,
    found_count : string
  }[]
}
```

### Example

```json
{
  "play_count" : 700,
  "data":[{
    "id":"FR-01",
    "found_count":40
  },{
    "id":"FR-02",
    "found_count":20
  },{
    "id":"FR-03",
    "found_count":150
  }]
}
```

## Associated SQL Request

### Function

```sql
CREATE OR REPLACE FUNCTION f_average_awareness (
    param_id_map VARCHAR(50),
    param_id_gamemod VARCHAR(50),
	param_id_lang CHAR(5) DEFAULT NULL
) 
RETURNS TABLE (
	id VARCHAR(50),
	found_count INT
) 
language plpgsql
as $$
begin
	RETURN QUERY
        SELECT mgd.id_geo_data as id,
            SUM(COALESCE(gds.found_count::int, 0))::int as found_count
        FROM map_geo_data mgd 
        LEFT JOIN lang l
        ON l.id like '%'||COALESCE(param_id_lang, '')||'%' -- if provided then filters, else any
        LEFT JOIN map m
        ON m.id = param_id_map
        LEFT JOIN gamemod g
        ON g.id = param_id_gamemod
        LEFT JOIN geo_data_statistic gds
        ON mgd.id = gds.id_geo_data AND m.id = gds.id_map AND g.id = gds.id_gamemod AND l.id = gds.id_lang
        WHERE mgd.id_map = m.id
        GROUP BY mgd.id_geo_data;
end; $$
```

### Test

```sql
INSERT INTO geo_data_statistic (id_gamemod,id_geo_data,id_lang,id_map,found_count)
SELECT 'AGAINST_CLOCK', id, 'fr-FR', id_map, floor(random() * 100 + 1)::int
FROM map_geo_data
WHERE id_map = 'FRANCE_DEPARTMENTS';

INSERT INTO geo_data_statistic (id_gamemod,id_geo_data,id_lang,id_map,found_count)
SELECT 'AGAINST_CLOCK', id, 'en-US', id_map, floor(random() * 50 + 1)::int
FROM map_geo_data
WHERE id_map = 'FRANCE_DEPARTMENTS';

SELECT * FROM f_average_awareness('FRANCE_DEPARTMENTS', 'AGAINST_CLOCK','de-DE');
SELECT * FROM f_average_awareness('FRANCE_DEPARTMENTS', 'AGAINST_CLOCK','pt-PT');
SELECT * FROM f_average_awareness('FRANCE_DEPARTMENTS', 'AGAINST_CLOCK', 'fr-FR');
SELECT * FROM f_average_awareness('FRANCE_DEPARTMENTS', 'AGAINST_CLOCK', 'en-US');
SELECT * FROM f_average_awareness('FRANCE_DEPARTMENTS', 'AGAINST_CLOCK');
SELECT * FROM f_average_awareness('FRANCE_DEPARTMENTS', 'AGAINST_CLOCK', null);

DELETE FROM geo_data_statistic;
```