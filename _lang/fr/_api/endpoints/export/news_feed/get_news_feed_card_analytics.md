---
nav_title: "GET : Analyse des cartes de fil d’actualité"
article_title: "GET : Analyse des cartes de fil d’actualité"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Liste de segments pour exporter une liste de segments disponibles et son utilisation."

---
{% api %}
# Endpoint Analyse des cartes de fil d’actualité
{% apimethod get %}
/feed/data_series
{% endapimethod %}

Cet endpoint vous permet de récupérer une série quotidienne de statistiques d’engagement pour une carte au fil du temps.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#9cdc3b1e-641e-4d62-b9e8-42d04ee9d4d8 {% endapiref %}

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre   | Requis | Type de données | Description |
| ----------- | -------- | --------- | ----------- |
| `card_id`   | Requis      | Chaîne de caractères    | Voir [Identifiant API de carte]({{site.baseurl}}/api/identifier_types/). <br><br> Le `card_id` pour une carte donnée se trouve sur la page **Developer Console (Console du développeur)** et sur la page d’informations relatives à la carte dans votre tableau de bord, sinon vous pouvez utiliser l’[endpoint Liste des fils d’actualité]({{site.baseurl}}/api/endpoints/export/news_feed/get_news_feed_cards/).|
| `length`    | Requis      | Entier | Nombre maximum d’unités (jours ou heures) avant `ending_at` à inclure dans la série renvoyée. Doit être compris entre 1 et 100 (inclus). |
| `unit`      | Facultatif       | Chaîne de caractères   | Unité de temps entre les points de données. Peut être `day` ou `hour`, valeur par défaut `day`.  |
| `ending_at` | Facultatif | Datetime <br>(chaîne de caractères [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601)) | Date à laquelle la série de données doit se terminer. Par défaut, l’heure de la demande. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
{% raw %}
```
curl --location -g --request GET 'https://rest.iad-01.braze.com/feed/data_series?card_id={{card_identifier}}&length=14&unit=day&ending_at=2018-06-28T23:59:59-5:00' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```
{% endraw %}

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "data" : [
        {
            "time" : (string) point in time - as ISO 8601 extended when unit is "hour" and as ISO 8601 date when unit is "day",
            "clicks" : (int) ,
            "impressions" : (int),
            "unique_clicks" : (int),
            "unique_impressions" : (int)
        },
        ...
    ]
}
```

{% alert tip %}
Pour obtenir de l’aide sur les exportations CSV et de l’API, consultez la section [Résolution des problèmes d’exportation]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
