---
lab:
  title: 使用 Bing Copilot 探索 owed AI
---

在此練習中，您將探索 Bing Copilot 的 AI。 

## 開始之前
您需要個人 Microsoft 帳戶。 如果您沒有帳戶，請移至 [signup.live.com](https://signup.live.com/signup?azure-portal=true) 註冊。

# 使用 Bing 探索 AI

1. 開啟 [Bing.com](https://www.bing.com?azure-portal=true) 並使用您的個人 Microsoft 帳戶登入。

**注意**：雖然您可以使用公司或學校帳戶登入，但相較于使用您的個人帳戶登入，您會看到稍微不同的使用者體驗。 使用公司或學校帳戶，您會看到 Bing 企業聊天。 

1. 從畫面頂端的功能表中選取 **[聊天** ]。 聊天會帶您前往 Bing Copilot，其使用 ability AI 來提供搜尋結果。 這表示，不同于單獨傳回現有內容的搜尋，Bing Copilot 可以根據自然語言模型化和 Web 的資訊來組合新的回應。  
    
1. 在畫面底部，您會看到視窗 **詢問我任何專案**。 當您在視窗中輸入提示時，Bing Copilot 會使用整個交談執行緒來傳迴響應。 例如，讓我們嘗試詢問一系列有關旅遊的問題。 

## 使用提示產生回應

1. 在提示字元中輸入： `What are 3 pros and cons of traveling in the winter?` 。 您會看到 *[搜尋：...]* 和 [ *產生...]* 出現在回應之前。 模型會使用搜尋的回應作為基礎資訊來產生原始回應。 請注意，回應結尾包含其來源的連結。 

![Bing copilot 回應的螢幕擷取畫面，其中具有三個專案符號的優缺點，以及三個專案符號。](../media/generative-ai/bing-copilot-response-traveling.png) 

**注意**：如果您看不到 **產生...* 訊息或專案符號清單回應，則尚未看到 Bing Copilot 運作中。 您必須返回登入功能表，並連接您搭配個人帳戶使用的目前帳戶。 
 
1. 在提示字元中輸入： `Find me 3 more pros` 。 這則提示的意義在於，您想要看到 3 個更正面的原因，表示在尚未列出的雪地中旅遊。 請注意，在此提示中，您會要求 Bing Copilot 執行兩個單獨搜尋不會執行的動作：使用先前的聊天回應來排除新回應中傳回的內容，並使用先前聊天的主題，而不明確指出它。 

1. 在提示字元中輸入： `Where are 3 places I can go to find fewer crowds?` 。 

**注意**：請注意，雖然 Bing Copilot 能夠提供相關的回應，但是它可以在繼續時卸載先前交談執行緒的「記憶」。 因此，您取得的回應可能不會直接與在雪地旅行有關。 這主要是使用權杖輸入限制。 當交談的先前部分聊天「記住」時，這是因為其已從交談中儲存特定數量的權杖。 隨著新權杖透過您的新提示和回應引進，聊天會讓舊權杖繼續。 

1. 聊天視窗旁的 [ **新增主題** ] 按鈕很有用 Bing Copilot 可清除先前的對話對話，因此您的新主題回應不會以上一個主題為基礎。 使用聊天視窗旁的 [ **新增主題** ] 圖示來清除您的訊息歷程記錄。 

## 嘗試產生映射

1. 現在讓我們看看影像產生範例。 在提示字元中輸入： `Create an image of an elephant eating a hamburger` 。 請注意，我在 Bing Copilot 傳迴響應之前， *會嘗試建立...* 的訊息。 

![擷取漢堡的動物螢幕擷取畫面。](../media/generative-ai/dall-e-elephant.png)

請務必注意，回應看起來可能類似，但不同。 這是因為回應會有所不同。  

1. 在回應中，底部有文字會讀取「由 DALL-E 提供電源」。 請考慮 DALL-E 如何以大型語言模型為基礎，因為您的自然語言輸入會產生影像。 

1. 按一下畫面右上角的 Microsoft Bing 圖示，返回 Bing Copilot 的聊天。 

## 嘗試產生程式碼

1. 現在讓我們看看程式碼產生和翻譯的範例。 在提示字元中輸入： `Use Python to create a list` 。 

1. 在提示字元中輸入： `Translate that into C#` 。 請注意，您不需要指定「該」是什麼，因為 Bing Copilot 知道參考交談歷程記錄。 

## Bonus 

1. 在提示字元中輸入： `What are 3 examples of generative AI helping people?` 。 您可以使用此方法作為一種腦力激蕩自己的主意！  

