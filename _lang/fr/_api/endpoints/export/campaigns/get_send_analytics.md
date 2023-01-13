---
nav_title: "GET : Envoyer des analyses"
article_title: "GET : Envoyer des analyses"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Statistiques quotidiennes de campagne par ID d’envoi de Braze."

---
{% api %}
# Endpoint Envoyer des analyses
{% apimethod get %}
/sends/data_series
{% endapimethod %}

Cet endpoint vous permet de récupérer une série quotidienne de diverses statistiques pour un `send_id` suivi. Braze stocke les envois d’analyse pendant 14 jours après l’envoi.

Les conversions de campagne seront attribuées à l’ID d’envoi le plus récent qu’un utilisateur donné a reçu de la campagne.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#76f822a8-a13b-4bfb-b20e-72b5013dfe86 {% endapiref %}

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| --------- | -------- | --------- |------------ |
| `campaign_id` | Requis | Chaîne de caractères | Voir [Identifiant API de campagne]({{site.baseurl}}/api/identifier_types/). |
| `send_id` | Requis | Chaîne de caractères | Voir [Identifiant API d’envoi]({{site.baseurl}}/api/identifier_types/). |
| `length` | Requis | Entier | Nombre maximum de jours avant `ending_at` à inclure dans la série renvoyée. Doit être compris entre 1 et 100 (inclus). |
| `ending_at` | Facultatif | Datetime <br>(chaîne de caractères [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601)) | Date à laquelle la série de données doit se terminer. Par défaut, l’heure de la demande. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande 
{% raw %}
```
curl --location -g --request GET 'https://rest.iad-01.braze.com/sends/data_series?campaign_id={{campaign_identifier}}&send_id={{send_identifier}}&length=30&ending_at=2014-12-10T23:59:59-05:00' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```
{% endraw %}

## Réponse

### Réponse API de l’endpoint Envoyer des analyses

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
            "variation_name": (string) variation name,
            "sent": (int) the number of sends,
            "delivered": (int) the number of messages successfully delivered,
            "undelivered": (int) the number of undelivered,
            "delivery_failed": (int) the number of rejected,
            "direct_opens": (int) the number of direct opens,
            "total_opens": (int) the number of total opens,
            "bounces": (int) the number of bounces,
            "body_clicks": (int) the number of body clicks,
            "revenue": (float) the number of dollars of revenue (USD),
            "unique_recipients": (int) the number of unique recipients,
            "conversions": (int) the number of conversions,
            "conversions_by_send_time": (int) the number of conversions,
            "conversions1": (int, optional) the number of conversions for the second conversion event,
            "conversions1_by_send_time": (int, optional) the number of conversions for the second conversion event by send time,
            "conversions2": (int, optional) the number of conversions for the third conversion event,
            "conversions2_by_send_time": (int, optional) the number of conversions for the third conversion event by send time,
            "conversions3": (int, optional) the number of conversions for the fourth conversion event,
            "conversions3_by_send_time": (int, optional) the number of conversions for the fourth conversion event by send time
          }
        ]
      },
      "conversions_by_send_time": 0,
      "conversions1_by_send_time": 0,
      "conversions2_by_send_time": 0,
      "conversions3_by_send_time": 0,
      "conversions": 0,
      "conversions1": 0,
      "conversions2": 0,
      "conversions3": 0,
      "unique_recipients": 1,
      "revenue": 0
    }
  ],
  "message": "success"
}
```

{% alert tip %}
Pour obtenir de l’aide sur les exportations CSV et de l’API, consultez la section [Résolution des problèmes d’exportation]({{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).
{% endalert %}

{% endapi %}
