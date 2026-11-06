# Tableau de tests des accès

## Organisation

- Organisation : `Agence`
- Collection `Direction` : accès réservés à la direction.
- Collection `Négociateurs` : accès partagés avec les négociateurs.

## Tests de visibilité et de permissions

| Test | Résultat attendu | Résultat obtenu | État |
|---|---|---|---|
| Création de l'organisation `Agence` | Organisation disponible | Organisation créée | Réalisé |
| Création de `Direction` | Collection disponible | Collection créée | Réalisé |
| Création de `Négociateurs` | Collection disponible | Collection créée | Réalisé |
| Accès du négociateur à `Négociateurs` | Accès autorisé | Accès attribué et vérifié | Réalisé |
| Accès du négociateur à `Direction` | Pas d'accès sans attribution | Accès non attribué | Conforme |
| Modification des éléments | Le membre peut modifier les éléments autorisés | Permission « Modifier les éléments » testée | Réalisé |
| Révocation du membre | Le membre ne doit plus accéder à l'organisation | Retrait de l'accès testé | Réalisé |

### Niveau de permission du négociateur

Le niveau sélectionné pour le membre est **Modifier les éléments**. Il autorise la consultation, la création et la modification des éléments de la collection, y compris leurs mots de passe. Il ne donne pas la gestion de la collection.

Les différents niveaux de permission proposés dans l'interface ont été examinés avant de sélectionner celui correspondant au besoin.

## Identifiants fictifs

Dix identifiants fictifs ont été créés et répartis entre les deux collections.

| Collection | Nombre d'éléments | État |
|---|---:|---|
| Direction | 5 | Créés |
| Négociateurs | 5 | Créés |
| **Total** | **10** | **Réalisé** |

Six mots de passe ont ensuite été renouvelés à l'aide du générateur intégré au coffre.

Aucun identifiant ni mot de passe de démonstration n'est publié dans ce dépôt.

## Résultat global

Les tests de création des collections, d'attribution des permissions, d'accès du membre et de révocation ont été réalisés. Les dix éléments fictifs sont présents dans les collections prévues et six mots de passe ont été renouvelés.
