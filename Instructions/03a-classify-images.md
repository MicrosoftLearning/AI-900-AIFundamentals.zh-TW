---
lab:
  title: 探索影像分類
---

# 探索影像分類

*Azure AI 視覺*服務提供實用的預先建置模型來處理影像，但您通常需要定型自己的電腦視覺模型。 例如，假設有一個動物動物組織想要使用動作敏感相機來追蹤動物的視覺。 接著，相機所擷取的影像可用來驗證特定區域中的特定物種是否存在，並協助對物種進行動物的海洋工作。 為了達成此目的，組織會受益于經過訓練的 *影像分類* 模型，以識別所擷取相片中的不同動物物種。

在 Azure 中，您可以使用***自訂視覺***服務，根據現有的影像來定型影像分類模型。 建立影像分類解決方案有兩個要素。 首先，您必須訓練模型，以使用現有影像來辨識不同的類別。 然後，模型完成定型時，您必須將其發佈為服務以供應用程式使用。

為了測試自訂視覺服務的功能，我們會使用在 Cloud Shell 中執行的簡單命令列應用程式。 相同的原則和功能適用于真實世界的解決方案，例如網站或行動裝置應用程式。

## 開始之前

若要完成此實驗室，您將需要擁有管理存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free?azure-portal=true)。

## 建立 *Azure AI 服務* 資源

您可以建立自訂視覺資源或**Azure AI 服務**資源，以使用**自訂視覺**服務。

>**注意** 並非所有區域都有提供這些資源。 不論您建立自訂視覺還是 Azure AI 服務資源，只有[在特定區域中](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services)建立的資源可用來存取自訂視覺服務。 為了簡單起見，以下設定指示會預先為您選取某個區域。

在 Azure 訂用帳戶中建立 **Azure AI 服務** 資源。

1. 開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. 按一下 ** [&#65291;[建立資源]** 按鈕，然後搜尋 *Azure AI 服務*。 選取 **[建立** **Azure AI 服務** 方案]。 系統會帶您前往頁面來建立 Azure AI 服務資源。 使用下列設定進行設定：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：美國東部
    - **名稱**：輸入唯一名稱。
    - **定價層**:標準 S0
    - **核取此方塊表示我已閱讀並了解下列所有條款**：選取。

1. 檢閱並建立資源，然後等候部署完成。 接著，移至所部署的資源。

1. 檢視 Azure AI 服務資源的 **[金鑰和端點]** 頁面。 您需要有端點和金鑰，才能從用戶端應用程式連線。

## 建立自訂視覺專案

若要訓練物件偵測模型，您必須根據訓練資源來建立自訂視覺專案。 若要這樣做，您要使用自訂視覺入口網站。

1. 從 [https://aka.ms/animal-images](https://aka.ms/animal-images) 下載並擷取定型影像。 這些影像會提供于壓縮的資料夾中，當擷取時，其**包含稱為子**資料夾、**擷取器及****動物**。

1. 開啟新的瀏覽器索引標籤，然後流覽至位於 的 自訂視覺 入口網站 [https://customvision.ai](https://customvision.ai?azure-portal=true) 。 如果出現提示，請使用與 Azure 訂用帳戶相關聯的 Microsoft 帳戶進行登入，並同意服務條款。

1. 在自訂視覺入口網站中，使用下列設定建立新的專案：

    - **名稱**：動物識別
    - **描述**：動物的影像分類
    - **資源**：*您先前建立的 Azure AI 服務或自訂視覺資源*
    - **專案類型**：分類
    - **分類類型**：多類別 (每個影像一個標記)
    - **網域**：一般 \[ A2]

1. 按一下 **[新增影像**]，然後選取您先前擷取之擷取之 **資料夾中** 的所有檔案。 然後上傳影像檔案，並指定標記 *，* 如下所示：

    ![影像上傳介面的螢幕擷取畫面。](media/create-image-classification-system/upload-elephants.png)

1. 使用 [**新增影像** ([+]) 按鈕，將影像上傳至具有*標籤* ** ( 標籤的 ) **資料夾中的影像，以及具有標籤*標籤*的 **) **資料夾中的影像。

1. 探索您在自訂視覺專案中上傳的影像 - 每個類別應該有 17 個影像，如下所示：

    ![自訂視覺入口網站中標記訓練影像的螢幕擷取畫面。](media/create-image-classification-system/animal-training-images.png)

1. 在自訂視覺專案中，影像的上方，按一下 [訓練] 以使用已標記的影像訓練分類模型。 選取 [ **快速訓練]** 選項，然後等候定型反復專案完成。

    > **提示**：訓練可能需要幾分鐘的時間。 當您在等候時，請查看 [雪地動物自我和 AI 如何協助儲存物種，](https://news.microsoft.com/transform/snow-leopard-selfies-ai-save-species/)其描述使用電腦視覺來追蹤動物在動物中的真實專案。

1. 當模型反覆項目已完成定型時，請檢閱*精確度*、*重新叫用率*和 *AP* 效能計量 - 這些計量會測量分類模型的預測精確度，而且值應該都很高。

## 測試模型

在發佈此模型反覆項目以供應用程式使用之前，請先進行測試。

1. 在效能計量上方，按一下 [快速測試]。

1. 在 [ **影像 URL]** 方塊中，輸入 `https://aka.ms/giraffe` 並按一下 **快速測試影像 (&#10132;) ** 按鈕。

1. 檢視模型所傳回的預測 - *網底的* 機率分數應為最高，如下所示：

    ![快速測試介面的螢幕擷取畫面。](media/create-image-classification-system/quick-test.png)

1. 關閉 [快速測試] 視窗。

## 發佈影像分類模型

現在，您已準備好發佈已定型的模型，並從用戶端應用程式使用此模型。

1. 按一下 [&#128504; 發佈]，使用下列設定發佈已定型的模型：
    - **模型名稱**：動物
    - **預測資源**：*您先前建立的 Azure AI 服務或自訂視覺預測資源*。

1. 發佈之後，按一下 [預測 URL](&#127760;) 圖示，以查看使用已發佈的模型所需的資訊。

    ![預測 URL 的螢幕擷取畫面。](media/create-image-classification-system/prediction-url.png)

之後，您需要適當的 URL 與 Prediction-Key 值，才能從影像 URL 取得預測，因此請讓此對話方塊保持開啟，並繼續進行下一個工作。

## 準備用戶端應用程式

為了測試自訂視覺服務的功能，我們將使用在 Azure 上 Cloud Shell 中執行的簡單命令列應用程式。

1. 切換回包含Azure 入口網站的瀏覽器索引標籤，然後選取搜尋方塊右邊頁面頂端的 (**[****>_]**) 按鈕。 這會開啟入口網站底部的 Cloud Shell 窗格。

    第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 如果是，請選取 **[PowerShell**]。

    如果系統提示您為Cloud Shell建立儲存體，請確定已選取您的訂用帳戶，然後選取 [**建立儲存體**]。 接著請等候一分鐘左右，讓系統建立儲存體。

    當 Cloud Shell 就緒時，它看起來應該會像這樣：
    
    ![Azure 入口網站中 Cloud Shell 的螢幕擷取畫面。](media/create-image-classification-system/cloud-shell.png)

    > **提示**：確定Cloud Shell窗格左上方所指出的殼層類型為*PowerShell*。 如果其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    請注意，如需調整 Cloud Shell 的大小，您可以拖曳窗格頂端的分隔線，或者使用窗格右上方的 **&#8212;** 、 **&#9723;** 、**X** 圖示，分別將窗格最小化、最大化或關閉窗格。 如需使用 Azure Cloud Shell 的詳細資訊，請參閱 [Azure Cloud Shell 文件](https://docs.microsoft.com/azure/cloud-shell/overview)。

2. 在命令殼層中，輸入下列命令來下載此練習的檔案，並在移除該資料夾之後，將其儲存在名為 **ai-900** (的資料夾中，如果該資料夾已經存在) 

    ```PowerShell
    rm -r ai-900 -f
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

3. 下載檔案之後，輸入下列命令以變更為 **ai-900** 目錄，並編輯此練習的程式碼檔案：

    ```PowerShell
    cd ai-900
    code classify-image.ps1
    ```

    請注意，這會如何開啟編輯器，就像下圖中的編輯器一樣：

     ![Cloud Shell 中程式碼編輯器的螢幕擷取畫面。](media/create-image-classification-system/code-editor.png)

     > **提示**：您可以使用 Cloud Shell 命令列與程式碼編輯器之間的分隔符號列來調整窗格的大小。

4. 不用太過顧慮程式碼的細節。 重要的是，它會從一些程式碼開始，以指定自訂視覺模型的預測 URL 和金鑰。 您必須更新這些專案，讓程式碼的其餘部分使用您的模型。

    從您在自訂視覺專案的瀏覽器索引標籤中開啟的對話方塊，取得*預測 URL*和*預測金鑰*。 ***如果您有映射 URL*，則需要使用的版本。**

    使用這些值來取代 **程式** 代碼檔案中的 **YOUR_PREDICTION_URL和YOUR_PREDICTION_KEY** 預留位置。

    貼上預測 URL 與預測金鑰值之後，前兩行程式碼看起來應該類似這樣：

    ```PowerShell
    $predictionUrl="https..."
    $predictionKey ="1a2b3c4d5e6f7g8h9i0j...."
    ```

5. 對程式碼中的變數進行變更之後，請按 **CTRL+S** 儲存檔案。 然後按 **CTRL+Q** 以關閉程式碼編輯器。

## 測試用戶端應用程式

現在，您可以使用範例用戶端應用程式，根據它們所包含的動物來分類影像。

1. 在 PowerShell 窗格中，輸入下列命令來執行程式碼：

    ```PowerShell
    ./classify-image.ps1 1
    ```

    此程式碼會使用您的模型來分類下列影像：

    ![手部的相片。](media/create-image-classification-system/animal-1.jpg)

1. 檢閱應 **為親和的**預測。

1. 現在讓我們嘗試另一個影像。 執行此命令：

    ```PowerShell
    ./classify-image.ps1 2
    ```

    這次會分類下圖：

    ![動物的相片。](media/create-image-classification-system/animal-2.jpg)

1. 確認模型將此影像分類為 **動物**。

1. 讓我們再試一次。 執行此命令：

    ```PowerShell
    ./classify-image.ps1 3
    ```

    最終影像看起來像這樣：

    ![耙耙的相片。](media/create-image-classification-system/animal-3.jpg)

1. 確認模型將此影像分類為 **耙耙**。

希望您的影像分類模型已正確分類這三個影像。


