---
nav_title: Entonnoirs de segments
article_title: Entonnoirs de segments
page_order: 3

page_type: reference
tool: Segments
description: "Cet article de référence explique comment utiliser les entonnoirs de segments de Braze et présente les meilleures pratiques à suivre ainsi que des exemples d’utilisation."

---

# Entonnoirs de segments

> Cet article de référence explique comment utiliser les entonnoirs de segments de Braze et présente les meilleures pratiques à suivre ainsi que des cas d’utilisation. 
> <br>
> <br>
> Les entonnoirs de segments sont parfaits pour limiter la taille de votre audience pour un cas d’utilisation de campagne spécifique, apprendre de cette audience et de ses interactions, et utiliser ces connaissances afin d’élaborer des stratégies et de concevoir des campagnes efficaces.

Les entonnoirs de segments vous permettent de voir comment chaque filtre que vous ajoutez affecte les statistiques de votre segment. Lorsque vous créez un segment, une ligne de données apparaîtra sous chaque filtre. Ces données fourniront les informations suivantes sur les utilisateurs ciblés par tous les filtres à ce moment-là :

- Nombre total d’utilisateurs ciblés et pourcentage de votre base utilisateur
- Valeur à vie et valeur à vie pour les utilisateurs payants  
- Nombre d’utilisateurs pouvant recevoir des e-mails
- Nombre d’utilisateurs abonnés aux communications par e-mail
- Nombre d’utilisateurs ayant activé les notifications push  
- Nombre d’utilisateurs abonnés aux notifications push

![][1]

## Meilleures pratiques

- Ajouter des filtres qui documentent votre flux utilisateur vous permet de voir à quel endroit vous perdez des utilisateurs. Par exemple, si vous avez une application de réseau social et que vous voulez voir à quelle étape vous risquez de perdre des utilisateurs pendant votre processus d’onboarding, vous pouvez ajouter des filtres de données personnalisés pour s’inscrire, ajouter des amis et envoyer un premier message. Si vous découvrez que 85 % des utilisateurs s’inscrivent et ajoutent des amis, mais que seulement 45 % ont envoyé un premier message, alors vous saurez qu’il vous faut encourager les utilisateurs à envoyer plus de messages pendant vos campagnes d’onboarding et de marketing.

- Les entonnoirs de segments vous permettent de comparer le pourcentage d’utilisateurs qui effectuent différentes actions. Par exemple, est-ce que les utilisateurs actifs, ou ceux qui ont une valeur à vie élevée, [ont tendance à interagir davantage avec les notifications push ou les e-mails][4] ? Pour en savoir plus, créez un segment d’utilisateurs actifs avec un ou plusieurs filtres, puis voyez comment les statistiques changent lorsque vous ajoutez un filtre pour s’abonner aux notifications push et lorsque vous ajoutez un filtre pour s’abonner aux communications par e-mail.

- Analysez la façon dont la valeur à vie change lorsque vous ajoutez des filtres. Pour les utilisateurs actifs, les personnes qui se connectent à Facebook ou celles qui se connectent à Twitter ont-elles une valeur à vie plus élevée ? Ou encore, la valeur à vie est-elle considérablement plus élevée pour les personnes qui se sont connectées aux deux ? Si vous trouvez, par exemple, que le fait de se connecter à Twitter a très peu d’impact sur la valeur à vie, mais que se connecter à Facebook a un impact important, vous pouvez décider d’encourager les connexions à Facebook dans vos campagnes marketing.

## Exemples de cas d’utilisation

### Impact d’une action utilisateur spécifique sur les conversions {#push-email}

En analysant l’impact d’une certaine action effectuée par un utilisateur (comme l’ajout d’articles à une liste d’envies) sur une conversion (comme effectuer des achats), vous pouvez répondre aux questions suivantes :

- L’action de l’utilisateur coïncide-t-elle avec davantage d’achats ?
- Quelle est l’importance de l’action de l’utilisateur ? Devez-vous créer des campagnes marketing qui encouragent davantage cette action ?

Supposons par exemple que vous ayez un groupe dans lequel tous les utilisateurs qui ont ajouté des articles à une liste d’envies ont également effectué un achat. Étant donné que seul un petit pourcentage d’utilisateurs ont ajouté des articles à une liste d’envies, l’application peut souhaiter encourager ce comportement à travers des campagnes marketing.

![Exemple d’entonnoir de segments avec les filtres suivants : « Last used these apps less than 30 days ago (A utilisé ces applications pour la dernière fois il y a moins de 30 jours) », « Last Added Item to Waitlist less than 30 days ago (Dernier article ajouté à liste d’envies il y a moins de 30 jours) », et « Last Made Purchase less than 30 days ago (Dernier achat effectué il y a moins de 30 jours) » pour atteindre un total de 4 302 utilisateurs.][3]

### Comparer les canaux de messagerie

Créez un segment d’utilisateurs actifs (ou d’utilisateurs ayant les traits souhaités) et comparez leurs interactions avec différents canaux d’engagement, tels que le Fil d’actualité, les e-mails et les notifications push. Par exemple, si les utilisateurs les plus loyaux sont abonnés aux notifications push, vous pourriez passer plus de temps à envoyer des campagnes par notification push aux utilisateurs actifs. Cependant, si vous constatez que la valeur à vie est plus élevée pour les personnes qui sont abonnées aux communications par e-mail, vous pourriez inviter plus d’utilisateurs actifs à s’abonner aux e-mails.

![Entonnoir de segments pour une campagne par e-mail avec les filtres suivants : « Last Made Purchase less than 30 days ago (Dernier achat effectué il y a moins de 30 jours) », « Last used these apps less than 30 days ago (A utilisé ces applications pour la dernière fois il y a moins de 30 jours) », « Push Enabled is true (Notifications push activées) », et « Email Subscription Status is Opted In (Statut d’abonnement aux e-mails : abonné) » pour atteindre un total de 2 799 utilisateurs.][5]


[1]: {% image_buster /assets/img_archive/segment_funnel_example.png %}
[3]: {% image_buster /assets/img_archive/Wish_List_2.png %}
[4]: #push-email
[5]: {% image_buster /assets/img_archive/Wish_List_Email.png %}
