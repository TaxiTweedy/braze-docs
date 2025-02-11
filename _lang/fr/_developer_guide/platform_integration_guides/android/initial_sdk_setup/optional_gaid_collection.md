---
nav_title: ID publicitaire Google (facultatif)
article_title: ID publicitaire Google en option pour Android
page_order: 9
platform: 
  - Android
description: "Cet article couvre les ID publicitaires Google et comment transmettre ces informations publicitaires à Braze pour votre application Android ou FireOS."

---

# ID publicitaire Google en option (Android uniquement)

L’[ID publicitaire Google][2] est un ID pour la publicité spécifique, anonyme, unique et pouvant être réinitialisé, fourni par les services Google Play. Le GAID permet aux utilisateurs de réinitialiser leur identifiant, de désactiver les publicités axées sur les centres d’intérêt dans les applications Google Play et de fournir aux développeurs un système simple et standard pour continuer à monétiser leurs applications.

## Transmettre l’ID publicitaire Google à Braze

L’ID publicitaire Google n’est pas automatiquement collecté par le SDK Braze et doit être défini manuellement via la méthode [`Braze.setGoogleAdvertisingId()`][1].

{% alert important %}
Google exige que l’ID publicitaire soit collecté sur un fil non-IU.
{% endalert %}

{% tabs %}
{% tab JAVA %}

```java
new Thread(new Runnable() {
  @Override
  public void run() {
    try {
      AdvertisingIdClient.Info idInfo = AdvertisingIdClient.getAdvertisingIdInfo(getApplicationContext());
      Braze.getInstance(getApplicationContext()).setGoogleAdvertisingId(idInfo.getId(), idInfo.isLimitAdTrackingEnabled());
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}).start();
```

{% endtab %}
{% tab KOTLIN %}

```kotlin
Thread(Runnable {
  try {
    val idInfo = AdvertisingIdClient.getAdvertisingIdInfo(getApplicationContext())
    Braze.getInstance(getApplicationContext()).setGoogleAdvertisingId(idInfo.id, idInfo.isLimitAdTrackingEnabled)
  } catch (e: Exception) {
    e.printStackTrace()
  }
}).start()
```

{% endtab %}
{% endtabs %}


[1]: https://appboy.github.io/appboy-android-sdk/kdoc/braze-android-sdk/com.braze/-i-braze/set-google-advertising-id.html
[2]: https://support.google.com/googleplay/android-developer/answer/6048248/advertising-id?hl=en
