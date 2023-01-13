---
nav_title: Vidéo
article_title: Vidéo dans les messages In-App
page_order: 4
page_type: reference
description: "Le présent article décrit comment intégrer des vidéos dans vos messages In-App HTML."
channel:
  - messages In-App
---

# Vidéo dans les messages In-App {#video}

Pour lire une vidéo dans un message In-App HTML, incluez les éléments suivants `<video>` dans votre HTML, et remplacez le nom de la vidéo par celui de votre fichier (ou l’URL de la ressource distante).

Pour utiliser une ressource vidéo locale, assurez-vous d’inclure ce fichier lors du téléchargement de ressources dans votre campagne.

Pour prendre en charge les appareils iOS, vous devez inclure l’attribut `playsinline` car la lecture plein écran n’est pas prise en charge pour le moment.

{% alert note %}
iOS ne prend pas en charge la lecture automatique par défaut. Pour mettre à jour cette option par défaut, vous pouvez modifier [`ABKInAppMessageHTMLViewController`](https://github.com/Appboy/appboy-ios-sdk/blob/master/AppboyUI/ABKInAppMessage/ViewControllers/ABKInAppMessageHTMLViewController.m)
{% endalert %}

Pour intégrer des vidéos et autres contenus HTML5 dans des messages In-App HTML sur Android, l’accélération matérielle est requise dans l’activité où le message In-App s’affiche. Pour plus d’informations, consultez le [guide du développeur Android]({{site.baseurl}}/developer_guide/platform_integration_guides/android/in-app_messaging/customization/youtube_in_html/).

Vous pouvez trouver d’autres options `<video>` possibles dans les [documents Web MDN][9]

```html
<video class="video" autoplay muted playsinline controls>
  <source src="https://video-provider.com/YOUR_VIDEO_FILE.mp4" type="video/mp4">
  <source src="https://video-provider.com/YOUR_VIDEO_FILE.ogg" type="video/ogg">
  Your device does not support playing this video.
</video>
```

{% alert warning %}
Les vidéos plein écran ne sont pas correctement rendues sur iOS et ne sont pas prises en charge pour le moment. Vous devez inclure l’attribut `playsinline` pour afficher à la place la vidéo dans le message HTML.
{% endalert %}

[9]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video
