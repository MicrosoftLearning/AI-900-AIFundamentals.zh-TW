---
lab:
  title: 探索語言理解
---

# 探索語言理解

> **注意** 若要完成此實驗室，您需要一個具備[系統管理存取權](https://azure.microsoft.com/free?azure-portal=true)的 Azure 訂用帳戶。

我們日漸期待電腦能夠使用 AI，以便理解口說或打字輸入的自然語言命令。 例如，您可以實作家庭自動化系統，以便能夠使用「switch on the light」或「put the fan on」之類的語音命令來控制家中的裝置，並讓具有 AI 功能的裝置理解命令並採取適當的動作。

為了測試交談語言理解服務的功能，我們會使用在 Cloud Shell 中執行的命令列應用程式。 真實世界的解決方案也適用相同準則與功能，例如網站或手機應用程式。

## 建立「語言服務」** 資源

您可以藉由建立**語言服務**資源來使用交談語言理解服務。

如果您尚未建立此資源，請在 Azure 訂用帳戶中建立**語言服務**資源。

1. 在另一個瀏覽器索引標籤中，開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. 按一下 [&#65291;建立資源]**** 按鈕，搜尋「語言服務」**，然後使用下列設定建立**語言服務**資源：
    - 選取其他功能：*保留預設功能，然後按一下 [繼續] 以建立您的資源*  
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：美國東部 2
    - **名稱**：*輸入唯一名稱*。
    - **定價層**：S (每分鐘 1K 次呼叫)
    - **核取此方塊表示我確認已檢閱並認同「負責任 AI 注意事項」中的條款。**：選取。

1. 檢閱並建立資源，然後等候部署完成。

### 建立交談語言理解應用程式

若要實作自然語言理解與交談語言理解，請建立應用程式；然後新增實體、意圖和表達來定義您想要應用程式執行的命令。

1. 在新的瀏覽器索引標籤中，開啟位於 [https://language.azure.com](https://language.azure.com?azure-portal=true) 的 Language Studio 入口網站，然後使用與您的 Azure 訂用帳戶相關聯的 Microsoft 帳戶登入。

1. 若系統提示您選擇語言資源，請選取下列設定：
    - **Azure 目錄**：包含您訂用帳戶的 Azure 目錄。
    - **Azure 訂用帳戶**：您的 Azure 訂用帳戶。
    - **語言資源**：您先前建立的語言資源。

    >**提示** 如果「未」****** 提示您選擇語言資源，可能是因為您的訂用帳戶中有多個語言資源；在此情況下：
    >1. 在分頁頂端的列上，按一下 [設定 (&#9881;)] **** 按鈕。
    >1. 在 [設定]**** 分頁上，檢視 [資源]**** 索引標籤。
    >1. 選取您的語言資源，並按一下 [切換資源]****。
    >1. 在頁面頂端，按一下 [Language Studio]**** 以回到 Language Studio 首頁。

1. 在入口網站頂端的 [新建] **** 功能表中，選取 [交談語言理解] ****。

1. 在 [建立專案]**** 對話方塊的 [輸入基本資訊]**** 頁面上，輸入下列詳細資料，然後按 [下一步]****：
    - **名稱**：*建立唯一的名稱*
    - **描述**：簡單家庭自動化
    - **表達主要語言**：英文
    - **在專案中啟用多種語言**：*請勿選取*

    ![輸入專案的詳細資料。](media/conversational-language-understanding/create-project.png)

    >**提示** 請記下您的「專案名稱」**，稍後會用到。

1. 在 [檢閱和完成] ** 頁面上，按一下 [建立]****。

### 建立意圖、表達和實體

*意圖*是您想要執行的動作 - 例如，您可以開燈或關閉風扇。 在此情況下，您會定義兩個意圖：一個用來開啟裝置，另一個用來關閉裝置。 針對每個意圖，您會指定*表達*範例，以指出用來表示意圖的語言種類。

1. 在 [結構描述定義]**** 窗格中，確定已選取 [意圖]****。接著，按一下 [新增]****、新增名稱為 **switch_on** (小寫) 的意圖，然後按一下 [新增意圖]****。

    ![在 [建置結構描述] 窗格的 [意圖] 下按一下 [新增]。](media/conversational-language-understanding/build-schema.png)
    ![新增 switch_on 意圖，然後選取 [新增意圖]。](media/conversational-language-understanding/add-intent.png)

1. 選取 [switch_on]**** 意圖。 其會帶您前往 [資料標籤]**** 頁面。 在 [意圖]**** 下拉式清單中，選取 [switch_on]****。 在 [switch_on]**** 意圖旁邊，輸入表達 ***turn the light on***，然後按 **Enter** 鍵將此表達提交至清單。

    ![在 [表達] 下輸入 "turn the light on"，以將表達新增至定型集。](media/conversational-language-understanding/add-utterance-on.png)

1. 語言服務需要每個意圖至少有五個不同的表達範例，才能充分為語言模型定型。 為 [switch_on]**** 意圖再新增五個表達範例：  
    - ***switch on the fan***
    - ***put the fan on***
    - ***put the light on***
    - ***switch on the light***
    - ***turn the fan on***

1. 在畫面右側的 [為要定型的實體加上標籤]**** 窗格上，選取 [加標籤]****，然後選取 [新增實體]****。 輸入**裝置**、選取 [清單]****，然後選取 [新增實體]****。

    ![在 [標記要定型的實體] 面板上選取 [標記] 來新增實體，然後選取 [新增實體]。](media/conversational-language-understanding/add-entity.png) 
    ![在 [實體] 下輸入 device 並選取 [清單]，然後選取 [新增實體]。](media/conversational-language-understanding/add-entity-device.png)

1. 在 ***turn the fan on*** 表達中，醒目提示「fan」一字。 然後在出現的清單中，於 [搜尋實體]** 方塊中選取 [裝置]****。

    ![在表達中反白 fan 這個字，並選取 device。](media/conversational-language-understanding/switch-on-entity.png)

1. 對所有表達執行相同的動作。 使用 [裝置]**** 實體為其餘的 *fan* 或 *light* 表達加上標籤。 完成時，請確認您有下列表達，並務必要選取 [儲存變更]****：

    | **意圖** | **表達** | **實體** |
    | --------------- | ------------------ | ------------------ |
    | switch_on   | Put on the fan      | 裝置 - *選取 fan* |
    | switch_on   | Put on the light    | 裝置 - *選取 light* |
    | switch_on   | Switch on the light | 裝置 - *選取 light* |
    | switch_on   | Turn the fan on     | 裝置 - *選取 fan* |
    | switch_on   | Switch on the fan   | 裝置 - *選取 fan* |
    | switch_on   | Turn the light on   | 裝置 - *選取 light* |

    ![完成後，選取 [儲存變更]。](media/conversational-language-understanding/save-changes.png) 

1. 在左側窗格中，按一下 [結構描述定義]****，並確認您的 **switch_on** 意圖已列出。 然後按一下 [新增]****，並新增名稱為 **switch_off** (小寫) 的新意圖。

    ![返回 [建置結構描述] 畫面，並新增 switch_off 意圖。](media/conversational-language-understanding/add-switch-off.png) 

1. 按一下 [switch_off]**** 意圖。 其會帶您前往 [資料標籤]**** 頁面。 在 [意圖]**** 下拉式清單中，選取 [switch_off]****。 在 [switch_off]**** 意圖旁邊，新增表達 ***turn the light off***。

1. 為 [switch_off]**** 意圖再新增五個表達範例。
    - ***switch off the fan***
    - ***put the fan off***
    - ***put the light off***
    - ***turn off the light***
    - ***switch the fan off***

1. 使用 [裝置]**** 實體為 *light* 或 *fan* 一字加上標籤。 完成時，請確認您有下列表達，並務必要選取 [儲存變更]****：  

    | **意圖** | **表達** | **實體** | 
    | --------------- | ------------------ | ------------------ |
    | switch_off   | Put the fan off    | 裝置 - *選取 fan* | 
    | switch_off   | Put the light off  | 裝置 - *選取 light* |
    | switch_off   | Turn off the light | 裝置 - *選取 light* |
    | switch_off   | Switch the fan off | 裝置 - *選取 fan* |
    | switch_off   | Switch off the fan | 裝置 - *選取 fan* |
    | switch_off   | Turn the light off | 裝置 - *選取 light* |

### 定型模型

現在，您已準備好使用所定義的意圖和實體來為應用程式的交談語言模型定型。

1. 在 Language Studio 的左側，選取 [定型作業]****，然後選取 [啟動定型作業]****。 使用下列設定： 
    - **為新模型定型**：*已選取並選擇模型名稱*
    - **定型模式**：標準定型 (免費)
    - **資料分割**：*選取自動從定型資料分割測試集，保留預設百分比*
    - 按一下頁面底部的 [定型]****。

1. 等候定型完成。 

### 部署和測試模型

若要在用戶端應用程式中使用所定型的模型，您必須將其部署為端點，以供用戶端應用程式傳送新表達到其中；以及從中預測意圖和實體。

1. 在 Language Studio 左側，按一下 [部署模型]****。

1. 選取您的模型名稱，然後按一下 [新增部署]****。 使用下列設定：
    - **建立或選取現有的部署名稱**：選擇建立新的部署名稱。新增唯一名稱**。
    - **將已定型的模型指派給您的部署名稱**：選取已定型模型的名稱**。
    - 按一下 [部署]****

    >**提示** 請記下您的「部署名稱」**，稍後會用到。 

1. 模型部署完成時，按一下頁面左側的 [測試部署]****，然後在 [部署名稱]**** 下選取已部署的模型。

1. 輸入下列文字，然後選取 [執行測試]****：

    *switch the light on*

    ![選取已部署的模型來測試模型，然後輸入文字並選取 [執行測試]。](media/conversational-language-understanding/test-model.png) 

    檢閱傳回的結果，注意其包含預測的意圖 (應該是 **switch_on**) 和預測的實體 (**裝置**)，並有信賴分數指出模型針對預測的意圖和實體所計算出的可能性。 [JSON] 索引標籤會顯示每個可能意圖的比較信賴度 (信賴分數最高的意圖就是預測的意圖)

1. 在 [輸入您自己的文字，或上傳文字文件]** 下，清除文字方塊並使用下列表達來測試模型：
    - *turn off the fan*
    - *put the light on*
    - *put the fan off*

## 執行 Cloud Shell

現在讓我們試用已部署的模型。 為了試用，我們會使用在 Azure 上的 Cloud Shell 中執行的命令列應用程式。 

1. 讓 Language Studio 的瀏覽器索引標籤保持開啟，切換回包含 Azure 入口網站的瀏覽器索引標籤。

1. 在 Azure 入口網站中，選取頁面頂端在搜尋方塊右邊的 **[>_]** (Cloud Shell**) 按鈕。 按一下此按鈕會在入口網站底部開啟 Cloud Shell 窗格。

    ![按一下頂端搜尋方塊右側的圖示來啟動 Cloud Shell](media/conversational-language-understanding/powershell-portal-guide-1.png)

1. 第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 選取 [PowerShell]****。 若未看到此選項，請略過該步驟。  

1. 如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂用帳戶，然後選取 [建立儲存體]****。 然後等候一分鐘左右，讓系統建立儲存體。 

    ![按一下確認以建立儲存體。](media/conversational-language-understanding/powershell-portal-guide-2.png)

1. 請確定 Cloud Shell 窗格左上方所指出的殼層類型已切換為 *PowerShell*。 若其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    ![如何尋找左側下拉式功能表來切換至 PowerShell](media/conversational-language-understanding/powershell-portal-guide-3.png) 

1. 等候 PowerShell 啟動。 您應該會在 Azure 入口網站中看到下列畫面：  

    ![等候 PowerShell 啟動。](media/conversational-language-understanding/powershell-prompt.png) 

## 設定和執行用戶端應用程式

現在，讓我們開啟並編輯預先撰寫的指令碼，以執行用戶端應用程式。

1. 在命令殼層中，輸入下列命令以下載範例應用程式，並將其儲存至名為 ai-900 的資料夾。

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**注意** 若您已在另一個實驗室中使用此命令來複製 *ai-900* 存放庫，則可跳過此步驟。

1. 檔案會下載到名為 **ai-900** 的資料夾。 現在，我們想要查看此資料夾中的所有檔案，並使用這些檔案。 在殼層中輸入下列命令：

     ```PowerShell
    cd ai-900
    code .
    ```

    請注意指令碼如何開啟編輯器，情況就和下圖一樣： 

    ![程式碼編輯器。](media/conversational-language-understanding/powershell-portal-guide-4.png)

1. 在左側的 [檔案]**** 窗格中，選取 **ai-900** 資料夾中的 **understand.ps1** 檔案。 此檔案包含一些使用交談語言理解模型的程式碼。 

    ![語言理解實驗室的程式碼，其中已框住您在執行程式之前需要修改和儲存的認證。](media/conversational-language-understanding/understand-code.png)

    不用太過顧慮程式碼的細節。 請務必使用下列指示來修改檔案，以指定您所定型的語言模型。 

1. 切換回包含 **Language Studio** 的瀏覽器索引標籤。 然後在 Language Studio 中，開啟 [部署模型]**** 頁面，並選取您的模型。 然後，按一下 [取得預測 URL]**** 按鈕。 您需要的兩項資訊位於此對話方塊中：
    - 模型的端點 - 您可以從 [預測 URL]**** 方塊複製端點。
    - 模型的金鑰 - 金鑰位於**範例要求**中，其形式為 **Ocp-Apim-Subscription-Key** 參數的值，樣貌就像 ***0ab1c23de4f56gh7i8901234jkl567m8***。

1. 複製端點值，然後切換回包含 Cloud Shell 的瀏覽器索引標籤，並將此值貼到程式碼編輯器中，然後取代 **YOUR_ENDPOINT** (引號內)。 針對金鑰重複該程序，然後取代 **YOUR_KEY**。

1. 接下來，將 **YOUR_PROJECT_NAME** 取代為您專案的名稱，並以 **YOUR_DEPLOYMENT_NAME** 取代為已部署模型的名稱。 第一行程式碼看起來應該類似您以下所看到的內容：

    ```PowerShell
    $endpointUrl="https://some-name.cognitiveservices.azure.com/language/..."
    $key = "0ab1c23de4f56gh7i8901234jkl567m8"
    $projectName = "name"
    $deploymentName = "name"
    ```

1. 在編輯器窗格右上方，使用 [...]**** 按鈕開啟功能表，並選取 [儲存]**** 以儲存變更。 接著再次開啟功能表，並選取 [關閉編輯器]****。

1. 在 PowerShell 窗格中，輸入下列命令來執行程式碼：

    ```PowerShell
    ./understand.ps1 "Turn on the light"
    ```

1. 檢閱結果。 應用程式應該已預測出意圖的動作是 switch on the light。

1. 現在請嘗試另一個命令：

    ```PowerShell
    ./understand.ps1 "Switch the fan off"
    ```

1. 檢閱此命令的結果。 應用程式應該已預測出意圖的動作是 switch off the fan。

1. 請再實驗幾個命令；包括所定型的模型未支援的命令，例如「Hello」或「switch on the oven」。 一般來說，應用程式應該會理解所定義的語言模型適用的命令，輸入其他命令則會失敗。

>**注意** 每次都需要以 ./understand.ps1**** 開頭，後面接著片語。 在片語周圍加上引號。

## 深入了解

此應用程式只顯示了語言服務的交談語言理解功能所擁有的一些能力。 若要深入了解此服務的功用，請參閱[交談語言理解頁面](https://docs.microsoft.com/azure/cognitive-services/language-service/conversational-language-understanding/overview)。 
