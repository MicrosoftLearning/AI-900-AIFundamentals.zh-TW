---
title: 線上託管說明
permalink: index.html
layout: home
---

# Azure AI 基本概念練習

這些實作練習是為了支援 [Microsoft Learn](https://docs.microsoft.com/training/) 上的訓練內容而設計。

若要完成這些練習，您需要 Microsoft Azure 訂用帳戶。 您可以在 [https://azure.microsoft.com](https://azure.microsoft.com) 註冊免費試用。

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| 練習 |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
