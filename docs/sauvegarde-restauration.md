# Sauvegarde et restauration de Vaultwarden

## Emplacement des données

Dans cette maquette, les données Vaultwarden sont conservées dans le dossier local `vw-data/`, monté dans le conteneur sur `/data`.

Les archives de sauvegarde contiennent la base du coffre et des données chiffrées. Elles peuvent donc rester sensibles et ne doivent jamais être déposées dans Git ni envoyées dans un espace public.

## Procédure de sauvegarde (PowerShell)

Depuis le dossier du projet :

```powershell
docker compose stop vaultwarden
New-Item -ItemType Directory -Force -Path .\backup
$stamp = Get-Date -Format "yyyyMMdd-HHmmss"
Compress-Archive -Path .\vw-data\* -DestinationPath ".\backup\vw-data-$stamp.zip"
docker compose start vaultwarden
```

L'arrêt de Vaultwarden avant la copie évite de sauvegarder une base SQLite pendant qu'elle est en cours d'écriture.

Après l'opération, vérifier que l'archive existe et possède une taille non nulle :

```powershell
Get-ChildItem .\backup
```

Conserver une copie de l'archive dans un emplacement distinct du dossier de travail. Ne pas la versionner.

## Procédure de restauration

> La restauration remplace les données présentes. Vérifier le nom et l'intégrité de l'archive avant toute opération.

1. Arrêter Vaultwarden.
2. Renommer le dossier actuel `vw-data` afin de le conserver en sauvegarde de sécurité.
3. Recréer un dossier `vw-data` vide.
4. Extraire l'archive choisie dans ce dossier.
5. Redémarrer Vaultwarden.
6. Se connecter avec un compte de test et contrôler la présence des utilisateurs, collections et éléments attendus.

Exemple PowerShell, en adaptant le nom de l'archive :

```powershell
docker compose stop vaultwarden
Rename-Item .\vw-data ".\vw-data-avant-restauration"
New-Item -ItemType Directory -Path .\vw-data
Expand-Archive -Path .\backup\vw-data-AAAA-MM-JJ-HHMMSS.zip -DestinationPath .\vw-data
docker compose start vaultwarden
docker compose logs --tail=30 vaultwarden
```

Si le service ne redémarre pas ou si les données attendues sont absentes, arrêter de nouveau Vaultwarden et remettre en place le dossier `vw-data-avant-restauration`.

## État du test

**Test de restauration : à effectuer.** La procédure est documentée, mais le test réel de restauration n'a pas encore été confirmé. Après le test, noter la date, l'archive utilisée, les comptes/collections retrouvés et le résultat.

| Contrôle | Résultat |
|---|---|
| Archive créée | À compléter |
| Taille de l'archive vérifiée | À compléter |
| Restauration effectuée | À effectuer |
| Comptes retrouvés après restauration | À compléter |
| Collections et éléments contrôlés | À compléter |

Ne jamais exécuter `docker compose down -v` pour une simple opération d'arrêt : cette commande supprimerait les volumes Docker nommés.
