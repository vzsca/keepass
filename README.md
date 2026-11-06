# Coffre de mots de passe — Agence immobilière

Projet BTS SIO — Sujet 04, épreuve E5.

Déploiement local d'un coffre de mots de passe destiné à une agence immobilière fictive, avec Vaultwarden, Docker Compose et Caddy.

## Objectifs

- Rendre le coffre accessible en HTTPS sur le poste de démonstration.
- Organiser les accès dans une organisation et des collections.
- Limiter les droits des membres selon leur fonction.
- Tester la révocation des accès lors du départ d'un salarié.
- Formaliser les règles de gestion des mots de passe.
- Vérifier cinq adresses avec Have I Been Pwned (HIBP).
- Créer des identifiants fictifs et renouveler des mots de passe.
- Tester la sauvegarde et la restauration des données.

## Architecture réalisée

- **Vaultwarden** : serveur compatible avec les clients Bitwarden.
- **Caddy** : proxy inverse et autorité de certification interne.
- **Docker Compose** : lancement des services.
- **Adresse locale** : https://vault.lan
- **Stockage Vaultwarden** : dossier local `vw-data/`, monté dans `/data`.
- **Exposition réseau** : port HTTPS lié à `127.0.0.1:443`, donc accessible uniquement depuis le PC hôte.

> Vaultwarden est une implémentation communautaire compatible avec le protocole Bitwarden, et non le serveur officiel Bitwarden. Cette maquette est un environnement pédagogique local, pas une recommandation de déploiement en production.

## Arborescence

```text
.
├── compose.yaml
├── Caddyfile
├── .env.example
├── .gitignore
└── docs/
    ├── installation.md
    ├── sauvegarde-restauration.md
    ├── tableau-tests.md
    ├── procedure-depart.md
    ├── politique-mdp.md
    ├── hibp.md
    └── preuves.md
```

## Démarrage

1. Installer et lancer Docker Desktop avec le moteur WSL 2.
2. Copier `.env.example` vers `.env`.
3. Générer un condensat Argon2id pour le jeton administrateur et le placer dans `.env`. Ne jamais publier le fichier réel.
4. Ajouter `127.0.0.1 vault.lan` au fichier hosts de Windows.
5. Placer `compose.yaml` et `Caddyfile` dans le même dossier.
6. Exécuter :

```powershell
docker compose pull
docker compose up -d
docker compose ps
```

La procédure complète, notamment l'installation du certificat Caddy, est dans [docs/installation.md](docs/installation.md).

## Bilan des validations

| Élément | État |
|---|---|
| Services Docker démarrés | Réalisé |
| Accès à Vaultwarden en HTTPS | Réalisé |
| Organisation `Agence` et collections | Réalisé |
| Compte négociateur et droits de collection | Testés |
| Révocation du membre | Testée |
| Cinq recherches d'adresses HIBP | Réalisées, aucune fuite connue signalée |
| Dix identifiants fictifs | Créés, cinq par collection |
| Renouvellement de six mots de passe | Réalisé |
| Sauvegarde des données | Réalisée |
| Restauration sur une instance de test isolée | Testée et validée |

Les résultats et procédures sont détaillés dans le dossier `docs/`. Les recherches HIBP concernaient les adresses e-mail : elles ne constituent pas un contrôle exhaustif des mots de passe.

## Sécurité et fichiers à ne pas publier

Le dépôt ne doit contenir aucun secret ni donnée réelle. Le fichier `.env`, le contenu de `vw-data/`, les archives de sauvegarde, les dossiers de restauration, les certificats privés et les captures contenant des identifiants ou des mots de passe sont exclus par `.gitignore`.

Les identifiants de démonstration sont fictifs. Les mots de passe ne doivent jamais être ajoutés à Git.
