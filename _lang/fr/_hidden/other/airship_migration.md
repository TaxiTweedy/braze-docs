---
nav_title: Migration du SDK depuis Airship vers Braze
permalink: /sdk_migration_guide_airship/
hidden: true
page_type: reference
---

# Migration des SDK depuis Airship vers Braze (iOS)

> Chez Braze, nous sommes conscients que le passage à une plateforme et un SDK entièrement nouveaux peut être intimidant, mais avec le guide de migration suivant, des exemples de code faciles à comprendre et des fonctionnalités impressionnantes, nous pensons que cela ne vous dérangera pas. Dans cet article, nous avons inclus l’équivalent Braze de nombreuses fonctionnalités clés d’Airship, ainsi que des extraits de code SDK « chercher-remplacer » pour rendre votre migration à la fois simple et rapide.

## Au-delà du code
### Gestion des jetons
Braze utilise le jeton d’appareil Apple, pour iOS.

| **Perspective Braze :**<br>Nous veillons à ce que les clients puissent communiquer en continu avec leurs utilisateurs (par exemple, avec des notifications push) lorsqu’ils migrent d’Airship vers Braze (qu’il s’agisse d’une migration avec basculement complet vers Braze, ou d’une transition partielle de type 50/50, etc.). |
{: .reset-td-br-1}

#### Migration des jetons de notification push

Il est nécessaire de [migrer des jetons de notification push via l’API]({{site.baseurl}}/help/help_articles/push/push_token_migration/#migration-via-api). La documentation liée contient des étapes spécifiques, ainsi qu’un exemple de charge utile, mais le processus global est le suivant :

1. Importer les jetons via le endpoint [`/users/track`]({{site.baseurl}}/api/endpoints/user_data/post_user_track/). Pour les importations de lots, nous disposons de ressources pour accélérer le processus. Contactez votre COM ou SA pour plus de détails !
2. Si le jeton existe déjà dans Braze, il sera ignoré. Sinon, un profil anonyme sera généré.
3. Assurance qualité de l’intégration de notification push. Assurez-vous que les étapes de [configuration des notifications push]({{site.baseurl}}/developer_guide/platform_integration_guides/ios/push_notifications/integration/) ont été achevées.

Si vos profils d’utilisateur et vos jetons de notification push sont stockés à des endroits distincts, nous vous recommandons d’importer des jetons de notification push de manière anonyme, puis de migration ultérieurement vos profils d’utilisateur existants. Il n’est pas nécessaire de les mapper ensemble car le SDK iOS de Braze va gérer la résolution du jeton lors de l’intégration réussie.

- Nous recommandons de migrer des utilisateurs via API, mais s’il est nécessaire d’importer une liste statique d’utilisateurs, cela peut être fait avec un CSV. Notez que **les jetons de notification push ne peuvent pas être importés via CSV** parce que le « jeton de notification push » ne peut pas être spécifié dans le CSV. Pour afficher un modèle d’importation et en savoir plus sur l’importation des données dans le tableau de bord, consultez notre [Documentation CSV]({{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/user_import/#csv).

{% alert note %}
Les jetons de notification push peuvent apparaître sous la forme `subscribed` dans le tableau de bord de Braze, mais ils deviendront `opted-in` une fois que les utilisateurs débuteront une session avec le SDK Braze.
{% endalert %}

#### Plusieurs jetons de notification push

Avec Braze, un utilisateur peut avoir plusieurs jetons de notification push (un pour chaque appareil) et en ciblant tous les jetons de notification push valides, vous pouvez envoyer des notifications à plusieurs appareils d’utilisateur. Il est également possible de configurer des campagnes pour qu’elles ne soient envoyées qu’à l’appareil le plus récent d’un utilisateur.

## Configuration de la campagne
Avec une certaine maîtrise, Braze est un véritable outil unique dans l’espace d’engagement des clients. Grâce à nos options de personnalisation étendues et à notre ensemble de fonctionnalités croissantes, les campagnes migrées dans Braze bénéficient souvent de la replanification pour tirer profit des avantages de ces outils, et notre framework de planification de campagne (contactez votre COM ou SA pour plus de détails) est spécialement conçu pour cela.

### Composition
#### Notifications push
Braze nécessite des canaux distincts pour les notifications push (un pour iOS, un pour Android).

| **Perspective Braze :**<br>Nous offrons à nos clients la possibilité d’obtenir le meilleur des deux mondes au lieu d’avoir à faire des concessions. Être capable de tirer parti de l’ensemble des capacités d’un seul canal offre plus de flexibilité pour le marketeur et une expérience utilisateur améliorée. Cela nous permet d’adopter les dernières fonctionnalités de chaque système d’exploitation ; par exemple, Android prenait en charge des notifications riches avant iOS. |
{: .reset-td-br-1}

Braze peut envoyer des notifications push aux utilisateurs qui ne mettent pas à jour leur application avec le SDK de Braze installé. Étant donné que Braze dispose d’un jeton de notification push valide, Braze peut envoyer la notification push sans le SDK Braze car les APN s’occupent du reste. Il est crucial de noter que **l’analyse de cette notification push ne sera pas disponible pour les builds sans le SDK Braze**.

##### Partage des jetons

Pour les campagnes spécifiques au cycle de vie qui doivent continuer pendant votre processus de migration vers le SDK Braze, les utilisateurs peuvent être éligibles à la réception de notifications de Braze et Airship, étant donné que Braze a reçu un jeton de notification push valide.

#### Centre de messages
Pour remplacer la fonctionnalité de campagne de centre de messages Airship, nous vous recommandons de créer une campagne multicanal qui consiste en une notification push et une [Carte de contenu]({{site.baseurl}}/user_guide/message_building_by_channel/content_cards/). Pour en savoir plus sur la façon d’utiliser les cartes de contenu au format de centre de messages, consultez notre [Guide d’implémentation de carte de contenu iOS]({{site.baseurl}}/developer_guide/platform_integration_guides/ios/content_cards/implementation_guide/#content-cards-in-a-message-center).

### Segmentation
Braze propose plusieurs [segmentations]({{site.baseurl}}/user_guide/engagement_tools/segments/) pour offrir une expérience utilisateur riche à vos clients.

| **Perspective Braze :**<br> Les segments de Braze sont entièrement dynamiques : les utilisateurs accéderont et quitteront le segment en fonction des conditions définies. |
{: .reset-td-br-1}

#### Migration de segment utilisateur

Pour recréer directement un segment statique Airship dans Braze, il existe deux options :
- **Importer via API - Affecter un attribut personnalisé** (recommandé)<br>
Nous recommandons d’importer des utilisateurs via l’endpoint d’API [/users/track]({{site.baseurl}}/api/endpoints/user_data/post_user_track/) tout en affectant un attribut personnalisé à ces utilisateurs importés. Par exemple, vous pouvez créer un segment d’utilisateurs qui possèdent chacun un attribut personnalisé `Segment_Group_1` défini sur `true`. Pour segmenter ces utilisateurs ultérieurement, vous pouvez [créer un segment]({{site.baseurl}}/user_guide/engagement_tools/segments/creating_a_segment/) de tous les utilisateurs, où `Segment_Group_1` est `true`.<br><br>
- **Filtre basé sur l’importation CSV d’utilisateurs**<br>
Il existe une option de Braze pour filtrer uniquement les utilisateurs inclus dans une importation CSV spécifique. Cette option de filtrage est visible lors de l'étape des utilisateurs cibles (outils d'engagement) dans « Filtrer les utilisateurs par `Updated/Imported via CSV` ».
![Importation CSV du filtre][1]{: style="max-width:90%;border:0;"}
Notez que pour les importations CSV, un `External ID` est demandé pour chaque utilisateur importé, et **les segments avec des utilisateurs anonymes (ou alias) ne pourront pas être importés**. Pour afficher un modèle d’importation et en savoir plus sur l’importation des données dans le tableau de bord, consultez notre [Documentation CSV]({{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/user_import/#csv).

## Rechercher/remplacer les extraits de code SDK
Afin de simplifier la migration, nous avons mis en évidence les extraits de code SDK d’Airship suivants présents dans votre code, avec les extraits de code SDK de Braze correspondants pour les remplacer. Consultez les sujets suivants pour commencer :
- [Installation](#installation)
- [Obtenir et définir l’ID utilisateur](#userid)
- [Activation des notifications push](#pushnotifications)
- [Analyse](#analytics)
- [Gestion des messages dans l’application](#iammessages)
- [Cartes de contenu et centre de messages](#messagecenter)

### Installation {#installation}
{% tabs %}
{% tab Swift %}
**Airship**
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) {

    UAirship.takeOff(UAConfig.default())

    UALocation.shared()?.isLocationUpdatesEnabled = true
    UALocation.shared().isBackgroundLocationUpdatesAllowed = true

    UAirship.push()?.notificationOptions = [.alert, .badge, .sound]
    UAirship.push()?.userPushNotificationsEnabled = true
    UAirship.push()?.pushNotificationDelegate = self

    UAInAppAutomation.shared()?.inAppMessageManager.delegate = self
    UAInAppAutomation.shared()?.inAppMessageManager.displayInterval = 30
}
```
**Braze**
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) {

    Appboy.start(withApiKey: apiKey, in: application, withLaunchOptions: launchOptions, withAppboyOptions: appboyOptions)

    locationManager.requestAlwaysAuthorization() // locationManager is a CLLocationManager property variable

    // Push Notifications
    let options: UNAuthorizationOptions = [.alert, .sound, .badge]
    UNUserNotificationCenter.current().requestAuthorization(options: options) { (granted, error) in
      Appboy.sharedInstance()?.pushAuthorization(fromUserNotificationCenter: granted)
    }
    UIApplication.shared.registerForRemoteNotifications()

    // In-App Messages
    Appboy.sharedInstance()?.inAppMessageController.inAppMessageUIController?.setInAppMessageUIDelegate?(self)
}
```
{% endtab %}
{% tab Objective-C %}
**Airship**
```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

  [UAirship takeOff:[UAConfig defaultConfig]];

  [[UALocation shared] setLocationUpdatesEnabled:YES];
  [[UALocation shared] setBackgroundLocationUpdatesAllowed:YES];

  [UAirship push].notificationOptions = UNAuthorizationOptionAlert | UNAuthorizationOptionSound | UNAuthorizationOptionBadge;
  [[UAirship push] setUserPushNotificationsEnabled:YES];
  [[UAirship push] setPushNotificationDelegate:self];

  [UAInAppAutomation shared].inAppMessageManager.delegate = self;
  [UAInAppAutomation shared].inAppMessageManager.displayInterval = 30;

  return YES;
}
```
**Braze**
```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

  [Appboy startWithApiKey:self.apiKey inApplication:application withLaunchOptions:launchOptions withAppboyOptions:self.appboyOptions];

  [self.locationManager requestAlwaysAuthorization]; // locationManager is a CLLocationManager property variable

  // Push Notifications
  UNAuthorizationOptions options = UNAuthorizationOptionAlert | UNAuthorizationOptionSound | UNAuthorizationOptionBadge;
  [[UNUserNotificationCenter currentNotificationCenter] requestAuthorizationWithOptions:options
                          completionHandler:^(BOOL granted, NSError * _Nullable error) {
    [[Appboy sharedInstance] pushAuthorizationFromUserNotificationCenter:granted];
  }];
  [[UIApplication sharedApplication] registerForRemoteNotifications];

  // In-App Messages
  [[Appboy sharedInstance].inAppMessageController.inAppMessageUIController setInAppMessageUIDelegate:self];

  return YES;
}
```

{% endtab %}
{% endtabs %}

### Obtenir et définir l’ID utilisateur {#userid}
{% tabs %}
{% tab Swift %}
**Airship**
```swift
extension AirshipManager {
  var userId: String? {
    return UAirship.namedUser()?.identifier
   }

  func setUser(_ userId: String) {
    UAirship.namedUser()?.identifier = userId
  }
}
```
**Braze**
```swift
extension AppboyManager {
  var userId: String? {
     return Appboy.sharedInstance()?.user.userID
  }

  func changeUser(_ userId: String) {
    Appboy.sharedInstance()?.changeUser(userId)
  }
}
```
{% endtab %}
{% tab Objective-C %}
**Airship**
```objc

- (NSString *)userId {
  return [UAirship namedUser].identifier
}

- (void)setUser:(NSString *)userId {
  [[UAirship namedUser] setIdentifier:userId];
}
```
**Braze**
```objc
- (NSString *)userId {
  return [Appboy sharedInstance].user.userID;
}

- (void)changeUser:(NSString *)userId {
  [[Appboy sharedInstance] changeUser: userId];
}
```
{% endtab %}
{% endtabs %}

### Gestion des notifications push {#pushnotifications}
{% tabs %}
{% tab Swift %}
**Airship**
```swift
extension AirshipManager: UAPushNotificationDelegate {
  func receivedBackgroundNotification(_ notificationContent: UANotificationContent, completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
    completionHandler(.noData)
  }

  func receivedForegroundNotification(_ notificationContent: UANotificationContent, completionHandler: @escaping () -> Void) {
    completionHandler()
  }

  func receivedNotificationResponse(_ notificationResponse: UANotificationResponse, completionHandler: @escaping () -> Void) {
    completionHandler()
  }
}
```
**Braze**
```swift
extension AppboyManager {
  func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    Appboy.sharedInstance()?.registerDeviceToken(deviceToken)
  }

  func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
    Appboy.sharedInstance()?.register(application, didReceiveRemoteNotification: userInfo, fetchCompletionHandler: completionHandler)
  }

  func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
    Appboy.sharedInstance()?.userNotificationCenter(center, didReceive: response, withCompletionHandler: completionHandler)
  }
}
```
{% endtab %}
{% tab Objective-C %}
**Airship**
```objc
- (void)receivedBackgroundNotification:(UANotificationContent *)notificationContent completionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {
  completionHandler(UIBackgroundFetchResultNoData);
}

- (void)receivedForegroundNotification:(UANotificationContent *)notificationContent completionHandler:(void (^)(void))completionHandler {
  completionHandler();
}

- (void)receivedNotificationResponse:(UANotificationResponse *)notificationResponse completionHandler:(void (^)(void))completionHandler {
  completionHandler();
}
```
**Braze**
```objc
- (void)application:(UIApplication *)application didRegisterForRemoteNotifications
  func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    Appboy.sharedInstance()?.registerDeviceToken(deviceToken)
  }

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  [[Appboy sharedInstance] registerDeviceToken:deviceToken];
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {
  [[Appboy sharedInstance] registerApplication:application
                didReceiveRemoteNotification:userInfo
                      fetchCompletionHandler:completionHandler];
}

- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void (^)(void))completionHandler {
  [[Appboy sharedInstance] userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
}
```
{% endtab %}
{% endtabs %}

### Analyse {#analytics}
{% tabs %}
{% tab Swift %}
**Airship**
```swift
extension AirshipManager {
  func trackEvent(with name: String, value: NSDecimalNumber? = nil, eventProperties: [String: Any]? = nil) {
    let event = UACustomEvent(name: name, value: value)

    if let eventProperties = eventProperties {
      event.properties = eventProperties
    }

    event.track()
  }

  func applyMutationsWithValue(_ value: String, forAttribute attribute: String) {
    let mutations = UAAttributeMutations()
    mutations.setString(value, forAttribute: attribute)
    UAirship.namedUser().apply(mutations)
  }
}
```
**Braze**
```swift
extension AppboyManager {
  func logCustomEvent(_ eventName: String, withProperties properties: [AnyHashable: Any]? = nil) {
    Appboy.sharedInstance()?.logCustomEvent(eventName, withProperties: properties)
  }

  func setCustomAttributeWithKey(_ key: String, andStringValue value: String) {
    Appboy.sharedInstance()?.user.setCustomAttributeWithKey(key, andStringValue: value)
  }

  func logPurchase(productIdentifier: String, inCurrency currency: String, atPrice price: String, withQuanitity quanity: Int) {
    Appboy.sharedInstance()?.logPurchase(productIdentifier, inCurrency: currency, atPrice: NSDecimalNumber(string: price), withQuantity: UInt(quanity))
  }
}
```
{% endtab %}
{% tab Objective-C %}
**Airship**
```objc
- (void)trackEventWith:(NSString *)name value:(NSDecimalNumber *)value eventProperties:(NSDictionary *)eventProperties {
  UACustomEvent *event = [[UACustomEvent alloc] init];
  event.eventName = name;
  event.eventValue = value;
  event.properties = eventProperties;

  [event track];
}

- (void)applyMutationWith:(NSString *)value forAttribute:(NSString *)attribute {
  UAAttributeMutations* mutations = [[UAAttributeMutations alloc] init];
  [mutations setString:value forAttribute:attribute];
  [[UAirship namedUser] applyAttributeMutations:mutations];
}
```
**Braze**
```objc
- (void)logCustomEvent:(NSString *)eventName withProperties:(NSDictionary *)properties {
  [[Appboy sharedInstance] logCustomEvent:eventName withProperties: properties];
}

- (void)setCustomAttributeWithKey:(NSString *)key andStringValue:(NSString *)value {
  [[Appboy sharedInstance].user setCustomAttributeWithKey:key andStringValue:value];
}

- (void)logPurchase:(NSString *)productIdentifier inCurrency:(NSString *)currency atPrice:(NSString *)price withQuantity:(NSInteger)quantity {
  [[Appboy sharedInstance] logPurchase:productIdentifier inCurrency:currency atPrice:[[NSDecimalNumber alloc] initWithString:price] withQuantity:quantity];
}
```
{% endtab %}
{% endtabs %}

### Gestion des messages dans l’application {#iammessages}
{% tabs %}
{% tab Swift %}
**Airship**
```swift

extension AirshipManager: UAInAppMessagingDelegate {
  func extend(_ message: UAInAppMessage) -> UAInAppMessage {
      return message
  }

  func messageWillBeDisplayed(_ message: UAInAppMessage, scheduleID: String) {
  }

  func messageFinishedDisplaying(_ message: UAInAppMessage, scheduleID: String, resolution: UAInAppMessageResolution) {
  }
}
```
**Braze**
```swift
extension AppboyManager: ABKInAppMessageControllerDelegate {
  func before(inAppMessageDisplayed inAppMessage: ABKInAppMessage) -> ABKInAppMessageDisplayChoice {
    // This delegate method defines whether the in-app message will be displayed now, displayed later, or discarded.
    return .displayInAppMessageNow
  }

  func beforeControlMessageImpressionLogged(_ inAppMessage: ABKInAppMessage) -> ABKInAppMessageDisplayChoice {
    // This delegate method defines the timing of when the control in-app message impression event should be logged: now, later, or discarded.
    return .displayInAppMessageNow
  }
}

extension AppboyManager: ABKInAppMessageUIDelegate {
  func on(inAppMessageDismissed inAppMessage: ABKInAppMessage) {
    // Use this method to perform any custom logic that should execute after the in-app message has been dismissed
  }

  func on(inAppMessageClicked inAppMessage: ABKInAppMessage) -> Bool {
    // This delegate method is fired when the user clicks on a slide-up in-app message or a modal/full in-app message without button(s) on it.
    return true
  }

  func on(inAppMessageButtonClicked inAppMessage: ABKInAppMessageImmersive, button: ABKInAppMessageButton) -> Bool {
    // This delegate method is fired whenever the user clicks a button on the in-app message.
    return true
  }

  func on(inAppMessageHTMLButtonClicked inAppMessage: ABKInAppMessageHTMLBase, clickedURL: URL?, buttonID buttonId: String) -> Bool {
    // This delegate method is fired whenever the user clicks a link on the HTML in-app message.
    return true
  }
}
```
{% endtab %}
{% tab Objective-C %}
**Airship**
```objc
- (UAInAppMessage *)extendMessage:(UAInAppMessage *)message {

  return message;
}

- (void)messageWillBeDisplayed:(UAInAppMessage *)message scheduleID:(NSString *)scheduleID {

}

- (void)messageFinishedDisplaying:(UAInAppMessage *)message scheduleID:(NSString *)scheduleID resolution:(UAInAppMessageResolution *)resolution {

}
```
**Braze**
```objc
- (ABKInAppMessageDisplayChoice) beforeInAppMessageDisplayed:(ABKInAppMessage *)inAppMessage {
  return ABKDisplayInAppMessageNow;
}

- (ABKInAppMessageDisplayChoice) beforeControlMessageImpressionLogged:(ABKInAppMessage *)inAppMessage {
  return ABKDisplayInAppMessageNow;
}

- (void)onInAppMessageDismissed:(ABKInAppMessage *)inAppMessage {
  // Use this method to perform any custom logic that should execute after the in-app message has been dismissed
}

- (BOOL)onInAppMessageClicked: (ABKInAppMessage *)inAppMessage {
  // This delegate method is fired when the user clicks on a slide-up in-app message or a modal/full in-app message without button(s) on it.
  return YES;
}

- (BOOL)onInAppMessageButtonClicked:(ABKInAppMessageImmersive *)inAppMessage
                             button:(ABKInAppMessageButton *)button {
  return YES;
}

- (BOOL)onInAppMessageHTMLButtonClicked:(ABKInAppMessageHTML *)inAppMessage
                             clickedURL:(nullable NSURL *)clickedURL
                               buttonID:(NSString *)buttonID {
  return YES;
}
```
{% endtab %}
{% endtabs %}

### Cartes de contenu et centre de messages {#messagecenter}
{% tabs %}
{% tab Swift %}
**Airship**
```swift
extension AirshipManager {
  func displayMessageCenter() {
    UAMessageCenter.shared()?.defaultUI.title = "My Message Center"

    let style = UAMessageCenterStyle()
    style.navigationBarColor = .black
    style.titleColor = .white
    style.tintColor = .white

    UAMessageCenter.shared()?.defaultUI.messageCenterStyle = style
    UAMessageCenter.shared()?.display()
  }
}
```
**Braze**
```swift
extension AppboyManager {
  func displayContentCards(navigationController: UINavigationController?) {
    let contentCardsVc = ABKContentCardsTableViewController()
    contentCardsVc.title = "My Message Center"
    contentCardsVc.disableUnreadIndicator = true
    navigationController?.pushViewController(contentCardsVc, animated: true)
  }
}
```
{% endtab %}
{% tab Objective-C %}
**Airship**
```objc
- (void)displayMessageCenter {
  [UAMessageCenter shared].defaultUI.title = @"My Message Center";
  [[UAMessageCenter shared] display];
}
```
**Braze**
```objc
- (void)displayContentCards:(UINavigationController *)navigationController {
  ABKContentCardsTableViewController *contentCards = [[ABKContentCardsTableViewController alloc] init];
  contentCards.title = @"My Message Center";
  [self.navigationController pushViewController:contentCards animated:YES];
}
```
{% endtab %}
{% endtabs %}

[1]: {% image_buster /assets/img/csv_filter.png %}
