---
nav_title: "POST : Envoyer des messages de campagne via une livraison déclenchée par API"
article_title: "POST : Envoyer des messages de campagne via une livraison déclenchée par API"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Braze Envoyer des messages de campagne via une livraison déclenchée par API."

---
{% api %}
# Envoyer des messages de campagne via une livraison déclenchée par API
{% apimethod post core_endpoint|https://www.braze.com/docs/core_endpoints %} 
/campaigns/trigger/send
{% endapimethod %}

Utilisez cet endpoint pour envoyer des messages instantanés et ad hoc aux utilisateurs désignés via la livraison déclenchée par API. La livraison déclenchée par API vous permet de stocker le contenu d’un message dans le tableau de bord de Braze, tout en indiquant quand et à qui un message est envoyé via votre API.

Si vous souhaitez cibler un segment, un enregistrement de votre demande sera stocké dans la [Developer Console (Console du développeur)](https://dashboard.braze.com/app_settings/developer_console/activitylog/). Notez que pour envoyer des messages avec cet endpoint, vous devez avoir un ID de campagne créé lorsque vous élaborez une [campagne déclenchée par API]({{site.baseurl}}/api/api_campaigns/).

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#aef185ae-f591-452a-93a9-61d4bc023b05 {% endapiref %}

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='send endpoints' category='message endpoints' %}

## Corps de la demande

```
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
```

```json
{
  "campaign_id": (required, string) voir l’identifiant de campagne,
  "send_id": (optional, string) voir l’identifiant d’envoi,
  "trigger_properties": (optional, object) les paires clé-valeur de personnalisation qui s’appliquent à tous les utilisateurs de cette demande,
  "broadcast": (optional, boolean) voir la diffusion ; défini par défaut sur « false » (faux) le 31/8/17, doit être défini sur « true » (vrai) si « destinataires » est absent,
  "audience": (optional, connected audience object) voir Audience connectée,
  // En incluant l’« audience », les messages seront uniquement envoyés aux utilisateurs de l’audience en question
  "recipients": (optional, array ; si non renseigné et que broadcast n’est pas défini sur `false` (faux), le message sera envoyé au segment entier ciblé par la campagne)
    [
      {
      // Soit « external_user_id » soit « user_alias » est nécessaire. Les demandes ne doivent en spécifier qu’un seul des deux.
      "user_alias": (optional, user alias object) l’alias utilisateur de l’utilisateur devant recevoir le message,
      "external_user_id": (optional, string) identifiant externe de l’utilisateur pour recevoir le message,
      "trigger_properties": (optional, object) les paires clé-valeur de personnalisation qui s’appliquent à l’utilisateur (ces paires clé-valeur vont écraser toute clé qui entre en conflit avec les trigger_properties du parent),
      "send_to_existing_only": (optional, boolean) défini sur true (vrai) par défaut, ne peut pas être utilisé avec un aliasing de l’utilisateur ; si défini sur `false`, un objet d’attribut doit être inclus,
      "attributes": (optional, object) les champs dans l’objet des attributs vont créer ou mettre à jour un attribut de ce nom avec la valeur fournie dans le profil utilisateur spécifié avant que le message ne soit envoyé et les valeurs existantes seront écrasées
    }
  ]
}
```

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
| --------- | ---------| --------- | ----------- |
|`campaign_id`|Required|String|Voir l’[identifiant de campagne]({{site.baseurl}}/api/identifier_types/). |
|`send_id`| Facultatif | String | Voir [Identifiant d’envoi]({{site.baseurl}}/api/identifier_types/). |
|`trigger_properties`| Facultatif | Objet | Voir [Propriétés du déclencheur]({{site.baseurl}}/api/objects_filters/trigger_properties_object/). Les paires clé-valeur de personnalisation qui s’appliquent à tous les utilisateurs de cette demande. |
|`broadcast` (diffusion)| Facultatif | Boolean | Voir [broadcast]({{site.baseurl}}/api/parameters/#broadcast). Ce paramètre est défini sur False par défaut (au 31 août 2017). <br><br> Si les `recipients` ne sont pas présents, `broadcast` (diffusion) doit être définie sur true (vrai). Cependant, faites attention lors de la configuration de `broadcast: true` (diffusion : vrai), car en configurant involontairement cet indicateur, vous pourriez envoyer votre campagne à une audience plus importante que prévue. |
|`audience`| Facultatif | Objet Audience connectée| Voir [Audience connectée]({{site.baseurl}}/api/objects_filters/connected_audience/). |
|`recipients`| Facultatif | Tableau | Voir [Objet de destinataire]({{site.baseurl}}/api/objects_filters/recipient_object/). Si non renseigné et que `broadcast` (diffusion) est définie sur true (vrai), le message sera envoyé au segment entier ciblé par la campagne. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

Le tableau des destinataires peut contenir jusqu’à 50 objets, avec chaque objet contenant une seule chaîne de caractères `external_user_id` et objet `trigger_properties`.

Quand `send_to_existing_only` est défini sur `true` (vrai), Braze envoie uniquement le message aux utilisateurs existants. Cependant, cet indicateur ne peut pas être utilisé avec les alias utilisateur. Quand `send_to_existing_only` est défini sur `false` (faux) et qu’un utilisateur avec l’`id` donné n’existe pas, Braze crée un utilisateur avec I’`id` et ses attributs avant d’envoyer le message.

## Exemple de demande
```
curl --location --request POST 'https://rest.iad-01.braze.com/campaigns/trigger/send' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "campaign_id": "campaign_identifier",
  "send_id": "send_identifier",
  "trigger_properties": "",
  "broadcast": false,
  "audience": {
    "AND": [
      {
        "custom_attribute": {
          "custom_attribute_name": "eye_color",
          "comparison": "equals",
          "value": "blue"
        }
      },
      {
        "custom_attribute": {
          "custom_attribute_name": "favorite_foods",
          "comparison": "includes_value",
          "value": "pizza"
        }
      },
      {
        "OR": [
          {
            "custom_attribute": {
              "custom_attribute_name": "last_purchase_time",
              "comparison": "less_than_x_days_ago",
              "value": 2
            }
          },
          {
            "push_subscription_status": {
              "comparison": "is",
              "value": "opted_in"
            }
          }
        ]
      },
      {
        "email_subscription_status": {
          "comparison": "is_not",
          "value": "subscribed"
        }
      },
      {
        "last_used_app": {
          "comparison": "after",
          "value": "2019-07-22T13:17:55+0000"
        }
      }
    ]
  },
  "recipients": [
    {
      "user_alias": {
        "alias_name" : "example_name",
        "alias_label" : "example_label"
      },
      "external_user_id": "external_user_identifier",
      "trigger_properties": "",
      "send_to_existing_only": true,
      "attributes": {
        "first_name" : "Alex"
      }
    }
  ]
}'
```

## Informations relatives à la réponse
Les réponses des endpoints d’envoi de messages incluront le `dispatch_id` du message pour y faire référence lors de l’envoi. Le `dispatch_id` est l’ID de distribution du message, un ID unique pour chaque transmission envoyée depuis la plateforme Braze. Lorsque vous utilisez cet endpoint, vous recevez un seul `dispatch_id` pour un ensemble complet d’utilisateurs regroupés. Pour plus d’informations sur `dispatch_id`, consultez notre documentation sur le [comportement de l’ID de distribution]({{site.baseurl}}/help/help_articles/data/dispatch_id/).

## Endpoint Créer un envoi

**Utilisation de l’objet Attributs dans les campagnes**

Braze dispose d’un objet d’envoi de messages appelé `Attributs` qui vous permet d’ajouter, de créer ou de mettre à jour les attributs et les valeurs d’un utilisateur avant de lui envoyer une campagne déclenchée par API en utilisant l’endpoint de `campaign/trigger/send`, car cet appel d’API traitera l’objet Attributs utilisateur avant qu’il ne traite et envoie la campagne. Cela permet de minimiser le risque de problèmes causés par des [conditions de concurrence]({{site.baseurl}}/help/best_practices/race_conditions/). 

{% alert important %}
Vous recherchez la version Canvas de cet endpoint ? Consultez [Envoyer des messages de Canvas via une livraison déclenchée par API]({{site.baseurl}}/api/endpoints/messaging/send_messages/post_send_triggered_canvases/#create-send-endpoint).
{% endalert %}

{% endapi %}