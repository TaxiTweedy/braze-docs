---
nav_title: Février
page_order: 11
noindex: true
page_type: update
description: "Cet article contient les notes de version de février 2022."
---
# Février 2022

## Étape des chemins d’expérience Canvas
La nouvelle Étape des chemins d’expérience Canvas vous permet de tester plusieurs chemins Canvas les uns par rapport aux autres et par rapport à un groupe de contrôle, à tout moment dans le parcours de l’utilisateur. Maintenant, vous pouvez tirer parti des analyses rassemblées ici pour déterminer encore plus précisément le parcours le plus efficace. En savoir plus sur la façon de créer une [Étape des chemins d’expérience]({{site.baseurl}}/user_guide/engagement_tools/canvas/canvas_components/experiment_step/).

## Gestion des numéros de téléphone non valides
Vous avez rencontré un scénario où un utilisateur a entré un numéro de téléphone non valide. Voici votre solution ! Braze marque ces numéros de téléphone comme non valides et ne tentera pas d’envoyer d’autres communications à ces numéros. En savoir plus sur la façon dont Braze [gère les numéros de téléphone non valides]({{site.baseurl}}/user_guide/message_building_by_channel/sms/phone_numbers/user_phone_numbers/#handling-invalid-phone-numbers/).

## Nouveaux endpoints pour SMS
Vous pouvez maintenant gérer les numéros de téléphone non valides en utilisant le nouvel [Endpoint SMS de Braze]({{site.baseurl}}/api/endpoints/sms/) ! Cette mise à jour comprend :
- [GET: L’endpoint de requête ou liste de numéros de téléphone non valides]({{site.baseurl}}/api/endpoints/sms/get_query_invalid_numbers/) renvoie une liste de numéros de téléphone considérés comme « non valides » par Braze.
- [POST: L’endpoint de suppression des numéros de téléphone invalides]({{site.baseurl}}/api/endpoints/sms/post_remove_invalid_numbers/) vous permet de supprimer ces numéros de téléphone « non valides » figurant sur la liste de numéros non valides de Braze.

## Limites de débit
Les limites de taux API ont été précisées dans tous les [articles sur les endpoints de Braze]({{site.baseurl}}/api/basics/#nav_top_endpoints). Vous pouvez maintenant afficher facilement les limites de débit par type de demande. Pour plus d’informations sur les limites de débit, consultez notre article sur les [Limites de débit de notre API]({{site.baseurl}}/api/api_limits/).

## Nouvel endpoint REST
Braze a ajouté un [nouvel endpoint EU-02 REST]({{site.baseurl}}/api/basics/#api-definitions).

## À propos de l’e-mail
Les e-mails sont un excellent moyen de communiquer avec vos clients. Pour une introduction rapide sur la façon de personnaliser et d’utiliser les e-mails, consultez notre nouvel article [À propos de l’e-mail]({{site.baseurl}}/user_guide/message_building_by_channel/email/about/). 

## À propos des messages in-app
Les messages in-app diffusent du contenu riche à vos utilisateurs qui sont actifs dans votre application. Vous pouvez facilement interagir avec vos clients actifs en créant des messages in-app pour des salutations personnalisées ou une adoption de fonctionnalité. Pour en savoir plus sur les avantages et les types de messages, consultez notre nouvel article [À propos des messages in-app]({{site.baseurl}}/user_guide/message_building_by_channel/in-app_messages/about/).