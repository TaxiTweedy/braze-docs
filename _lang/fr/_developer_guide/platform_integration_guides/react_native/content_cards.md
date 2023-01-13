---
nav_title: Cartes de contenu
article_title: Cartes de contenu pour React Native
platform: React Native
page_order: 3
page_type: reference
description: "Cet article explique comment démarrer avec les cartes de contenu pour les applications React Native."
channel: cartes de contenu

---

# Cartes de contenu

Les SDK Braze incluent un flux de cartes par défaut pour vous permettre de démarrer avec les cartes de contenu. Pour afficher le flux de carte, vous pouvez utiliser la méthode `ReactAppboy.launchContentCards()`. Le flux de cartes par défaut inclus avec le SDK Braze traitera tous les suivis, les masquages et le rendu des cartes de contenu d’un utilisateur.

## Personnalisation

Vous pouvez utiliser ces méthodes supplémentaires pour créer un flux de cartes de contenu personnalisé dans votre application :

| Méthode                                         | Description                                                                                            |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `ReactAppboy.requestContentCardsRefresh()`     | Demande les dernières cartes de contenu au serveur Braze SDK.                                           |
| `ReactAppboy.getContentCards()`                | Récupère les cartes de contenu du SDK Braze. Cela renverra la dernière liste de cartes du serveur. |
| `ReactAppboy.logContentCardClicked(cardId)`    | Enregistre un clic pour l’ID de carte de contenu donné.                                                            |
| `ReactAppboy.logContentCardImpression(cardId)` | Enregistre une impression pour l’ID de carte de contenu donné.                                                      |
| `ReactAppboy.logContentCardDismissed(cardId)`  | Enregistre un rejet pour l’ID de carte de contenu donné.                                                        |
{: .reset-td-br-1 .reset-td-br-2}

## Test affichant l’exemple de carte de contenu

Suivez ces étapes pour tester un exemple de carte de contenu.

1. Définir un utilisateur actif dans l’application React en appelant la méthode `ReactAppboy.changeUserId('your-user-id')`.
2. Accédez à **Campagnes** et suivez [ce guide][4] pour créer une nouvelle campagne de carte de contenu.
3. Composez votre campagne de carte de contenu et rendez-vous sur l’onglet **Test**. Ajouter le même `user-id` comme utilisateur de test et cliquez sur **Send Test** (Envoyer le test). Vous devriez pouvoir lancer rapidement une carte de contenu sur votre périphérique.

![Une campagne de carte de contenu Braze indiquant que vous pouvez ajouter votre propre ID utilisateur en tant que destinataire de test pour tester votre carte de contenu.][5]

Pour plus d’intégrations, suivez les [Instructions d’intégration Android][2] ou les [Instructions d’intégration iOS][3], selon votre plateforme.

Un exemple d’implémentation de ce type de document est disponible dans AppboyProject, dans le [SDK React][1].

[1]: https://github.com/Appboy/appboy-react-sdk
[2]: {{site.baseurl}}/developer_guide/platform_integration_guides/android/content_cards/data_models/
[3]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/content_cards/data_model/
[4]: {{site.baseurl}}/user_guide/message_building_by_channel/content_cards/create

[5]: {% image_buster /assets/img/react-native/content-card-test.png %} "Content Card Campaign Test"
