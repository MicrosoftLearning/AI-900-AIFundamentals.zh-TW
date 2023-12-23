---
lab:
  title: 探索 Content Safety Studio
---

Azure AI 服務可協助使用者使用現成、預先建置且可自訂的 API 與模型來建立 AI 應用程式。 在此練習，您會在 Content Safety Studio 查看其中一項服務 Azure AI 內容安全。 

Content Safety Studio 可讓您探索如何仲裁文字與影像內容。 您可針對範例文字或影像執行測試，並取得每個類別的嚴重性分數，範圍從安全到高。 在此實驗室練習，您會在 Content Safety Studio 建立單一服務資源，並測試其功能。 

> **注意** 本練習的目標是要大致瞭解 Azure AI 服務的佈建和使用方式。 內容安全僅作為範例，但並不要求您透過此練習獲得有關內容安全的全面知識！

## 瀏覽 Content Safety Studio 

![Content Safety Studio 登陸頁面的螢幕擷取畫面。](./media/content-safety/content-safety-getting-started.png)


1. 開啟 [Content Safety Studio][](https://contentsafety.cognitive.azure.com?azure-portal=true)。 如果您尚未登入，則必須登入。 選取畫面右上角的 [登入]****。 使用與您的 Azure 訂用帳戶相關聯的電子郵件與密碼來登入。 

1. Content Safety Studio 的設定方式如同 Azure AI 服務的其他許多工作室。 在畫面頂端的功能表，按一下 *Azure AI* 左側的圖示。 您會看到其他工作室的下拉式清單，這些工作室專為使用 Azure AI 服務進行開發而設計。 再次按一下圖示即可隱藏清單。

![Content Safety Studio 功能表的螢幕擷取畫面，其中切換選取已開啟以便切換至其他 Studio。](./media/content-safety/studio-toggle-icon.png)  

## 將資源與 Studio 產生關聯 

使用 Studio 之前，您必須關聯 Azure AI 服務資源與 Studio。 視工作室而定，您可能會發現您需要特定單一服務資源，或使用一般多服務資源。 針對 Content Safety Studio，您可建立單一服務*內容安全*資源或 *Azure AI 服務*一般多服務資源，來使用服務。 在下列步驟，我們將建立單一服務內容安全資源。 

1. 在畫面右上方，按一下 [設定]**** 圖示。 

![螢幕擷取畫面：設定圖示顯示於畫面右上方，在鈴鐺、問號與微笑圖示旁邊。](./media/content-safety/settings-toggle.png)

1. 在 [設定]**** 頁面，您會看到 [目錄]** 索引標籤與 [資源]** 索引標籤。在 [資源]** 索引標籤，選取 [建立新資源]****。 這會帶您前往頁面以便在 Azure 入口網站建立資源。

> **注意** [目錄]** 索引標籤可讓使用者選取不同目錄並用以建立資源。 除非您要使用不同目錄，否則不需變更其設定。 

![螢幕擷取畫面：從 Content Safety Studio 的 [設定] 頁面選取 [建立新資源]。](./media/content-safety/create-new-resource-from-studio.png)

1. 在 [Azure 入口網站][](https://portal.azure.com?auzre-portal=true) 的 [建立內容安全]** 頁面，您必須設定數個詳細資料來建立資源。 使用下列設定對其進行設定：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：選擇任何可用的區域**。
    - **名稱**：*輸入唯一名稱*。
    - **定價層**：免費 F0

1. 選取 [檢閱 + 建立]****，然後檢閱設定。 然後選取**建立**。 畫面會指出部署完成的時間。 

*恭喜！您剛建立或佈建 Azure AI 服務資源。您特別佈建的內容是單一服務內容安全服務資源。*

1. 當部署完成時，請開啟新索引標籤，並返回 [Content Safety Studio][](https://contentsafety.cognitive.azure.com?azure-portal=true)。 

1. 請再次選取畫面右上角的 [設定]**** 圖示 這次您應會看到新建立的資源已新增至清單。  

1. 在 Content Safety Studio 的 [設定] 頁面，選取您剛才建立的 [Azure AI 服務資源]，然後按一下畫面底部的 [使用資源]****。 您將回到 Studio 首頁。 現在您可開始搭配新建立的資源使用工作室。

## 在 Content Safety Studio 試用文字仲裁

1. 在 Content Safety Studio 首頁的 [執行仲裁測試]** 底下，瀏覽至 [仲裁文字內容]**** 方塊，然後按一下 [試用]****。
1. 在 [執行簡單測試] 下，按一下 [安全內容]****。 請注意，文字會顯示於下方方塊。 
1. 按一下 [執行測試]****。 執行測試會呼叫 Content Safety Service 的深度學習模型。 深度學習模型已經過定型，可辨識不安全內容。
1. 在 [結果]** 面板檢查結果。 有四種嚴重性層級，從安全到高，以及四種有害內容類型。 內容安全 AI 服務是否認為此範例可接受？ 請務必注意的是，結果在信賴區間內。 訓練良好的模型 (例如 Azure AI 的現成模型之一) 所傳回的結果具高度機率符合人類標記結果。 每次執行測試時，您都會再次呼叫模型。 
1. 現在請嘗試另一範例。 選取 [拼字錯誤的暴力內容] 底下的文字。 檢查內容是否顯示於下方方塊。
1. 按一下 [執行測試]****，然後在 [結果] 面板再次檢查結果。 

您可針對提供的所有範例執行測試，然後檢查結果。

## 查看金鑰與端點

您測試的這些功能可設計成各種應用程式。 您可在 Content Safety Studio 與 Azure 入口網站找到用於應用程式開發的金鑰與端點。 

1. 在 Content Safety Studio，瀏覽回 [設定]**** 頁面，並選取 [資源]** 索引標籤。 尋找您所使用的資源。 捲動以查看資源的端點與金鑰。 
1. 在 Azure 入口網站，您會針對資源看到這些*相同*端點，但*不同*金鑰。 若要查看，請前往 [Azure 入口網站][](https://portal.azure.com?auzre-portal=true)。 在頂端搜尋列，搜尋 [內容安全]**。 尋找您的資源，然後按一下。 在左側功能表，查看 [資源管理]** 下的 [金鑰與端點]**。 選取 [金鑰與端點]****，並檢視資源的端點與金鑰。 

在完成之後，您可從 Azure 入口網站刪除內容安全資源。 由於當資源存在訂用帳戶時會累算成本，因此刪除資源可降低成本。 若要這樣做，請瀏覽至內容安全資源的 [概觀]**** 頁面。 選取畫面頂端的 [部署]****。 
