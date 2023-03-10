# Routes

## Api endpoints


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

