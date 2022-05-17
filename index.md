---
title: 線上託管說明
permalink: index.html
layout: home
ms.openlocfilehash: b85af520a10e63a2f9a5696db03bfd946aff968f
ms.sourcegitcommit: 1ef64e3008a439d0d0bb3d93a27d3df68d3d64a9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/17/2022
ms.locfileid: "140688689"
---
# <a name="azure-ai-fundamentals-exercises"></a>Azure AI Fundamentals 練習

請使用下列連結完成 Microsoft 課程 [AI-900 *Microsoft Azure AI 基本概念*](https://docs.microsoft.com/learn/certifications/courses/ai-900t00)的實作教室練習。

您將需要 Microsoft Azure 訂用帳戶，以完成這些練習。 若您的講師沒有為您提供 Microsoft Azure 訂閱，您可以在 [https://azure.microsoft.com](https://azure.microsoft.com) 註冊免費試用版。

{% assign labs = site.pages | where_exp:"page", "page.url contains '/instructions'" %}
| Exercises |
| ------- | 
{% for activity in labs  %}| [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
