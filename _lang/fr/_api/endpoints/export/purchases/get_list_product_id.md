---
nav_title: "GET : Répertorier les ID de produit"
article_title: "GET : Répertorier les ID de produit"
search_tag: Endpoint
page_order: 1
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Braze Répertorier les ID de produit."

---
{% api %}
# Endpoint Répertorier les ID de produit
{% apimethod get %}
/purchases/product_list
{% endapimethod %}

Cet endpoint renvoie les listes paginées d’ID de produit.

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#dff4ed40-81f5-451d-9d44-accc0e932285{% endapiref %}

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='purchases product list' %}

## Paramètres de demande

| Paramètre | Requis | Type de données | Description |
|---|---|---|---|
| `page`  | Facultatif | Chaîne de caractères | La page de votre liste de produits que vous souhaitez afficher. |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de demande

{% raw %}
```
https://rest.iad-01.braze.com/purchases/product_list?page=1
```
{% endraw %}

## Réponse

```json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "products": [
    "5499334426779",
    "5499334819995",
    "5499335442587",
    "5499335835803",
    "Calendula Face Mask Peel",
    "Dior Lip Gloss",
    "Rice Bowl",
    "product_name"
  ],
  "message": "success"
}
```

{% endapi %}
