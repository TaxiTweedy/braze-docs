---
nav_title: Comment les attributs de campagne et les attributs Canvas diffèrent entre les sources
article_title: Comment les attributs de campagne et les attributs Canvas diffèrent entre les sources dans Braze 
page_order: 1

page_type: reference
description: "Cet article compare les ID et noms d’attribut de campagne et de Canvas sur les différentes sources de Braze."
platform: API
---

# Comment les attributs de campagne et les attributs Canvas diffèrent entre les sources dans Braze

Les noms et ID de campagne, Canvas et Canvas Step sont tous disponibles dans Liquid, notre API REST et Currents. Ces attributs correspondent à la même valeur dans les trois sources, mais ils peuvent avoir des noms différents. Cette page est destinée à vous aider établir les liens entre ces trois attributs.

## Cas d’utilisation

### Liquid

Les attributs Campagne et Canvas sont disponibles sous forme de tags Liquid sur notre tableau de bord {% raw %}(c.-à-d. `{{campaign.${api_id}}}`){% endraw %}. Vous pouvez utiliser Liquid pour transmettre ces attributs dans le message lui-même, dans un Contenu connecté ou en tant que paires valeur-clé. C’est généralement fait à des fins de suivi.

### API REST

Les attributs Campagne et Canvas sont également disponibles dans l’[endpoint Détails de la campagne]({{site.baseurl}}/api/endpoints/export/campaigns/get_campaign_details/) ou [Détails du Canvas]({{site.baseurl}}/api/endpoints/export/canvas/get_canvas_details/). Vous pouvez utiliser notre API REST pour créer des mappages, c’est-à-dire une liste de tous les noms de Canvas et leurs ID correspondants.

### Currents

Les attributs Campagne et Canvas sont liés à [événements d’engagement]({{site.baseurl}}/user_guide/data_and_analytics/braze_currents/event_glossary/message_engagement_events) de Currents. C’est important pour pouvoir déterminer la campagne ou la Canvas Step associée à l’envoi de push ou l’ouverture d’e-mail.

## Attributs de campagne 

| Attribut | Liquid | API REST | Currents |
| --- | --- | --- | --- |
| Nom de campagne | {% raw %}`{{campaign.${name}}}`{% endraw %} | Nom | campagne_nom |
| ID Campagne | {% raw %}`{{campaign.${api_id}}}`{% endraw %} | S.O. (utilisé comme entrée pour l’appel API lui-même) | Campagne_ID |
| Nom de la variante | {% raw %}`{{campaign.${message_name}}}`{% endraw %} | messages.message_variation_nom.id | S.O. (mapper le nom de la variante sur l’ID Variante avec l’endpoint Détails de campagne) |
| Variant ID | {% raw %}`{{campaign.${message_api_id}}}`{% endraw %} | messages.message_variation_ID | message_variation_ID |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}

## Attributs Canvas

| Attribut | Liquid | API REST | Currents |
| --- | --- | --- | --- |
| Nom du Canvas | {% raw %}`{{canvas.${name}}}`{% endraw %} | Nom | Nom_Canvas  |
| ID Canvas | {% raw %}`{{canvas.${api_id}}}`{% endraw %} | S.O. (utilisé comme entrée pour l’appel API lui-même) | canvas_id |
| Nom de la variante | {% raw %}`{{canvas.${variant_name}}}`{% endraw %} | nom.variantes | canvas_variation_nom |
| Variant ID | {% raw %}`{{canvas.${variant_api_id}}}`{% endraw %} | variants.name.id | canvas_variation_ID |
| Nom de l’étape | {% raw %}`{{campaign.${name}}}`{% endraw %} | nom.étapes | canvas_étape_nom |
| ID Étape | {% raw %}`{{campaign.${api_id}}}`{% endraw %} | steps.id | canvas_étape_ID |
| Canal de communication | N/A | étapes.messages.message_variation_canal.id | S.O. (inhérente à un type d’événement, par exemple envoi de push ou ouverture d’e-mail) |
| Message ID | {% raw %}`{{campaign.${message_api_id}}}`{% endraw %} | étapes.message.message_variation_ID | message_variation_ID |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3 .reset-td-br-4}