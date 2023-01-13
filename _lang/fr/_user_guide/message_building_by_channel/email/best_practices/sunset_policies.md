---
nav_title: Politiques de temporisation
article_title: Politiques de temporisation des e-mails
page_order: 8
page_type: reference
description: "Le présent article couvre les meilleures pratiques en matière de temporisation et décrit les situations dans lesquelles il vaut mieux arrêter d’envoyer des communications à des utilisateurs désengagés."
channel: E-mail

---

# Politiques de temporisation des e-mails

Bien sûr, il est parfois tentant d’envoyer des campagnes à autant d’utilisateurs que possible, mais il existe des situations où il vaut vraiment mieux arrêter d’envoyer des messages aux utilisateurs désengagés. 

Pour les e-mails, votre adresse IP d’envoi a un score de réputation basé sur l’engagement, le signalement de spam, les blocages, etc. Vous pouvez utiliser des outils comme [Sender Score](https://www.senderscore.org/ "Sender Score") ou le [Smart Network Data Service](https://postmaster.live.com/snds/ "Outlook's Smart Network Data Service") d’Outlook pour surveiller le score de votre réputation. Si votre score de réputation est constamment faible, les filtres de fournisseurs de services Internet et boîte aux lettres peuvent envoyer automatiquement vos e-mails dans un dossier spam ou à faible priorité pour tous les destinataires, même ceux qui sont engagés. La création d’une politique de temporisation permet de garantir que vos e-mails ne sont pas livrés aux destinataires inactifs. 

Les filtres de segmentation de Braze empêchent que vos communications ressemblent à du spam, en vous permettant de mettre en œuvre facilement des politiques de temporisation pour les e-mails, les notifications push et notifications in-app et les éléments du fil d'actualité. Voici quelques éléments à prendre en compte en créant une politique de temporisation

- Comment définit-on un utilisateur « non engagé » ? 
- L’engagement est-il défini par des clics, des achats, l’utilisation de l’appli ou une combinaison de ces comportements ? 
- Quelle durée d’inactivité avant d’arrêter d’envoyer des messages ?
- Allez-vous envoyer des campagnes spéciales aux utilisateurs avant de les exclure de vos segments ?
- À quels canaux de messagerie votre politique de temporisation sera-t-elle appliquée ? 

Par exemple, si vous avez des utilisateurs qui choisissent la [protection de la confidentialité dans Apple Mail ]({{site.baseurl}}/user_guide/message_building_by_channel/email/mpp/), réfléchissez à l’impact que cela peut avoir sur vos campagnes par e-mail et vos métriques de délivrabilité pour définir et optimiser votre politique de temporisation.

Pour intégrer des politiques de temporisation dans vos campagnes, créez un [segment][19] qui exclut automatiquement les utilisateurs ayant marqué vos e-mails comme spam ou n’ayant pas interagi avec vos messages pendant une certaine période.  

Pour configurer ces segments, choisissez les filtres `Has Marked You As Spam` et/ou `Last Engaged With Message` dans la section **Marketing Activity (Activité marketing)** dans la liste déroulante du filtre. 

Lorsque vous appliquez le filtre `Last Engaged With Message`, spécifiez le type de message (push, e-mail ou notification in-app) avec lequel l’utilisateur a ou n’a pas interagi, ainsi que le nombre de jours depuis la dernière interaction avec l’utilisateur. Après avoir créé un segment, choisissez de cibler ce segment avec un [canal de messagerie]({{site.baseurl}}/user_guide/message_building_by_channel/).

![Page Détails du segment avec filtre « Last Engaged with Message (Message de la dernière interaction) » sélectionné.][20]

La plateforme de Braze cesse automatiquement d’envoyer des e-mails aux utilisateurs qui vous ont marqué comme spam, mais le filtre `Has Marked You As Spam` vous permet également d’envoyer des messages de notification push ciblés, des notifications in-app et des cartes de fil d'actualité à ces utilisateurs. Ce filtre est utile pour [campagnes de reciblage][21]. Par exemple, vous pouvez envoyer aux utilisateurs désengagés des messages ou des fils d'actualités pour leur rappeler les fonctionnalités ou offres qu’ils manquent quand ils n’ouvrent pas vos e-mails.

Les politiques de temporisation peuvent être particulièrement utiles dans les campagnes par e-mail qui ciblent les utilisateurs inactifs. En effet, ces campagnes se concentrent sur des segments qui n’ont pas interagi avec votre application depuis un certain temps, et elles peuvent avoir un impact sur la délivrabilité de vos e-mails si vous incluez systématiquement des utilisateurs désengagés. Les politiques de temporisation vous permettent de cibler les utilisateurs inactifs sans terminer dans le dossier Courrier Indésirables.

[19]: {{site.baseurl}}/user_guide/engagement_tools/segments/creating_a_segment/#creating-a-segment
[20]: {% image_buster /assets/img_archive/email_sunset_policies_new.png %}
[21]: {{site.baseurl}}/user_guide/engagement_tools/campaigns/ideas_and_strategies/retargeting_campaigns/#retargeting-campaigns
