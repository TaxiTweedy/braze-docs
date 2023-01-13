---
nav_title: Abandon du contenu connecté
article_title: Abandon du contenu connecté
page_order: 2
description: "À l’aide d’un placage liquide, vous avez la possibilité d’abandonner des messages avec des conditionnements. Le présent article de référence couvre un message qui abordera les meilleures pratiques."

---

# Abandon des messages {#aborting-connected-content}

À l’aide d’un plan de liquide, vous avez la possibilité d’abandonner des messages avec logique conditionnelle. Par exemple :

{% raw %}
```
{% connected_content https://example.com/webservice.json :save connected %}
   {% if connected.recommendations.size < 5 or connected.foo.bar == nil %}
     {% abort_message() %}
   {% endif %}
```

Dans cet exemple, les conditionnements `connected.recommendations.size < 5` et `connected.foo.bar == nil` spécifier des situations qui entraîneront l’abandon du message.

Vous pouvez également spécifier une raison d’abandon, qui sera enregistrée dans le **Journal des activités du message** dans votre **Developer Console**. Cette raison d’abandon doit être une chaîne de caractères et ne peut pas contenir de liquide.

`{% abort_message('Could not get enough recommendations') %}`
{% endraw %}

{% alert important %}
Braze ne compte pas les messages abandonnés vers le compte d’envoi sur votre compte Braze ou dans Currents.
{% endalert %}
