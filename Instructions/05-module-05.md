---
lab:
  title: 使用 Bing Copilot 探索產生的 AI
---

在此練習中，您將探索使用 Bing Copilot 的生成 AI。 

## 在您開始使用 Intune 之前
您需要個人 Microsoft 帳戶。 如果您沒有帳戶，請移至 [signup.live.com](https://signup.live.com/signup?azure-portal=true) 註冊。

# 使用 Bing 探索產生的 AI

1. 開啟 [Bing.com](https://www.bing.com?azure-portal=true) 並使用您的個人 Microsoft 帳戶登入。

**注意**：雖然您可以使用公司或學校帳戶登入，但相較於使用個人帳戶登入，您會看到略有不同的用戶體驗。 使用您的公司或學校帳戶，您會看到 Bing 企業聊天。 

1. 從畫面頂端的功能表中選取 **[聊天** ]。 聊天會帶您前往 Bing Copilot，其使用產生 AI 來提供搜尋結果。 這表示，與單獨傳回現有內容的搜尋不同，Bing Copilot 可以根據自然語言模型化和 Web 的資訊來結合新的回應。  
    
1. 在畫面底部，您會看到窗口 **詢問我任何專案**。 當您在視窗中輸入提示時，Bing Copilot 會使用整個對話線程來傳回回應。 例如，讓我們嘗試詢問一系列關於旅行的問題。 

## 使用提示來產生回應

1. 在提示中輸入： `What are 3 pros and cons of traveling in the winter?`。 您會在回應之前看到 [ *搜尋：...* ] 和 *[產生...* ]。 此模型會使用搜尋的回應作為基礎資訊來產生原始回應。 請注意，回應結尾包含其來源的連結。 

![Bing 警察回應旅行提示的螢幕快照，其中包含三個專案符號的優缺點和三個項目符號。](../media/generative-ai/bing-copilot-response-traveling.png) 

**注意**：如果您看不到 **產生...* 訊息或項目符號列表回應，則尚未看到 Bing Copilot 運作。 您必須返回登入功能表，並連接您搭配個人帳戶使用的目前帳戶。 
 
1. 在提示中輸入： `Find me 3 more pros`。 您對於這個提示的意義在於，您想要在尚未列出的冬季旅行看到 3 個更積極的原因。 請注意，使用此提示時，您會要求 Bing Copilot 執行兩項單獨搜尋不會執行的工作：使用先前的聊天回應來排除新回應中傳回的內容，並使用先前聊天的主題，而不明確指出。 

1. 在提示中輸入： `Where are 3 places I can go to find fewer crowds?`。 

**注意**：請注意，雖然 Bing Copilot 能夠提供相關回應，但是它可以在繼續時卸除先前交談線程的「記憶」。 因此，您得到的回應可能不會與冬季旅行直接相關。 這主要是與令牌輸入限制搭配使用。 當交談的早期部分聊天「記住」時，這是因為它已從交談中儲存了一定數量的令牌。 隨著新令牌透過新的提示和響應引進，聊天會放開較舊的令牌。 

1. 聊天視窗旁的 [ **新增主題** ] 按鈕會很有用 Bing Copilot 來清除先前的對話對話，因此您的新主題回應不會以上一個主題為基礎。 使用聊天視窗旁的 [ **新增主題** ] 圖示來清除您的訊息歷程記錄。 

## 嘗試產生映像

1. 現在讓我們看看影像產生範例。 在提示中輸入： `Create an image of an elephant eating a hamburger`。 請注意，我會嘗試建立...* 的訊息*會出現在 Bing Copilot 傳回回應之前。 

![大象吃火腿漢堡的螢幕快照。](../media/generative-ai/dall-e-elephant.png)

重要的是，請注意回應看起來可能類似，但不相同。 這是因為回應會有所不同。  

1. 在回應中，底部有文字會讀取「由 DALL-E 提供電源」。 請考慮 DALL-E 如何以大型語言模型為基礎，因為您的自然語言輸入會產生影像。 

1. 按兩下畫面右上角的 Microsoft Bing 圖示，返回 Bing 的聊天。 

## 嘗試產生程序代碼

1. 現在讓我們看看程式代碼產生和翻譯的範例。 在提示中輸入： `Use Python to create a list`。 

1. 在提示中輸入： `Translate that into C#`。 請注意，您不需要指定 Bing Copilot 參考交談歷程記錄時所知道的「那」是什麼。 

## Bonus 

1. 在提示中輸入： `What are 3 examples of generative AI helping people?`。 您可以使用這種方式來集思廣益！  

