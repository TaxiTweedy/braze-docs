---
nav_title: "GET : Informations relatives à la carte de fil d’actualité"
article_title: "GET : Informations relatives à la carte de fil d’actualité"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Informations relatives à la carte de fil d’actualité."

---
{% api %}
# Endpoint Informations relatives à la carte de fil d’actualité
{% apimethod get %}
/feed/details
{% endapimethod %}

Cet endpoint vous permet de récupérer des informations pertinentes sur la carte, qui peuvent être identifiées par le `card_id`.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#5b1401a6-f12c-4827-82c9-8dc604f1671e {% endapiref %}

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description            |
| --------- | -------- | --------- | ---------------------- |
| `card_id`   | Requis      | Chaîne de caractères    | Voir [Identifiant API de carte]({{site.baseurl}}/api/identifier_types/). <br><br> Le `card_id` pour une carte donnée se trouve sur la page **Developer Console (Console du développeur)** et sur la page d’informations relatives à la carte dans votre tableau de bord, sinon vous pouvez utiliser l’[endpoint Liste des fils d’actualité]({{site.baseurl}}/api/endpoints/export/news_feed/get_news_feed_cards/).|
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
{% raw %}
```
curl --location -g --request GET 'https://rest.iad-01.braze.com/feed/details?card_id={{card_identifier}}' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```
{% endraw %}

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) The status of the export, returns 'success' when completed without errors,
    "created_at" : (string) Date created as ISO 8601 date,
    "updated_at" : (string) Date last updated as ISO 8601 date,
    "name" : (string) Card name,
    "publish_at" : (string) Date card was published as ISO 8601 date,
    "end_at" : (string) Date card will stop displaying for users as ISO 8601 date,
    "tags" : (array) Tag names associated with the card,
    "title" : (string) Title of the card,
    "image_url" : (string) Image URL used by this card,
    "extras" : (dictionary) Dictionary containing key-value pair data attached to this card,
    "description" : (string) Description text used by this card,
    "archived": (boolean) whether this Card is archived,
    "draft": (boolean) whether this Card is a draft,
}
```

{% alert tip %}
Pour obtenir de l’aide sur les exportations CSV et de l’API, consultez la section [Résolution des problèmes d’exportation]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
