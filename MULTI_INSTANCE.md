Déployer plusieurs instances de wordsmith avec Docker Compose

Approche : utiliser un petit fichier d'environnement par instance contenant au minimum :

- `COMPOSE_PROJECT_NAME` : nom du projet Compose (isolera réseaux/containers)
- `WEB_PORT` : port hôte pour exposer le service web

Exemples fournis dans `instances/instance1.env` et `instances/instance2.env`.

Commandes :

Démarrer la première instance :

```bash
docker compose --env-file instances/instance1.env up -d
```

Démarrer la seconde instance (même machine) :

```bash
docker compose --env-file instances/instance2.env up -d
```

Arrêter et supprimer :

```bash
docker compose --env-file instances/instance1.env down
```

Notes :

- Le fichier `docker-compose.yaml` a été modifié pour utiliser la variable `WEB_PORT` (valeur par défaut 8080).
- Si vous préférez, vous pouvez définir ces variables dans `.env` avant d'exécuter `docker compose up` sans passer `--env-file`.
- Chaque instance crée son propre réseau et ses containers grâce à `COMPOSE_PROJECT_NAME`.
