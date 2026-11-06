# Politique de mots de passe de l'agence

## Objectif

Protéger les comptes de l'agence, ses portails professionnels et les données auxquelles ils donnent accès. Les règles sont adaptées à la sensibilité de chaque service et aux risques associés.

**Référence :** ANSSI, *Recommandations relatives à l'authentification multifacteur et aux mots de passe* (ANSSI-PG-078, 8 octobre 2021), recommandation de mener une analyse de risque.

## Longueur minimale

Les mots de passe doivent être suffisamment longs, robustes et difficiles à deviner. Leur robustesse est adaptée au contexte du compte ; les mots de passe des accès sensibles doivent bénéficier d'un niveau de protection renforcé. Les mots de passe faibles ou prévisibles sont refusés.

**Référence :** ANSSI-PG-078, recommandation d'adapter la robustesse du mot de passe au contexte d'utilisation.

## Un mot de passe par service

Chaque service possède un mot de passe distinct. La réutilisation est interdite afin qu'une fuite sur un site ne permette pas de compromettre les autres comptes.

**Référence :** ANSSI-PG-078, recommandations relatives à la robustesse des secrets et à la limitation des conséquences d'une compromission.

## Usage obligatoire du coffre

Les identifiants professionnels sont enregistrés dans le coffre de l'organisation, dans la collection correspondant à leur usage. Les mots de passe sont générés par le coffre et ne sont pas conservés dans un cahier, un fichier non protégé ou un message.

**Référence :** ANSSI-PG-078, recommandation d'utiliser un coffre-fort de mots de passe.

## Double authentification

L'authentification multifacteur est activée lorsqu'elle est proposée par le service, en priorité pour les comptes d'administration et les accès sensibles. Un facteur de possession, tel qu'une application d'authentification, est privilégié lorsque le service le permet.

**Référence :** ANSSI-PG-078, recommandations de privilégier l'authentification multifacteur et un facteur de possession.

## Départ d'un salarié

À la fin du contrat ou lors d'un changement de fonction, les droits du salarié sont retirés de l'organisation. Les mots de passe des comptes partagés qu'il pouvait connaître sont renouvelés, puis mis à jour dans le coffre.

**Référence :** ANSSI-PG-078, analyse de risque et gestion des moyens d'authentification ; mesure ANSSI #0084, renouveler les secrets des comptes partagés lors du retrait d'un utilisateur.

## Fuite constatée

En cas de fuite ou de suspicion de compromission, le mot de passe concerné est changé sans attendre. Si le même secret a été réutilisé, il est remplacé sur tous les services concernés. Les accès et activités inhabituels sont vérifiés.

**Référence :** ANSSI-PG-078, adaptation des moyens d'authentification au risque ; mesure ANSSI #0084 pour les comptes partagés.

## Documents de référence

- ANSSI, *Recommandations relatives à l'authentification multifacteur et aux mots de passe*, ANSSI-PG-078, 08/10/2021 : https://cyber.gouv.fr/publications/recommandations-relatives-lauthentification-multifacteur-et-aux-mots-de-passe
- ANSSI / MesServicesCyber, mesure #0084 : renouvellement des secrets des comptes partagés lors du retrait d'un utilisateur : https://monservicesecurise.cyber.gouv.fr/referentiel-mesures

Cette politique est une règle interne proposée pour l'agence ; elle adapte les recommandations aux usages du projet.
