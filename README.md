
Documentation de l'API du projet de AREA
======

Le langage utilisé pour la creation de cette _api_ est _Python3_.
Nous avons utilisé le framework open-source python _Flask_.

L'API comporte 10 requêtes : 6 POST, 3 GET et 1 DELETE

Vous pouvez accéder à toutes ces requêtes dans Postman en important la collection associée à ce lien :
https://www.getpostman.com/collections/6e9b4d5e32d2c0c00fbe

Attention, les requêtes de cette collection sont prévues pour fonctionner en local sur le port 5000.
Pour lancer le serveur en mode dévelopemment et sur le port 5000, exécutez le fichier _run_dev.sh_ du dossier _serverapi_.


Tous les retours sont un json :

`
[{
    "code": "200",
    "data": [
        "msg": "Succes"
    ]
}]
`

Créer un nouveaux compte
------------

POST	:	http://127.0.0.1:5000/api/users

http://127.0.0.1:5000       		URL
/api/users				route

Dans le body : 
`{"username":"Florian",
"password":"zefqldkqk",
"email":"florian.bord@epitech.eu"}`

Trois retours possibles:
- 404 en cas d'erreur, avec un message spécifique 
- 200 pour ok


Vérifier que le compte existe dans la base de données
----------

POST	:	http://127.0.0.1:5000/api/login

http://127.0.0.1:5000/					URL
api/login/						route

Dans le body : 
`{"username":"florianles@oui.crom", "password":"zefqldkqk"}`

Le token est retourné dans _data_ avec la clé _token_.

Deux retours possibles:
- 200 pour ok.
- 401 si l'utilisateur n'existe pas.
- 404 en cas d'erreur.


Ajouter un service
----------

POST	:	http://127.0.0.1:5000/service

http://127.0.0.1:5000/				URL
service/					route

Dans le header : 'Authorization : token'
exemple : 'Authorization : EQ4b60fb_AuewuYCpK6SPA'

Dans le body : `{"action":"Nom de l'action",
				"action_data":"argument de l'action",
				"reaction":"Nom de la reaction",
				"reaction_data":"argument de la reaction",
				"name":"Nom donné au service"}`

Deux retours possibles:
- 200 		si tout s'est bien passé
- 401		si la connexion a echoué (mauvais username password)
- 404 		en cas d'erreur

Retirer un service
---------

DELETE	:	http://127.0.0.1:5000/service

http://127.0.0.1:5000/				URL
service/					route

Dans le header : 'Authorization : token'
exemple : 'Authorization : EQ4b60fb_AuewuYCpK6SPA'

Dans le body : `{"name": "Service1"}`

Trois retours possibles:
- 200		pour ok
- 404		si le service n'existe pas
- 401		si la connexion a echoué (mauvais username password)


Obtenir la liste des services d'un utilisateur et l'état de chacun (activé / desactivé)
-------------

GET	:	http://127.0.0.1:5000/service_list

http://127.0.0.1:5000/			URL
service_list/				route

Dans le header : 'Authorization : $token'
exemple : 'Authorization : EQ4b60fb_AuewuYCpK6SPA'

Les service sont retournés dans data sous la forme : `[{"name":"SERVICE1","state":"true"}]`

exemple pour 4 service nommés 'serv1', 'serv2', 'serv3', 'serv4' :
	`[{"name":"serv1","state":true},{"name":"serv2","state":true},{"name":"serv3","state":true},{"name":"serv4","state":true}]`

Trois retours possibles:
- 200		pour ok
- 404		(pas de service pour cet utilisateur)
- 401		problème de connexion


Changer l'état d'un service, s'il est true il passe a false et vice-versa
----------------

POST	:	http://127.0.0.1:5000/change_state/

http://127.0.0.1:5000/			URL
change_state/				route

Dans le header : 'Authorization : $token'
exemple : 'Authorization : EQ4b60fb_AuewuYCpK6SPA'

Dans le body : {"name":"Nom du service"}

Trois retours possibles:
- 200		pour ok
- 404	si le service n'existe pas
- 401	si le token est mauvais

Récupérer la liste des reactions disponibles
-------------

GET	:	http://127.0.0.1:5000/reaction_list

http://127.0.0.1:5000/			URL
reaction_list/				route

Retourne la liste des actions avec leurs descriptions.
Exemple:
`{"code":"200","data":{"send_mail":{"desc":"L\u2019utilisateur re\u00e7oit un mail avec le contenu qu\u2019il passe en param\u00e8tre"}}}`


Récupérer la liste des actions disponibles
-------------

GET	:	http://127.0.0.1:5000/action_list

http://127.0.0.1:5000/			URL
action_list/				route

Retourne la liste des actions avec leurs descriptions.
Exemple:
`{"code":"200","data":"fb_birthday":{"desc":"Regarde si la date d\u2019anniversaire Facebook est celle d\u2019aujourd\u2019hui."}}}`

Ajouter un token special
-------------------

POST	:	http://127.0.0.1:5000/add_token

http://127.0.0.1:5000/			URL
add_token				route

Dans le header : 'Authorization : $token'
exemple : 'Authorization : EQ4b60fb_AuewuYCpK6SPA'

Dans le body : `{"token":"qdqdzjdjqkfkq", "name":"facebook"}`

Trois retours possibles:
- 200		pour ok
- 404		en cas d'erreur
- 401		si la connexion échoue

Récupérer un token special
----------

POST	:	http://127.0.0.1:5000/get_token

http://127.0.0.1:5000/			URL
get_token				route


Dans le header : 'Authorization : $token'
exemple : 'Authorization : EQ4b60fb_AuewuYCpK6SPA'

Dans le body : `{"name":"facebook"}`

Retours possibles:
- 200		pour ok
- 404		en cas d'erreur
- 401		si la connexion échoue
`
