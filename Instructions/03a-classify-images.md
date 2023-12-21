---
lab:
  title: 探索影像分類
---

# 探索影像分類

*Azure AI 視覺*服務提供了實用的預建模型來處理影像，但針對電腦視覺，您通常需要定型自己的模型。 例如，假設野生動物保護組織想要使用運動感應相機來追蹤動物的出沒。 然後，運用攝影機拍攝的影像來驗證特定區域存在特定物種，以便協助保護瀕危物種。 為達成此目的，該組織可受益於*影像分類*模型，因其經過訓練可從所擷取相片識別不同動物物種。

您可在 Azure 使用***自訂視覺***服務，根據現有影像來訓練影像分類模型。 建立影像分類解決方案有兩個要素。 首先，您必須訓練模型，以使用現有影像來辨識不同的類別。 然後，模型完成定型時，您必須將其發佈為服務以供應用程式使用。

為了測試自訂視覺服務的功能，我們會使用在 Cloud Shell 中執行的簡單命令列應用程式。 相同的原則與功能適用於現實世界的解決方案，例如網站或行動應用程式。

## 在您開始使用 Intune 之前

若要完成此實驗室，您將需要擁有管理存取權的 [Azure 訂用帳戶](https://azure.microsoft.com/free?azure-portal=true)。

## 建立 *Azure AI 服務*資源

您可以透過建立**自訂視覺**資源或 **Azure AI 服務**資源，以使用自訂視覺服務。

>**注意** 並非所有區域都有提供這些資源。 無論您建立的是自訂視覺資源或 Azure AI 服務資源，只有在[特定區域](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services)建立的資源才能用於存取自訂視覺服務。 為了簡單起見，以下設定指示會預先為您選取某個區域。

在 Azure 訂閱建立 **Azure AI 服務**資源。

1. 開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. 按一下 **＋建立資源 **按鈕並搜尋  * Azure AI 服務 *。 選取**建立** **Azure AI 服務**方案。 系統會帶您前往建立 Azure AI 服務資源的頁面。 使用下列設定對其進行設定：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：美國東部
    - **名稱**：*輸入唯一名稱*。
    - **定價層**:標準 S0
    - **核取此方塊表示我已閱讀並了解下列所有條款**：選取。

1. 檢閱並建立資源，然後等候部署完成。 接著，移至所部署的資源。

1. 檢視 Azure AI 服務資源的**金鑰與端點**頁面。 您需要有端點和金鑰，才能從用戶端應用程式連線。

## 建立自訂視覺專案

若要訓練物件偵測模型，您必須根據訓練資源來建立自訂視覺專案。 為此，您將使用自訂視覺入口網站。

1. 從 [https://aka.ms/animal-images](https://aka.ms/animal-images) 下載並擷取正在訓練的影像。 這些影像會以 zip 壓縮資料夾提供，此資料夾在解壓縮後會包含名為 **elephant**、**giraffe** 與 **lion** 的子資料夾。

1. 開啟新瀏覽器索引標籤，並瀏覽至自訂視覺入口網站 (位於 [https://customvision.ai](https://customvision.ai?azure-portal=true))。 如果出現提示，請使用與 Azure 訂用帳戶相關聯的 Microsoft 帳戶進行登入，並同意服務條款。

1. 在自訂視覺入口網站中，使用下列設定建立新的專案：

    - **名稱**：動物識別
    - **描述**：動物影像分類
    - **資源**：*您先前建立的 Azure AI 服務或自訂視覺資源*
    - **專案類型**：分類
    - **分類類型**：多類別 (每個影像一個標記)
    - **區域**：一般 \[A2]

1. 按一下 [新增影像]****，然後選取先前解壓縮的 **elephant** 資料夾中的所有檔案。 然後上傳影像檔，並指定 *elephant* 標籤，如下所示：

    ![影像上傳介面的螢幕擷取畫面。](media/create-image-classification-system/upload-elephants.png)

1. 使用 [新增影像]**** ([+]) 按鈕，上傳 **giraffe** 資料夾中帶有 *giraffe* 標記的影像，以及 **lion** 資料夾中帶有 *lion* 標記的影像。

1. 探索您在自訂視覺專案中上傳的影像 - 每個類別應該會有 17 個影像，如下所示：

    ![螢幕擷取畫面顯示自訂視覺入口網站已標記的定型影像。](media/create-image-classification-system/animal-training-images.png)

1. 在自訂視覺專案中，於影像上方按一下 [定型]**** 以使用已加上標籤的影像來定型分類模型。 選取 [快速定型]**** 選項，然後等候定型反覆項目完成。

    > **提示**：定型可能需要幾分鐘時間。 在等待時，請查看[雪豹自拍與 AI 如何協助拯救物種免於滅絕](https://news.microsoft.com/transform/snow-leopard-selfies-ai-save-species/)，其中描述真實專案使用電腦視覺來追蹤野生瀕危動物。

1. 當模型反覆項目已完成定型時，請檢閱*精確度*、*重新叫用率*和 *AP* 效能計量 - 這些計量會測量分類模型的預測精確度，而且值應該都很高。

## 測試模型

在發佈此模型反覆項目以供應用程式使用之前，請先進行測試。

1. 在效能計量上方，按一下 [快速測試]****。

1. 在 [影像 URL]**** 方塊，輸入 `https://aka.ms/giraffe` 並按一下 [快速測試影像 (➔)]**** 按鈕。

1. 檢視模型傳回的預測 - *giraffe* 的可能性分數應會最高，如下所示：

    ![快速測試介面的螢幕擷取畫面。](media/create-image-classification-system/quick-test.png)

1. 關閉 [快速測試]**** 視窗。

## 發佈影像分類模型

現在，您已準備好發佈已定型的模型，並從用戶端應用程式使用此模型。

1. 按一下 [&#128504; 發佈]****，使用下列設定發佈已定型的模型：
    - **模型名稱**：動物
    - **預測資源**：*您先前建立的 Azure AI 服務或自訂視覺預測資源*。

1. 發佈之後，按一下 [預測 URL]**(&#127760;) 圖示，以查看使用已發佈的模型所需的資訊。

    ![預測 URL 的螢幕擷取畫面。](media/create-image-classification-system/prediction-url.png)

之後，您需要適當的 URL 與 Prediction-Key 值，才能從影像 URL 取得預測，因此請讓此對話方塊保持開啟，並繼續進行下一個工作。

## 準備用戶端應用程式

為了測試自訂視覺服務的功能，我們會使用在 Azure 上的 Cloud Shell 中執行的簡單命令列應用程式。

1. 切換回包含 Azure 入口網站的瀏覽器標籤，然後選取頁面頂端搜尋方塊右側的 **Cloud shell** (**[>_]**) 按鈕。 這會在入口網站底部開啟 Cloud Shell 窗格。

    第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 如果是這樣，請選取 **PowerShell**。

    如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂閱，然後選取**建立儲存體**。 然後等候一分鐘左右，讓系統建立儲存體。

    當 Cloud Shell 就緒時，看起來應該會像這樣：
    
    ![Azure 入口網站 Cloud Shell 的螢幕擷取畫面。](media/create-image-classification-system/cloud-shell.png)

    > **提示**：請確定 Cloud Shell 窗格左上方所指出的殼層類型已切換為 *PowerShell*。 若其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    請注意，如需調整 Cloud Shell 的大小，您可以拖曳窗格頂端的分隔線，或者使用窗格右上方的 **&#8212;**、**&#9723;**、**X** 圖示，分別將窗格最小化、最大化或關閉窗格。 如需使用 Azure Cloud Shell 的詳細資訊，請參閱 [Azure Cloud Shell 文件](https://docs.microsoft.com/azure/cloud-shell/overview)。

2. 在命令殼層中，輸入下列命令來下載此練習的檔案，並將其儲存在名為 ** ai-900 ** 的資料夾中 (如果資料夾已經存在，則刪除該資料夾後)

    ```PowerShell
    rm -r ai-900 -f
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

3. 下載檔案之後，輸入下列命令以變更為 ** ai-900 ** 目錄，並編輯此練習的程式碼檔案：

    ```PowerShell
    cd ai-900
    code classify-image.ps1
    ```

    請注意此命令如何開啟編輯器，如下圖：

     ![Cloud Shell 中程式碼編輯器的螢幕擷取畫面。](media/create-image-classification-system/code-editor.png)

     > **提示**：您可以使用 Cloud Shell 命令列與程式碼編輯器之間的分隔線來調整窗格的大小。

4. 不用太過顧慮程式碼的細節。 重要的是，它以一些程式碼開頭來指定自訂視覺模型的預測 URL 與金鑰。 您需要更新這些，以便其餘程式碼使用您的模型。

    從自訂視覺專案的瀏覽器索引標籤開啟的對話方塊取得*預測 URL* 以及*預測金鑰*。 ***如果您有影像 URL*，則需要使用這些版本。**

    使用這些值來取代程式碼檔案中的 **YOUR_PREDICTION_URL** 及 **YOUR_PREDICTION_KEY** 預留位置。

    貼上預測 URL 與預測金鑰值之後，前兩行程式碼看起來應該類似這樣：

    ```PowerShell
    $predictionUrl="https..."
    $predictionKey ="1a2b3c4d5e6f7g8h9i0j...."
    ```

5. 對程式碼中的變數進行變更之後，請按 ** CTRL+S ** 儲存檔案。 然後按 **CTRL+Q** 關閉程式碼編輯器。

## 測試用戶端應用程式

現在您可以使用範例用戶端應用程式，根據其所包含的動物來分類影像。

1. 在 PowerShell 窗格中，輸入下列命令來執行程式碼：

    ```PowerShell
    ./classify-image.ps1 1
    ```

    此程式碼會使用您的模型來分類下列影像：

    ![長頸鹿的照片。](media/create-image-classification-system/animal-1.jpg)

1. 檢閱預測，值應該會是 **giraffe**。

1. 現在讓我們嘗試另一個影像。 執行此命令：

    ```PowerShell
    ./classify-image.ps1 2
    ```

    這次會分類下影像：

    ![大象的照片。](media/create-image-classification-system/animal-2.jpg)

1. 確認模型將此影像分類為 **elephant**。

1. 讓我們再試一張。 執行此命令：

    ```PowerShell
    ./classify-image.ps1 3
    ```

    完成的結果看起來如同此影像：

    ![獅子的照片。](media/create-image-classification-system/animal-3.jpg)

1. 確認模型將此影像分類為 **lion**。

如無意外，您的影像分類模型已正確分類這三張影像。


