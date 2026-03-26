# TP 1 

Pour lancer le projet il faut d'abord se placer dans le dossier `api/` et crée un fichier `.env` a partir du fichier `.env-template`, ensuite il faut lancer la commande `docker compose up --build` pour construire les images et lancer les conteneurs.

## Questions du TP
### Étape 2 — Dockeriser l’API
#### Questions de réflexion
> Pourquoi séparer l’installation des dépendances et la copie du code ?
```
Séparer l'installation des dépendances et la copie du code nous permet d'utiliser le cache de docker. 
En installant les dépendances avant de copier le code, docker peut réutiliser les couches d'installation des dépendances pour accélère la construction de l'image.
```

### Étape 4 — Configuration via variables d’environnement
### Question de réflexion
> Pourquoi l’image Docker doit rester la même entre dev et prod ?
```
L'image docker doit rester la même entre dev et prod pour garantir que l'application fonctionne de manière cohérente dans les deux environnements. En utilisant la même image, on s'assure que les dépendances, les configurations et les comportements de l'application sont identiques, ce qui réduit les risques de bugs ou de problèmes liés à des différences d'environnement.
```

> Pourquoi l’API se connecte à `db` et pas à `localhost` ?
```
L'API se connecte à db et pas à localhost car dans l'environnement docker, chaque service est isolé dans son propre conteneur. Le localhost ferait référence au conteneur de l'API lui-même, tandis que db fait référence au conteneur de la base de données, c'est ensuite docker qui gere la resolution DNS pour faire communiquer les deux conteneurs (avec le network défini dans le docker compose).
```


### Étape 5 — Ajouter une base de données PostgreSQL
#### Question de réflexion
> Pourquoi la table `notes` n'existe plus au re-lunch (après un `docker compose down`) ?
```
La table notes n'existe plus au re-lunch après un docker compose down car les données sont stockées dans le conteneur de la base de données, qui est supprimé lorsque le conteneur est arrêté. Sans un volume configurer dans le docker compose il y a pas une persistance de données.
```

### Étape 6 — Persister les données avec un volume
#### Question de réflexion
> Pourquoi ne met-on pas les données directement dans le container ?
```
Parce que les conteneurs a chaque fois qu'ils sont supprimés, ils perdent toutes les données qui y sont stockées. Ce qui est problèmatique par exemple si on veut avoir plusieurs instances de l'app avec une seule base de données.
```
> Quel composant est stateful ? Lequel est stateless ?
```
Le composant stateful est la base de données parce qu'elle stocke les données de manière persistante et l'api est stateless car elle ne stocke pas de données de manière persistante, elle traite les requêtes et retourne des réponses sans conserver d'état entre les requêtes.
```

### Étape 7 - Utiliser un fichier `.env`
#### Question de réflexion
> Pourquoi les secrets ne doivent-ils pas être dans le code ni dans le dépôt Git ?
```
Par securité, les secrets contienent des données sensibles comme des mots de passe ou des clés d'API, les stocker dans le code ou dans le dépôt Git expose ces informations à des risques de fuite, surtout si le code est partagé.
```

