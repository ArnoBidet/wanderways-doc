# Routes

## Api endpoints

<!-- @TODO create better design for this and translate-->

- Map
    - [Get the list of maps](./routes/map/list.md)
    - [Get datas from a map](./routes/map/ID-MAP_data.md)
- Game
    - [Get the list of games @TODO]()
- Tag
    - [Get the list of tags](./routes/tag/list.md)
- Against the clock
    - [Save an entry in a game](./routes/against-the-clock/save-entry.md)
    - [Giving up in a game](./routes/against-the-clock/give-up.md)
- Statistics
    - [Average awareness](./routes/statistics/average-awareness.md)


<!-- - /game/list (, permet d’obtenir des données comme la popularité ou le taux de réussite par jeux)
- /against-the-clock
  - /start (POST, retourne ID de la session, avec potentiellement d’autres infos)
  - /end (POST, sert à demander au serveur si la partie est bien fini)
  - /abort-session (POST, sert à indiquer au serveur que le client a quitté/rafraichis l’onglet innopinément et que les résultat doivent être supprimés NÉCESSITE VERIFICATION TECHNIQUE) -->

Notes :

- The language is always passed through the HTTP header "prefered-language" and corresponds to the following schema  :<br>`fr-FR|en-US|es-ES|pt-PT|de-DE`.
- For a game creation, the sessions' cookie is instanciated throuh `SET-COOKIE` HTTP header.
- The next api-call will have the cookie.
- Session cookies will have the following propertiers by default :<br>`Secure`, `SameSite : strict` and `HttpOnly`.

