---
nav_title: "Objet Web"
article_title: Objet de communication Web
page_order: 12
page_type: reference
channel: Notification push
platform: Web
description: "Cet article répertorie et explique les différents objets Web utilisés chez Braze."

---
# Spécification de l’objet Notification push Web

Le `web_push` vous permet de définir ou de demander des informations relatives au contenu de notification push Web et de notification push Web pour les alertes via nos [endpoints de messagerie]({{site.baseurl}}/api/endpoints/messaging).

## Objet de notification push Web

```json
{
   "alert": (required, string) the notification message,
   "title": (required, string) the title that appears in the notification drawer,
   "extra": (optional, object) additional keys and values to be sent in the push,
   "message_variation_id": (optional, string) used when providing a campaign_id to specify which message variation this message should be tracked under (must be an Kindle/FireOS Push Message),
   "custom_uri": (optional, string) a web URL,
   "image_url": (optional, string) URL for image to show,
   "large_image_url": (optional, string) URL for large image, supported on Chrome Windows/Android,
   "require_interaction": (optional, boolean) whether to require the user to dismiss the notification, supported on Mac Chrome,
   "time_to_live": (optional, integer (seconds)),
   "send_to_most_recent_device_only" : (optional, boolean) defaults to false, if set to true, Braze will only send this push to a user's most recently used browser, rather than all eligibles browsers,
   "buttons" : (optional, array of Web Push Action Button Objects) push action buttons to display
}
```

La valeur de `image_url` doit être une URL qui renvoie à l’emplacement où votre image est hébergée. Les images doivent être recadrées au format 1:1.

## Objet Bouton d’action push Web

```json
{
  "text": (required, string) the button's text,
  "action": (optional, string) one of "OPEN_APP", "URI", or "CLOSE", defaults to "OPEN_APP",
  "uri": (optional, string) a web URL
}
```
