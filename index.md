---
title: 線上託管說明
permalink: index.html
layout: home
---

# <a name="azure-ai-fundamentals-exercises"></a>Azure AI Fundamentals 練習

這些實作練習是為了支援 [Microsoft Learn](https://docs.microsoft.com/training/) 上的訓練內容而設計。

您將需要 Microsoft Azure 訂用帳戶，以完成這些練習。 您可以在 [https://azure.microsoft.com](https://azure.microsoft.com) 註冊免費試用。

## <a name="labs"></a>實驗室

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions'" %}
| 模組 | 實驗室 |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
