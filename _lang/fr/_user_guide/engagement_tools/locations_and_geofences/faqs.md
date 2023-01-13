---
nav_title: FAQ
article_title: FAQ sur les localisations et geofences
page_order: 4
page_type: FAQ
description: "Cet article de référence aborde plusieurs questions fréquemment posées sur l’utilisation des geofences."
tool: Location

---

# FAQ sur les localisations et geofences

## Localisations

### Quand Braze recueille-t-il des données de localisation ?

Braze enregistre uniquement les données de localisation lorsque l’application est ouverte en avant-plan. Par conséquent, notre filtre `Most Recent Location` cible les utilisateurs en fonction du dernier endroit où ils ont ouvert l’application (également appelé début de session). 

Gardez les nuances suivantes à l’esprit :

- Si le suivi de la géolocalisation est désactivé, le filtre `Most Recent Location` affichera le dernier emplacement enregistré.
- Si un utilisateur a déjà eu un emplacement enregistré sur son profil, il sera éligible pour le filtre `Location Available`, même s’il a désactivé le suivi de la géolocalisation depuis que l’emplacement a été enregistré.

### Quelle est la différence entre le filtre Most Recent Device Locale (Dernière localisation de l’appareil) et Most Recent Location (Dernière localisation) ?

La `Most Recent Device Locale` provient des paramètres de l’appareil de l’utilisateur. Pour les utilisateurs d’iPhone, ces informations se trouvent dans **Paramètres** > **Général** > **Langue et région**. Ce filtre est utilisé pour collecter des informations sur la langue et la mise en forme régionale, telles que les dates et adresses, et est indépendant du filtre `Most Recent Location`.

La `Most Recent Location` correspond aux dernières données GPS connues du dispositif. Ces informations sont mises à jour lors de l’ouverture d’une session.

### Si un utilisateur désactive le suivi de la géolocalisation, leurs anciennes données de géolocalisation seront-elles supprimées de Braze ?

Non ! Si un utilisateur a déjà eu un emplacement enregistré sur son profil, ces données ne seront pas automatiquement supprimées même si cet utilisateur désactive le suivi de la géolocalisation ultérieurement.

## Geofences

### Combien de geofences puis-je stocker ?

Selon la [documentation][3] Android, les applications Android ne peuvent stocker localement que 100 geofences à la fois. Braze est configuré pour stocker jusqu’à 20 geofences par application en local. Pour que les geofences fonctionnent correctement, vous devez vous assurer que votre application n’utilise pas tous les emplacements de geofence disponibles.

Les appareils iOS peuvent surveiller jusqu’à 20 [geofences][4] à la fois par application. Braze surveille jusqu’à 20 emplacements s’il y a suffisamment d’espace disponible. Pour que les geofences fonctionnent correctement, vous devez vous assurer que votre application n’utilise pas tous les emplacements de geofence disponibles.

### Combien de geofences puis-je télécharger sur Braze ?

Vous pouvez créer ou télécharger une quantité illimitée de geofences dans le tableau de bord, ce qui permet à votre équipe marketing de configurer des campagnes et des ensembles de geofences sans avoir à calculer le nombre de geofences. Cependant, chaque ensemble de geofences peut contenir un maximum de 10 000 geofences. Braze synchronise de façon dynamique les geofences que nous suivons pour chaque utilisateur, en veillant à ce que les geofences les plus pertinentes soient toujours disponibles.

### Quel est le niveau de précision des geofences de Braze ?

Les geofences de Braze utilisent une combinaison de tous les outils de géolocalisation disponibles sur un appareil pour trianguler l’emplacement de l’utilisateur. Cela comprend le Wi-Fi, le GPS et les antennes-relais.

La précision type est de 20 à 50 m et le plus haut degré de précision est compris entre 5 et 10 m. Dans les zones rurales, la précision peut se dégrader considérablement, potentiellement sur plusieurs kilomètres. Braze recommande de créer des geofences avec des rayons plus importants pour les zones rurales.

### Comment les geofences affectent-elles la durée de vie de la batterie ?

Notre solution de geofence utilise le service de système de geofence natif d’iOS et Android et est réglée pour équilibrer de manière intelligente la précision et la performance, garantissant ainsi une durée de vie optimale de la batterie ainsi que des améliorations de performances lorsque le service sous-jacent est amélioré.

### Quand les geofences sont-elles actives ?

Les geofences de Braze fonctionnent à toute heure de la journée, même lorsque votre application est fermée.

### Quelle est la fréquence d’actualisation des geofences pour les utilisateurs ?

Pour les utilisateurs actifs, le SDK de Braze ne demandera de geofences qu’une fois par jour au démarrage de la session. Cela signifie que si des modifications sont apportées aux ensembles de geofences après le début de la session, vous devrez attendre 24 heures à compter de la première collecte des ensembles pour recevoir l’ensemble mis à jour.

Pour les utilisateurs inactifs, si les notifications push sont activées en arrière-plan, Braze enverra également une notification push silencieuse toutes les 24 heures pour extraire les derniers emplacements de l’appareil.

Pour les utilisateurs individuels, vous pouvez mettre à jour manuellement les ensembles de geofences à tout moment en cliquant sur **Re-sync Geofences (Résynchroniser les geofences)** dans le coin inférieur de la page **Locations (Emplacements)**.

{% alert note %}
Si les geofences ne sont pas chargées localement sur l’appareil, l’utilisateur ne pourra pas déclencher la geofence même s’il pénètre dans la zone délimitée.
{% endalert %}

### Quelle est la différence entre les geofences et la segmentation de l’emplacement le plus récent ?

Dans Braze, les geofences sont un concept différent de la segmentation basée sur l’emplacement le plus récent. Les geofences sont uniquement utilisées pour les déclencheurs, notamment pour envoyer un message lorsqu’un utilisateur entre ou sort d’une zone spécifique. Les segments basés sur le filtre `Most Recent Location` sont utilisés pour cibler une région spécifique de votre audience, par exemple pour envoyer un message aux utilisateurs situés à New York.

[3]: https://developers.google.com/android/reference/com/google/android/gms/location/package-summary
[4]: https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/LocationAwarenessPG/RegionMonitoring/RegionMonitoring.html
