# 歡迎使用您的 VS Code 擴充套件

## 資料夾內容

* 這個資料夾包含您的擴充套件所需的所有檔案。
* `package.json` - 這裡是宣告這個擴充套件和命令的檔案清單。
  * 範例套件每註冊一個命令，都必須定義了其標題和命令名稱，這些資訊將在 VS Code 命令面板中顯示，此時還不需要載入該套件。
* `src/extension.ts` - 這裡是提供命令實作的主要檔案。
  * 該檔案匯出一個函數 `activate`，當此擴充套件首次啟動時會被呼叫（執行此套任何命令時）。在 `activate` 函數內，我們呼叫 `registerCommand`。
  * 我們將包含命令實作的函數作為第二個參數傳遞給 `registerCommand`。

## 設定

* 建議安裝 (amodio.tsl-problem-matcher 和 dbaeumer.vscode-eslint) 這二個擴展套件。

## 快速啟動

* 按下 `F5` 開啟一個新的視窗，載入您的擴充套件。
* 在命令面板中按下 (`Ctrl+Shift+P` 或在 Mac 按 `Cmd+Shift+P`) 後，再輸入 `Hello World` 來執行您的命令。
* 在 `src/extension.ts` 內設定中斷點來除錯您的擴充套件。
* 在除錯控制台中找到您的擴充套件輸出。

## 套件維䕶

* 在 `src/extension.ts` 中更改程式碼後，您可以從除錯工具列重新啟動擴展。
* 您也可以按下 (`Ctrl+R` 或在 Mac 按 `Cmd+R`) 重新載入 VS Code 執行修改後的擴充套件。

## API 參考 

* 您可以開啟 `node_modules/@types/vscode/index.d.ts` 檔案，查閱完整的 API 程式碼。

## 執行測試

* 開啟除錯檢視 (`Ctrl+Shift+D` 或在 Mac 按 `Cmd+Shift+D`)，從啟動配置下拉式選單中選擇 `Extension Tests`。
* 按下 `F5` 鍵將在一個新視窗中載入您的擴充套件，並執行測試。
* 在除錯控制台中可以看到測試的結果。
* 您可以更改 `src/test/suite/extension.test.ts` 或在 `test/suite` 資料夾中建立新的測試檔案。
  * 建立新的測試檔必須符合 `**.test.ts` 這個名稱格式的檔案，測試運行器才會執行。
  * 您可以在 `test` 資料夾內建立新的資料夾，來組織您想要的相關測試。

## 更深入了解

* [遵循 UX 指南](https://code.visualstudio.com/api/ux-guidelines/overview) 建立與 VS Code 本機介面和無縫模式整合的擴件。
* 通過 [封裝擴件](https://code.visualstudio.com/api/working-with-extensions/bundling-extension) 來減少套件大小和改善啟動時間。
* 在 VS Code 套件市集中 [發佈套件](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)。
* 透過設置 [持續整合](https://code.visualstudio.com/api/working-with-extensions/continuous-integration) 來自動化構建。
