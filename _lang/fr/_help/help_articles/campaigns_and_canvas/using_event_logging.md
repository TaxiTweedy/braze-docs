---
nav_title: Journalisation des événements
article_title: Journalisation des événements
page_order: 6

page_type: solution
description: "Cet article d’aide décrit comment utiliser la journalisation des événements pour résoudre les problèmes liés à l’intégration de Braze."
---

# Journalisation des événements

Le [Journal d’événements utilisateurs][1] vous aide à résoudre les problèmes liés à votre intégration Braze. Deux choses à configurer sont particulièrement utiles :
* [Un profil anonyme](#setting-up-an-anonymous-profile)
* [La journalisation des événements](#using-event-logging)

## Configuration d’un profil anonyme

Pour configurer un profil anonyme, consultez cet article sur [l’ajout d’utilisateurs de test][2].

## Journalisation des événements

Utilisez la journalisation des événements pour voir à quoi ressemble le comportement pour un utilisateur anonyme. Cela peut être particulièrement utile pour identifier l’ID utilisateur si l’application testée ne collecte pas l’adresse de courriel. Vous pouvez utiliser Braze avec l’adresse IP de votre appareil pour ajouter cet appareil en tant qu’utilisateur test.

C’est également un excellent moyen de trouver des utilisateurs anonymes. Vous pouvez également utiliser ces informations pour tester les données envoyées à Braze et vérifier les incohérences. Dans cette vue, vous pouvez voir si les deltas de vos données sont envoyés à Braze. Si une adresse e-mail ou un jeton est envoyé à chaque événement enregistré, alors toutes les données sont envoyées à Braze.

Vous avez toujours besoin d’aide ? Ouvrez un [ticket de support]({{site.baseurl}}/braze_support/).

_Dernière mise à jour le 27 mars 2019_

[1]: {{site.baseurl}}/user_guide/administrative/app_settings/developer_console/event_user_log_tab
[2]: {{site.baseurl}}/user_guide/administrative/app_settings/developer_console/internal_groups_tab/#adding-test-users