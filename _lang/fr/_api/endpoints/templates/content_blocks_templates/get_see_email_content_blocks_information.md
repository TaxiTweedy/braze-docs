---
nav_title: "GET : Voir les informations sur les blocs de contenu"
article_title: "GET : Voir les informations sur les blocs de contenu"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Braze Afficher les informations sur les blocs de contenu disponibles."
---

{% api %}
# Voir les informations sur les blocs de contenu
{% apimethod get %}
/content_blocks/info
{% endapimethod %}

Cet endpoint appelle les informations de vos [blocs de contenu d’e-mail]({{site.baseurl}}/user_guide/engagement_tools/templates_and_media/content_blocks/) existants.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#589adda3-0def-4369-9ddc-eae71923c0ee {% endapiref %}

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='default' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `content_block_id`  | Requis | Chaîne de caractères | Identifiant du bloc de contenu. <br><br>Vous pouvez le trouver en répertoriant les informations de bloc de contenu via un appel d’API ou en accédant à **Developer Console (Console du développeur)** > **API Settings (Paramètres API)**, puis défilez vers le bas et recherchez votre identifiant d’API bloc de contenu.|
| `include_inclusion_data`  | Facultatif | Booléen | Quand il est défini sur `true`, l’API renvoie l’identifiant d’API Variation de message des campagnes et des Canvas où ce bloc de contenu est inclus, à utiliser lors des appels ultérieurs.  Les résultats excluent les campagnes ou Canvas archivé(e)s ou supprimé(e)s. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande
{% raw %}
```
curl --location -g --request GET 'https://rest.iad-01.braze.com/content_blocks/info?content_block_id={{content_block_id}}&include_inclusion_data=false' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'
```
{% endraw %}

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-API-KEY-HERE
{
  "content_block_id": "string",
  "name": "string",
  "content": "string",
  "description": "string",
  "content_type": "html or text",
  "tags":  "array of strings",
  "created_at": "time-in-iso",
  "last_edited": "time-in-iso",
  "inclusion_count" : "integer",
  "inclusion_data": "array",
  "message": "success",
}
```

### Erreurs possibles

Le tableau suivant répertorie les erreurs renvoyées possibles et les étapes de résolution des problèmes associées.

| Erreur | Résolution des problèmes |
| --- | --- |
| L’ID du bloc de contenu ne peut pas être vide | Assurez-vous qu’un bloc de contenu est répertorié dans votre demande et compris entre des guillemets (`""`). |
| L’ID du bloc de contenu n’est pas valide pour ce groupe d’apps | Ce bloc de contenu n’existe pas ou est dans un compte de société ou un groupe d’apps différent. |
| Le bloc de contenu a été supprimé : contenu non disponible | Ce bloc de contenu, bien qu’il ait pu exister, a été supprimé. |
| Inclure les données d’inclusion : erreur | Ce paramètre accepte uniquement les valeurs booléennes (vrai ou faux). Assurez-vous que la valeur de `include_inclusion_data` n’est pas comprise entre des guillemets (`""`), sinon la valeur est envoyée comme chaîne de caractères. Voir les [paramètres de demande](#request-parameters) pour plus d’informations. |
{: .reset-td-br-1 .reset-td-br-2}


{% endapi %}
