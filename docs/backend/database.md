# Database

## Schema

![Wanderway's database schema](../assets/database_schema.png)

### Table generation script

```sql
CREATE TABLE map (
    id varchar(50),
    id_description varchar(50),
    url_wiki  varchar(250)
);
CREATE TABLE tag_group (
    id varchar(50)
);

CREATE TABLE tag (
    id varchar(50),
    id_group varchar(50),
    FOREIGN KEY(id_group) REFERENCES tag_group(id)
);

CREATE TABLE tag_map (
    id_map varchar(50),
    id_tag varchar(50),
    FOREIGN KEY(id_tag) REFERENCES tag(id),
    FOREIGN KEY(id_map) REFERENCES map(id)
);

CREATE TABLE languages (
    id varchar(50)
);

CREATE TABLE map_statistics (
    id_map varchar(50),
    id_lang varchar(50),
    play_count number,
    FOREIGN KEY(id_map) REFERENCES map(id),
    FOREIGN KEY(id_lang) REFERENCES languages(id)
);

CREATE TABLE translations (
    id number,
    id_lang varchar(50),
    translation text,
    id_item varchar(50),
    FOREIGN KEY(id_lang) REFERENCES languages(id)
);
```

### Dataset generation script

```sql
INSERT INTO languages (id)
VALUES ('fr-FR');

INSERT INTO tag_group (id)
VALUES  ('TAG_GROUP_CONTINENT'),
        ('TAG_GROUP_COUNTRY'),
        ('TAG_GROUP_ECONOMIC_UNION');

INSERT INTO tag (id,id_group)
VALUES  ('TAG_FRANCE','TAG_GROUP_COUNTRY'),
        ('TAG_JAPAN','TAG_GROUP_COUNTRY'),
        ('TAG_EUROPE','TAG_GROUP_CONTINENT'),
        ('TAG_ASIA','TAG_GROUP_CONTINENT');

INSERT INTO map (id, id_description, url_wiki)
VALUES  ('FRANCE_DEPARTMENT', "DESCRIPTION_FRANCE_DEPARTMENT", ""),
        ('JAPAN_PREFECTURES', "DESCRIPTION_JAPAN", "");

INSERT INTO map_statistics (id_map, id_lang, play_count)
VALUES ('FRANCE_DEPARTMENT', "fr-FR", 700);

INSERT INTO translations (id, id_lang, translation, id_item)
VALUES  (1,'fr-FR', "France", "TAG_FRANCE"),
        (2,'fr-FR', "Japon", "TAG_JAPAN"),
        (3,'fr-FR', "Europe", "TAG_EUROPE"),
        (4,'fr-FR', "Asie", "TAG_ASIA"),
        (5,'fr-FR', "Continent", "TAG_GROUP_CONTINENT"),
        (6,'fr-FR', "Pays", "TAG_GROUP_COUNTRY"),
        (7,'fr-FR', "france - Départements", "FRANCE_DEPARTMENT"),
        (8,'fr-FR', "Japon - Préfectures", "JAPAN_PREFECTURES"),
        (9,'fr-FR', "Départements de france", "DESCRIPTION_FRANCE_DEPARTMENT"),
        (6,'fr-FR', "Préfectures du japon", "DESCRIPTION_JAPAN");


INSERT INTO tag_map (id_map, id_tag)
VALUES  ("FRANCE_DEPARTMENT","TAG_FRANCE"),
        ("FRANCE_DEPARTMENT","TAG_EUROPE");
```