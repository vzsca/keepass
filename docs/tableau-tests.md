# Tableau de tests des accès

## Organisation

- Organisation : `Agence`
- Collection `Direction` : accès réservés à la direction.
- Collection `Négociateurs` : accès partagés avec les négociateurs.

## Tests de visibilité et de permissions

Les vérifications ci-dessous reprennent les tests réalisés dans l'interface. Les captures correspondantes restent à ajouter dans le dossier de preuves.

| Compte de test | Collection | Visibilité attendue | Observation | État |
|---|---|---|---|---|
| Direction | Direction | Oui | Collection créée et visible depuis le compte direction | Réalisé |
| Direction | Négociateurs | Oui | Collection créée dans l'organisation | Réalisé |
| Négociateur 1 | Direction | Non | Accès non attribué | À documenter par capture |
| Négociateur 1 | Négociateurs | Oui | Accès attribué | Réalisé |

### Niveau de permission du négociateur

Le niveau sélectionné pour le membre est **Modifier les éléments**. Il autorise la consultation, la création et la modification des éléments de la collection, y compris leurs mots de passe. Il ne donne pas la gestion de la collection.

La première attribution était en lecture seule ; elle a été remplacée par le niveau de modification après constat que le membre ne pouvait pas créer d'élément.

## Les dix accès fictifs demandés par le sujet

Le sujet demande quatre éléments dans `Direction` et six dans `Négociateurs`. Ils doivent être créés avec des identifiants et mots de passe entièrement fictifs, générés dans le coffre.

| Collection | Élément fictif à créer | État |
|---|---|---|
| Direction | Portail bancaire | À créer |
| Direction | Compte de l'expert-comptable | À créer |
| Direction | Outil de paie | À créer |
| Direction | Portail des notaires | À créer |
| Négociateurs | Portail d'annonces A | À créer |
| Négociateurs | Portail d'annonces B | À créer |
| Négociateurs | Portail d'annonces C | À créer |
| Négociateurs | CRM | À créer |
| Négociateurs | Planning de visites | À créer |
| Négociateurs | Boîte de contact | À créer |

Pour chaque élément, choisir `Agence` comme propriétaire puis sélectionner la collection appropriée. Un élément créé dans le coffre personnel ne sera pas partagé avec l'organisation.

## Résultat attendu du test de séparation

| Compte | Collection | Visible | Attendu | Résultat |
|---|---|---|---|---|
| Négociateur 1 | Direction | Non | Non | À confirmer avec capture |
| Négociateur 1 | Négociateurs | Oui, 6 éléments après leur création | Oui | À compléter |

Les dix éléments et le contrôle du nombre six ne sont pas déclarés réalisés tant que leur création et leur vérification n'ont pas été faites.
