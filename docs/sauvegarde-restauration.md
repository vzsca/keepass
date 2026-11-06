# Sauvegarde et restauration de Vaultwarden

## Emplacement des données

Dans cette maquette, les données Vaultwarden sont conservées dans le dossier local `vw-data/`, monté dans le conteneur sur `/data`.

Les archives de sauvegarde contiennent la base du coffre et des données chiffrées. Elles restent sensibles et ne doivent jamais être déposées dans Git ni envoyées dans un espace public.

## Sauvegarde réalisée

Depuis le dossier du projet, la sauvegarde a été réalisée après l'arrêt de Vaultwarden :

```cmd
mkdir backups
docker compose stop vaultwarden
robocopy vw-data backups\vw-data /E
docker compose start vaultwarden
```

L'arrêt du service avant la copie évite de copier la base SQLite pendant qu'elle est en cours d'écriture. La sauvegarde est conservée localement dans `backups\vw-data`.

## Test de restauration réalisé

Pour ne pas écraser les données du coffre principal, une copie de travail distincte a été utilisée :

```cmd
mkdir restauration-test
robocopy backups\vw-data restauration-test /E
```

Cette copie a ensuite été ouverte dans une instance Vaultwarden temporaire, séparée de l'instance principale. Un accès HTTPS temporaire via Caddy a été mis en place, car l'interface client Vaultwarden refuse une connexion HTTP non sécurisée.

Le test a été déclaré concluant après vérification de l'accès aux données restaurées. Le coffre principal n'a pas été remplacé par la copie de test.

## Résultat

| Contrôle | Résultat |
|---|---|
| Arrêt du service avant copie | Réalisé |
| Copie des données dans `backups\vw-data` | Réalisée |
| Création d'une copie indépendante `restauration-test` | Réalisée |
| Démarrage d'une instance temporaire de restauration | Réalisé |
| Accès HTTPS à l'instance temporaire | Réalisé |
| Vérification des données restaurées | Validée |

## Précautions

- Conserver les sauvegardes hors du dépôt Git.
- Ne pas partager les dossiers `vw-data`, `backups` ou `restauration-test`.
- Ne jamais effectuer un test de restauration directement sur le coffre principal.
- Conserver une copie de sécurité avant toute restauration réelle.
- Ne pas exécuter `docker compose down -v` pour un simple arrêt : cette commande supprimerait les volumes Docker nommés.
