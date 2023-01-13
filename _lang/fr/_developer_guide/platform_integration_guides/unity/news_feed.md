---
nav_title: Fil d’actualité
article_title: Fil d’actualité de Unity
channel: Fil d’actualité
platform: 
  - Unity
  - iOS
  - Android
page_order: 5
description: "Cet article de référence couvre l’intégration de fils d’actualités pour la plateforme Unity."

---

# Fil d’actualité

## Réception des données du fil d’actualités dans Unity

Vous pouvez lister des objets de jeu Unity pour être avertis des cartes de fil d’actualités entrantes. 

Sur iOS, nous recommandons de définir des auditeurs d’objets de jeu à partir de l’éditeur de configuration Braze.

Sur Android, définir `com_braze_feed_listener_callback_method_name` et `com_braze_feed_listener_game_object_name` dans votre projet Unity `braze.xml`.

Pour configurer votre auditeur d’objet de jeu à l’exécution sur l’une ou l’autre plateforme, utilisez `AppboyBinding.ConfigureListener()` et spécifiez `BrazeUnityMessageType.NEWS_FEED`.

## Cartes d’analyse

Les messages `string` entrants reçus dans votre rappel d’objet de jeu peuvent être analysés dans notre objet [Feed][11] (Fil) pré-fourni, qui contient une liste d’objets [Card][12] (Carte) pour plus de commodité.

Pour plus de détails, consultez l’exemple suivant :

### Exemple de fonction de rappel

```csharp
void FeedReceivedCallback(string message) {
  Feed feed = new Feed(message);
  Debug.Log("Feed received: " + feed);
  foreach (Card card in feed.Cards) {
    Debug.Log("Card: " + card);
  }
}
```

## Actualisation du fil d’actualités

Pour actualiser le fil d’actualité à partir de Braze, utilisez l’une des méthodes suivantes :

```csharp
// results in a network request to Braze
AppboyBinding.RequestFeedRefresh()

AppboyBinding.RequestFeedRefreshFromCache()
```

Les deux méthodes informeront votre auditeur de fil d’actualités et transmettront le fil d’actualités à votre méthode de rappel.

## Analytique

Les clics et les impressions doivent être enregistrés manuellement pour les cartes qui ne sont pas affichées directement par Braze.

Utilisez `LogClick()` et `LogImpression()` dans [Card][12] (Carte) pour enregistrer des clics et des impressions pour des cartes spécifiques.

Pour consigner que l’utilisateur a consulté le flux dans son ensemble, appelez `AppboyBinding.LogFeedDisplayed()`.

[11]: https://github.com/Appboy/appboy-unity-sdk/blob/master/Assets/Plugins/Appboy/models/Feed.cs
[12]: https://github.com/Appboy/appboy-unity-sdk/blob/master/Assets/Plugins/Appboy/models/Cards/Card.cs
