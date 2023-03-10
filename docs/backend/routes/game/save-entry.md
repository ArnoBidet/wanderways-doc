# Save entry

<style>.scheme-container{display:none;}</style>

!!swagger save-entry.yaml!!


@TODO uml sequence diagramm


## Typescript schema

```ts
interface SaveEntryStatus{
   reponsecode : GameResponse
}

enum GameResponse {
    OK=1,
    ALREADY_FOUND=2,
    WRONG_GUESS=3,
    UNKNOWN_ERROR=4
}
```

### Example
```json
{
   "reponsecode" : 1
}
```

## Associated SQL Request

*none*

<!-- @TODO create sequence diagram or sth
Séquence de traitements backend particuliers :

- Une requête arrive, elle a une id de session
- La session est récupéré
- La réponse (au sens de réponse au jeu) est comparé avec ce qu’il est possible de trouver sur le jeu/carte et ce qui a déjà été trouvé. 3 cas
- la réponse est bien une nouvelle réponse :  200 OK
- la réponse a déjà été trouvé :  400 BAD REQUEST
- la réponse est fausse :  400 BAD REQUEST
- [voir comment gérer le timestamp et la triche]
- La réponse approprié est renvoyé au client -->

<!-- 
Comments :
Une énum GameResponse est à réfléchir pour déterminer les réponses possible d’erreur prévues. Cette énum pourrait prendre les valeurs suivantes : OK, ALREADY_FOUND, WRONG_GUESS, UNKNOWN_ERROR
 -->