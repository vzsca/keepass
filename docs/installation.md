# Procédure d'installation

## 1. Pré-requis

- Windows 11 et droits administrateur pour modifier le fichier hosts et importer le certificat.
- Docker Desktop démarré avec le moteur WSL 2.
- Docker Compose disponible dans PowerShell.
- Un dossier de projet contenant `compose.yaml` et `Caddyfile`.

Vérification :

```powershell
docker --version
docker compose version
docker info
```

## 2. Préparer les fichiers

Copier `.env.example` vers `.env`, puis générer un condensat Argon2id pour le jeton administrateur :

```powershell
docker run --rm -it vaultwarden/server:latest /vaultwarden hash
```

Reporter le condensat dans `.env`, sans le publier. Le fichier réel `.env` est ignoré par Git.

Le fichier Compose utilise `ADMIN_TOKEN` comme variable d'environnement. Le service Vaultwarden conserve ses données dans `./vw-data`.

## 3. Configurer le nom local

Ouvrir le Bloc-notes en administrateur et modifier :

`C:\Windows\System32\drivers\etc\hosts`

Ajouter :

```text
127.0.0.1 vault.lan
```

Contrôler la résolution :

```powershell
ping vault.lan
```

L'adresse doit résoudre vers `127.0.0.1`.

## 4. Démarrer les services

Depuis le dossier du projet :

```powershell
docker compose pull
docker compose up -d
docker compose ps
```

Les conteneurs `vaultwarden` et `caddy` doivent être actifs. Ouvrir ensuite :

`https://vault.lan`

## 5. Faire confiance au certificat Caddy

Caddy utilise `tls internal` et génère une autorité de certification locale. Exporter le certificat racine depuis le conteneur :

```powershell
docker compose cp caddy:/data/caddy/pki/authorities/local/root.crt .\root.crt
```

Sous Windows, importer ce certificat dans les autorités racines de confiance avec les droits administrateur :

```powershell
certutil -addstore -f Root C:\Projets\coffre-agence\root.crt
```

Firefox peut utiliser son propre magasin de certificats : dans ce cas, importer le certificat dans les autorités depuis les paramètres de Firefox. Fermer puis rouvrir le navigateur et vérifier l'absence d'avertissement sur `https://vault.lan`.

Le certificat racine public `root.crt` peut être conservé localement pour le laboratoire, mais ne doit pas être remplacé par une clé privée ni accompagné de secrets dans Git.

## 6. Contrôles de sécurité

- `SIGNUPS_ALLOWED` doit rester à `false` après la création contrôlée des comptes.
- Le port HTTPS est lié à `127.0.0.1:443` : le service n'est pas publié sur les interfaces réseau de la machine.
- Le port 80 de Vaultwarden est uniquement exposé dans le réseau Docker interne.
- Le jeton administrateur et le fichier `.env` ne sont jamais déposés dans le dépôt.

Commandes de diagnostic :

```powershell
docker compose ps
docker compose logs --tail=50 vaultwarden
docker compose logs --tail=50 caddy
```

## 7. Particularités de cette maquette

Le déploiement utilise un dossier local `vw-data/` pour les données Vaultwarden et deux volumes Docker nommés pour les données et la configuration Caddy. Le port HTTPS est volontairement limité à la boucle locale, ce qui est plus restrictif que l'exposition à tout le réseau local.

Vaultwarden est une implémentation communautaire. Cette configuration est destinée à une démonstration pédagogique sur un poste local.
