---
nav_title: Vérification des données de localisation
article_title: Vérification des données de localisation
page_order: 1

page_type: solution
description: "Cet article d’aide décrit des vérifications rapides qui peuvent vous aider si aucun utilisateur n’a des données de localisation."
tool: Location
---

# Vérification des données de localisation

Par défaut, le SDK Braze capture l’emplacement le plus récent d’un utilisateur. Cela signifie généralement que « l’emplacement récent » est l’endroit à partir duquel votre utilisateur a récemment utilisé votre application. Si vous envoyez des données de localisation Braze en arrière-plan, vous aurez peut-être des données plus granulaires.

Si aucun utilisateur n’est disponible, il y a deux vérifications rapides qui peuvent vous aider à confirmer :

* [Collecte de données](#confirm-data-collection)
* [Transfert de données](#confirm-data-transfer)

## Collecte de données

Confirmez que votre application recueille les données de localisation :

- Pour iOS, cela signifie que les utilisateurs choisissent de partager leurs données de localisation via une invite à un moment donné du parcours utilisateur. 
- Pour Android, assurez-vous que votre application demande des autorisations de localisation fine ou grossière lors de l’installation.

Pour voir si les données de localisation de l’utilisateur sont envoyées à Braze, utilisez le filtre **Location Available** (Localisation disponible). Ce filtre vous permet de voir le pourcentage d’utilisateurs pour lesquels vous avez un « emplacement le plus récent ».

![Tester l’Emplacement le plus récent][25]

## Transfert de données

Confirmez auprès de vos développeurs que les données de localisation sont bien transmises à Braze. Normalement, le passage des données de localisation est géré automatiquement par le SDK une fois que l’utilisateur donne les autorisations, mais il est possible que vos développeurs aient désactivé le suivi de localisation dans Braze. Vous trouverez plus d’informations sur le suivi des données de localisation pour :
- [Android][26]
- [iOS][27]
- [Web][28]

Vous avez toujours besoin d’aide ? Ouvrez un [ticket de support]({{site.baseurl}}/braze_support/).

_Dernière mise à jour le 27 mars 2019_

[25]: {% image_buster /assets/img_archive/trouble7.png %}
[26]: {{site.baseurl}}/developer_guide/platform_integration_guides/android/analytics/location_tracking/
[27]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/analytics/location_tracking/
[28]: {{site.baseurl}}/developer_guide/platform_integration_guides/web/analytics/location_tracking/
