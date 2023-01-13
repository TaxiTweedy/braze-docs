---
nav_title: Cartes de contenu
article_title: Cartes de contenu pour Unity
platform: 
  - Unity
  - iOS
  - Android
channel: cartes de contenu
page_order: 4
description: "Cet article de référence couvre les directives d’implémentation des cartes de contenu pour la plateforme Unity."

---

# Cartes de contenu

## Affichage natif des cartes de contenu {#unity-content-cards-native-ui}

Vous pouvez afficher l’interface utilisateur par défaut pour les cartes de contenu à l’aide de l’appel suivant :

```csharp
Appboy.AppboyBinding.DisplayContentCards();
```

## Réception des données de carte de contenu dans Unity

Vous pouvez lister des objets de jeu Unity pour être avertis des cartes de contenu entrantes. Nous recommandons de définir des auditeurs d’objets de jeu à partir de l’éditeur de configuration Braze.

Si vous devez configurer votre auditeur d’objet de jeu lors de l’exécution, utilisez `AppboyBinding.ConfigureListener()` et spécifiez `BrazeUnityMessageType.CONTENT_CARDS_UPDATED`.

Notez que vous devrez également appeler `AppboyBinding.RequestContentCardsRefresh()` pour commencer à recevoir des données dans votre auditeur d’objet de jeu sur iOS.

## Analyse des cartes de contenu

Les messages `string` entrants reçus dans votre rappel d’objet de jeu de cartes de contenu peuvent être analysés dans notre objet de modèle [`ContentCard`][17] pré-fournis pour plus de commodité.

L’analyse des cartes de contenu nécessite l’analyse Json, consultez l’exemple suivant pour plus de détails :

##### Exemple de fonction de rappel des cartes de contenu

```csharp
void ExampleCallback(string message) {
  try {
    JSONClass json = (JSONClass)JSON.Parse(message);

    // Content Card data is contained in the `mContentCards` field of the top level object.
    if (json["mContentCards"] != null) {
      JSONArray jsonArray = (JSONArray)JSON.Parse(json["mContentCards"].ToString());
      Debug.Log(String.Format("Parsed content cards array with {0} cards", jsonArray.Count));

      // Iterate over the card array to parse individual cards.
      for (int i = 0; i < jsonArray.Count; i++) {
        JSONClass cardJson = jsonArray[i].AsObject;
        try {
          ContentCard card = new ContentCard(cardJson);
          Debug.Log(String.Format("Created card object for card: {0}", card));

          // Example of logging Content Card analytics on the ContentCard object 
          card.LogImpression();
          card.LogClick();
        } catch {
          Debug.Log(String.Format("Unable to create and log analytics for card {0}", cardJson));
        }
      }
    }
  } catch {
    throw new ArgumentException("Could not parse content card JSON message.");
  }
}
```

## Rafraîchir les cartes de contenu

Pour actualiser les cartes de contenu de Braze, appelez l’une des méthodes suivantes :

```csharp
// results in a network request to Braze
AppboyBinding.RequestContentCardsRefresh()

AppboyBinding.RequestContentCardsRefreshFromCache()
```

## Analytique

Les clics et les impressions doivent être enregistrés manuellement pour les cartes de contenu non affichées directement par Braze.

Utiliser `LogClick()` et `LogImpression()` sur [ContentCard][17] (Carte de contenu) pour enregistrer des clics et des impressions pour des cartes spécifiques.

[17]: https://github.com/Appboy/appboy-unity-sdk/blob/master/Assets/Plugins/Appboy/models/Cards/ContentCard.cs
