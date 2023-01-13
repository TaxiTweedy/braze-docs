---
nav_title: Définir des ID utilisateur
article_title: Définir des ID utilisateur pour Roku
platform: Roku
page_order: 0
page_type: reference
description: "Cette page couvre les méthodes d’identification des utilisateurs, ainsi que les meilleures pratiques et les considérations importantes."
 
---

# Définir des ID utilisateur

{% multi_lang_include archive/setting_user_ids/setting_user_ids.md %}

Vous devez effectuer l’appel suivant dès que l’utilisateur est identifié (généralement après s’être connecté) afin de définir l’ID utilisateur :

```
m.Braze.setUserId(YOUR_USER_ID_STRING)
```

## Convention de dénomination des ID utilisateur suggérée

{% multi_lang_include archive/setting_user_ids/naming_convention.md %}

## Meilleures pratiques et remarques sur l’intégration de l’ID utilisateur

{% multi_lang_include archive/setting_user_ids/best_practices.md %}

[1]: {{site.baseurl}}/developer_guide/rest_api/user_data/#user-data
[2]: {{site.baseurl}}/api/endpoints/messaging/
