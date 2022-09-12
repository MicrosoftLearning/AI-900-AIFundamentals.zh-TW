---
title: 線上託管說明
permalink: index.html
layout: home
ms.openlocfilehash: 86fa2da9bfa9e4d7edb0c853f77e95fe69e97411
ms.sourcegitcommit: 3fc8440b350b498c2f50ab4ce531a0f906792584
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2022
ms.locfileid: "147866003"
---
# <a name="azure-ai-fundamentals-exercises"></a>Azure AI Fundamentals 練習

這些實作練習是為了支援 [Microsoft Learn](https://docs.microsoft.com/training/) 上的訓練內容而設計。

您將需要 Microsoft Azure 訂用帳戶，以完成這些練習。 您可以在 [https://azure.microsoft.com](https://azure.microsoft.com) 註冊免費試用。

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Exercises |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
