# FlexiGPT

作為進階使用者與 GPT AI 模型（GPT3、ChatGPT 等）進行互動。

FlexiGPT 提供預定義的提示（prompt），搭配自定或預定義的函數，可進行工程化調整，以滿足特定的使用者需求。
提示可以儲存並直接在 VSCode 中使用，且此擴充套件支援 GPT APIs 的請求參數修改，以及透過提示中的 responseHandlers 進行回應後處理。

使用者可以使用聊天活動欄介面中，進行請求/互動，載入/儲存歷史對話、匯出對話至檔案，以及從 GPT 回應中複製/插入/建立新檔案。

FlexiGPT 也提供多種使用者介面和存取功能，包括鍵盤快速鍵、編輯器/命令內文，以及命令面板控制，更易於使用並可自訂。

從此處下載：[VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=ppipada.flexigpt)


## 目錄 (Table of contents) <!-- omit from toc -->

- [功能特色](#功能特色)
- [安裝](#安裝)
- [配置](#配置)
- [使用方式](#使用方式)
- [提示文件格式](#提示文件格式)
  - [範例](#範例)
  - [這是一個 JavaScript (.js) 提示檔案的範例](#這是一個 JavaScript (.js) 提示檔案的範例)
  - [這是一個複雜一點的 JavaScript (.js) 提示檔案範例](#這是一個複雜一點的 JavaScript (.js) 提示檔案範例)
  - [建立命令](#建立命令)
    - [預定義系統變量](#預定義系統變量)
    - [預定義系統函數](#預定義系統函數)
  - [變量建立](#變量建立)
  - [函數建立](#函數建立)
- [許可證](#許可證)
- [貢獻](#貢獻)
- [支援](#支援)

## 功能特色

- 可以向 GPT AI 模型（例如 GPT3, ChatGPT 等）提出任何问题

  - 目前支援：
    - 使用 GPT3.5 模型的 OpenAI 聊天完成 API
    - 使用 GPT2/3 模型的 OpenAI 完成 API

- 使用預先定義的提示在配置文件中

  - 工程師和微調提示，儲存並直接在 VSCode 中使用。
  - 可以使用預定義功能或自定義功能來分類提示。內建多種的 [預定義系統功能](#預定義系統功能)。
  - 支援 GPT API 的請求參數修改
  - 支援在提示中通過 responseHandlers 進行後處理響應。
  - 內建提示：

    - [FlexiGPT 基本提示](https://github.com/ppipada/vscode-flexigpt/blob/main/media/prompts/flexigptbasic.js)

      - 重構選擇
      - 產生單元測試
      - 完成
      - 解釋代碼
      - 產生文檔
      - 查找問題
      - 優化選擇

    - [Go 基本提示](https://github.com/ppipada/vscode-flexigpt/blob/main/media/prompts/gobasic.js)
      - 寫 godoc 字串
      - 產生單元測試

- UI 和訪問

  - 聊天活動欄界面，可進行請求/響應互動
  - 從歷史記錄中載入/儲存對話
  - 將對話匯出到文件
  - 複製、插入、建立新文件以獲取 GPT 響應。
  - 活動欄本身提供了從/to GPT APIs 的詳細請求和響應，以進行更好的提示工程和調試。
  - 快捷鍵、編輯器/命令內文（在編輯器中右鍵單擊）、命令面板控件，以便快速訪問

- 立即的 TODO:

  - 額外的功能:
    - 支援其他模型，例如：[Cohere](https://cohere.ai/)、[AI21](https://docs.ai21.com/)
  - 提示文件:
    - 在發送 API 之前加入支援預處理提示。
  - 提供豐富的數據處理功能，例如:
    - 收集定義，剝離它們並傳遞它們等。
    - 從 git 分支收集差異以進行 

## 安裝

- 需求
  - Visual Studio Code v1.74.0 或更高版本
- 步驟：
  1. 安裝 Visual Studio Code v1.74.0 或更高版本
  2. 啟動 Visual Studio Code
  3. 從命令選單 `Ctrl`-`Shift`-`P` (Windows, Linux) 或 `Cmd`-`Shift`-`P` (macOS)，執行 `> Extensions: Install Extension`.
  4. 選擇 `ppipada` 開發的 `FlexiGPT` 擴展程式
  5. 安裝完畢後重新啟動 Visual Studio Code

## 設定

FlexiGPT 需要 OpenAI API 金鑰才能運作。您可以在 OpenAI 帳戶中取得 [OpenAI API 金鑰](https://platform.openai.com/account/api-keys)。

要設定 FlexiGPT，請開啟 Visual Studio Code 的設定檔 (檔案 > 喜好設定 > 設定或使用 `Ctrl`/`Cmd` + `,` 快速鍵)，然後搜尋 `flexigpt`。

FlexiGPT 預設使用 `gpt-3.5-turbo` 的模型，除非 prompt 覆寫它。

選項：

- flexigpt.openai.apiKey: 您的 [OpenAI API 金鑰](https://platform.openai.com/account/api-keys)，可從 OpenAI 網站取得。
- flexigpt.openai.timeout: OpenAI 請求的逾時時間，以秒為單位。預設值：60。
- flexigpt.openai.defaultChatCompletionModel: 聊天完成請求的預設模型。
  - 您可以透過 prompt 檔案命令宣告，永遠覆寫預設模型。
  - FlexiGPT 基本提示將使用預設模型集。
  - 預設值：`gpt-3.5-turbo`。請注意，`gpt-3.5-turbo` 的使用量計入 OpenAI 的計費。目前僅有 Codex (`code-davinci-002`) 是免費 beta 模型（2023 年 2 月）。
- flexigpt.openai.defaultCompletionModel: 完成請求的預設模型。
- flexigpt.openai.defaultEditModel: 編輯請求的預設模型（目前不支援）。
  - 您可以透過 prompt 檔案命令宣告，始終覆寫預設模型。
  - FlexiGPT 基本提示將使用預設模型集。
  - 預設值：`code-davinci-edit-001`。
- flexigpt.promptFiles: 一個以分號分隔的使用者定義的提示配置檔案的路徑列表。提示檔案的配置詳情請見 [下面](#prompt-file-format)。
- flexigpt.inBuiltPrompts: 一個以分號分隔的內建提示檔名列表，用於啟用內建提示。多個名稱請以 ';' 分隔。'flexigptbasic.js' 將始終啟用。可在 [這個路徑](https://github.com/ppipada/vscode-flexigpt/tree/main/media/prompts) 找到內建提示。當前值為："flexigptbasic.js" 和 "gobasic.js"。
- 完整配置示例

  ```text
  "flexigpt.openai.apiKey": "sk-mkey",
  "flexigpt.openai.timeout": "120",
  "flexigpt.openai.defaultCompletionModel": "gpt-3.5-turbo",
  "flexigpt.openai.defaultChatCompletionModel": "gpt-3.5-turbo",
  "flexigpt.openai.defaultEditModel": "code-davinci-edit-001",
  "flexigpt.promptFiles": "/home/me/my_prompt_files/myprompts.js",
  "flexigpt.inBuiltPrompts": "gobasic.js"
  ```

## 使用方式

- 啟動/調用 FlexiGPT:

  - 要詢問 GPT AI 模型（GPT3、ChatGPT等）您想問的任何問題，請使用命令面板（`Ctrl`/`Cmd` + `Shift` + `P`）中的 `FlexiGPT: Ask` 命令，或使用 `Ctrl` + `Alt` + `G` 鍵盤快捷鍵。
  - 這應該會開啟帶有輸入文字框的 FlexiGPT 活動欄。
  - 點擊輸入文字框時，由 FlexiGPT 自己提供的 [基本提示](https://github.com/ppipada/vscode-flexigpt/blob/main/media/prompts/flexigptbasic.js)，任何在 `flexigpt.promptFiles` 中定義的提示以及使用 `flexigpt.inBuiltPrompts` 啟用的任何內建提示，將根據配置進行加載。 （如果首次點擊文字框未加載某些預配置提示，請嘗試選擇其他選項再次點擊。VSCode可能需要一些時間來從文件加載動態列表。）

- 問些什麼

  - 如果選擇預配置提示，則將在取代定義的系統/用戶變量後使用提示命令中定義的問題範本。其他命令選項也將從定義本身中獲取。
  - 如果您在文字框中輸入自由浮動問題，則文字本身將直接用作提示。
  - 可以使用[預定義的系統變數](#預定義的系統變數)來增強您的問題。
    - 例如：您可以使用 `{system.selection}` 來傳遞編輯器中選定的文字（代碼或其他）。
    - 請注意，系統變量的 `system.` 前綴是可選的。因此您可以只用 `{selection}` 來選定文字，或者使用 `{language}` 取代 `{system.language}` 來使用您的文件的語言。

- 要查看提示歷史記錄，請開啟 FlexiGPT 活動欄。

## 提示文件格式

### 範例

- [FlexiGPT 基本提示](https://github.com/ppipada/vscode-flexigpt/blob/main/media/prompts/flexigptbasic.js)
- [Go 基本提示](https://github.com/ppipada/vscode-flexigpt/blob/main/media/prompts/gobasic.js)

### 這是 javascript（.js）提示文件的範例

```js
module.exports = {
  commands: [
    {
      name: "Refactor",
      template: `Refactor following function.
            function:
            {system.selection}`,
    },
  ],
};
```

### 這是較複雜的 Javascript (.js) 提示框檔案

```js
module.exports = {
  commands: [
    {
      name: "Create unit test.",
      template: `Create unit test in {user.unitTestFramework} framework for following function.
            code:
            {system.selection}`,
      responseHandler: {
        func: "writeFile",
        args: {
          filePath: "user.testFileName",
        },
      },
      requestparams: {
        model: "gpt-3.5-turbo",
        stop: ["##", "func Test", "package main", "func main"],
      },
    },
    {
      name: "Write godoc",
      template: `Write godoc for following functions.
            code:
            {system.selection}`,
      responseHandler: {
        func: "append",
        args: {
          position: "start",
        },
      },
      requestparams: {
        model: "code-davinci-002",
        stop: ["##", "func Test", "package main", "func main"],
      },
    },
  ],
  functions: [
    // you could also write your own responseHandler
    function myHandler({ system, user }) {
      console.table({ system });
      console.table({ user });
    },
  ],
  variables: [
    {
      name: "unitTestFramework",
      value: "testing",
    },
    {
      name: "testFileName",
      value: ({ baseFolder, fileName, fileExtension }) =>
        `${baseFolder}\\${fileName}_test.${fileExtension}`,
    },
  ],
};
```

### 建立指令

- 名稱：必填

  - 指令名稱，可以是任何您想要的名稱

- 範本：必填

  - 建立 GPT 模型請求時使用的提示範本（OpenAI等）。您可以在範本中使用系統變數或使用者定義變數。在準備請求時，變數將被取代為正確的值。
  - 要使用系統變數，請加上 `{system.*variableName*}`，variableName 可以是[預先定義的系統變數](#predefined-system-variables)之一。
  - 要使用使用者變數，請加上 `{user.*variableName*}`，variableName 必須在提示檔案的變數欄位中。

- 請求參數：可選

  - 這是一個類型為 `{[key:string]: any}` 的物件。
  - 可以覆蓋與 GPT 提供者 API 相關的任何參數。
  - OpenAI 完成請求的有效參數可以在此 [API 參考](https://platform.openai.com/docs/api-reference/completions) 中找到。

- 回應處理程序：可選

  - 回應處理程序用於處理回應。預設使用取代函數。處理函數可以是 [預先定義的系統函數](#預先定義的系統函數) 或使用者定義函數之一。
  - 您可以使用以下方式設置回應處理程序：

    - 僅使用函數名稱。函數使用預設值執行。

   ```js
    responseHandler: "replace";
    ```

    - With args function name to set function args

    ```js
    responseHandler: {
        func: 'replace',
        args: {
        textToReplace: 'user.answerModified'
        }
    }
    ```
#### 預定義的系統變數

| 變數名稱                | 說明                              |
| ----------------------- | -------------------------------- |
| system.selection        | 編輯器中選定的文字                 |
| system.question         | OpenAI 的問題                     |
| system.answer           | OpenAI 的回答                     |
| system.language         | 目前檔案的程式語言                 |
| system.baseFolder       | 專案的基礎路徑                     |
| system.fileName         | 目前檔案的名稱                     |
| system.filePath         | 目前檔案的完整路徑                 |
| system.fileExtension    | 目前檔案的副檔名                   |
| system.commitAndTagList | 最近的 25 次提交及其相關的標籤列表  |

請注意，系統變數的 `system.` 前綴是可選。因此只能用 `{selection}` 來使用選定或使用文字， `{language}` 而不是 `{system.language}` 來獲取檔案的程式語言。

#### 預定義的系統函數

| 函數名稱      | 說明               | 參數（預設值）                                        |
| -------------| ------------------ | ---------------------------------------------------- |
| append       | 新增文字            | textToAppend（system.answer）、postion（'end'）       |
| replace      | 取代選定的文字       | textToReplace（system.answer）                       |
| showWebView  | 顯示 Webview        | question（system.question）、question（system.answer）|
| writeConsole | 將文字寫入控制台     | content（system.answer）                              |
| writeFile    | 將文字寫入檔案       | filePath（）、content（system.answer）                |

- 取代文字

  - 在選取範圍內取代文字，可接受選擇性參數 `textToReplace`。若未提供此參數，則預設值為 API 的回答。
  - 預設用法

    ```js
        ...
        commands: [
            {
                name: "Refactor",
                template: `Refactor following function.
                function:
                {system.selection}`
                responseHandler:'replace'
            },
        ],
    ```

  - 參數的用法

    ```js
        ...
        commands: [
            {
                name: "Refactor",
                template: `Refactor following function.
                function:
                {system.selection}`
                responseHandler:{
                    func: 'replace',
                    args: {
                        textToReplace: 'user.answerModified'
                    }
                }
            },
        ],
        variables: [
            {
                name: "answerModified",
                value: ({answer})=>`/*\n${anwer}\n*/`
            },
        ],
    ```

  - 附加文字

  - 在選取範圍內附加文字，可接受 `textToAppend` 和 `postion` 兩個選擇性參數。`postion` 可以為 `start` 或 `end`。
  - 當沒有提供 `textToAppend` 參數時，預設值為 OpenAI。
  - 若未提供 `postion` 參數，則附加文字至選取範圍結尾。
  - 範例用法
  
    ```js
        ...
        commands: [
            {
                name: "Append",
                template: `Write jsdoc for following function.
                function:
                {system.selection}`
                responseHandler:{
                    func: 'append',
                    args: {
                        position: 'start'
                    }
                }
            },
        ],
    ```

### 建立變數

任何 `變數` 項目都可以在命令範本中使用。使用者自定義的值必須具有 "user" 前綴。
例如：如果在變數中定義 "testFileName"，則可以在範本文件中使用 "user.TestFileName" 或將其傳遞給函數。

變數值可以是靜態或動態的。對於動態值，應該建立一個 getter 方法。
調用變量 getter 時，系統變量 (參見預定義的系統變量) 和函數作為參數傳遞，第一個參數是系統變量，第二個是函數。


```js
module.exports = {
variables: [
    {
        //static
        name: "testingFramework",
        value: "xUnit"
    },
    {
        //dynamic
        name: "typeNameInResponse",
        value: ({ answer/*system variable*/ }, { extractTypeName/*user defined function*/ }) => extractTypeName({ code: answer })
    },
]
functions: [function extractTypeName({ code, system }) {/**/}],
commands: [
    {
        name: "Create DTO",
        template: `Create unit test with {user.testingFramework} for following class.
        class:
        {system.selection}`,
        responseHandler: {
            func: 'writeFile',
            args: {
                filePath: 'user.typeNameInResponse'/*usage for function arg*/
            }
        }
    }
]
}
```

### 建立函數

待完成

## 授權

FlexiGPT 是根據 [MIT 授權](https://github.com/ppiapda/vscode-flexigpt/blob/master/LICENSE) 的開源軟件。

## 貢獻

歡迎貢獻！請在 GitHub 上提交拉取請求。

## 支援

如果您有任何問題或問題，請在 GitHub 的 [issues](https://github.com/ppiapda/vscode-flexigpt/issues) 頁面上開啟問題。 
