---
nav_title: "Objet Webhook"
article_title: Objet de messagerie Webhook
page_order: 13
page_type: reference
channel: 
  - webhook
description: "Cet article présente l’objet webhook de Braze."

---

# Spécification de l’objet Webhook

Le `webhook` vous permet de modifier ou de créer des messages webhook via nos [endpoints de messagerie]({{site.baseurl}}/api/endpoints/messaging).

```json
{
  "url": (required, string),
  "request_method": (required, string) one of "POST", "PUT", "DELETE", or "GET",
  "request_headers": (optional, Hash) key-value pairs to use as request headers,
  "body": (optional, string) if you want to include a JSON object, make sure to escape quotes and backslashes,
  "message_variation_id": (optional, string) used when providing a campaign_id to specify which message variation this message should be tracked under
}
```

En tant que meilleure pratique, Braze recommande de fournir une valeur explicite pour `Content-Type` dans le champ `request_headers` afin de garantir un comportement cohérent et prévisible, car les expéditeurs et les serveurs peuvent changer au fil du temps. Si aucune valeur n’est spécifiée pour l’en-tête `Content-Type`, elle sera déduite du corps de la requête.
