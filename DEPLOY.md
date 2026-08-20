# 部署教學：從零到朋友能加到主畫面

全程免費，不需要買網域。預計 15 分鐘。

---

## 你不需要網域

GitHub 會免費給你一個網址，長這樣：

```
https://你的帳號.github.io/signal-card/
```

這個網址就是你要傳給朋友的東西。**你不需要傳任何檔案給他們**——他們打開網址、加到主畫面，就完成了。

而且這個網址是 HTTPS，PWA 安裝功能才能運作（這是硬性要求，所以不能只把 HTML 檔傳給對方）。

---

## 第一步：把檔案放上 GitHub

### 方法 A：網頁上傳（不用裝任何東西，推薦）

1. 到 [github.com](https://github.com) 註冊或登入
2. 右上角 **+** → **New repository**
3. Repository name 填 `signal-card`
4. 選 **Public**（要用免費的 GitHub Pages 就必須公開）
5. 不要勾任何 "Add a README" 之類的選項，直接 **Create repository**
6. 進到空白 repo 頁面，點 **uploading an existing file**
7. 把 `signal-card` 資料夾裡的**所有檔案**拖進去（全部都是一般檔案，沒有子資料夾）
8. 下方 **Commit changes**


### 方法 B：用 Git 指令

```bash
cd signal-card
git init
git add -A
git commit -m "feat: 報單圖產生器 v1.0"
git branch -M main
git remote add origin https://github.com/你的帳號/signal-card.git
git push -u origin main
```

---

## 第二步：開啟 GitHub Pages

1. 在你的 repo 頁面點 **Settings**
2. 左側選單找到 **Pages**
3. Source 選 **Deploy from a branch**
4. Branch 選 **main**，資料夾選 **/ (root)**
5. 按 **Save**

等 1～3 分鐘，重新整理這個頁面，上方會出現你的網址。

**這個網址就是你的成品。** 存起來。

---

## 第三步：傳給朋友

直接傳網址就好，不用傳檔案。

告訴他們怎麼裝：

**iPhone / iPad**
1. 用 **Safari** 打開網址（Chrome 不行，iOS 只有 Safari 能加主畫面）
2. 點下方中間的**分享**圖示
3. 往下滑，選 **加入主畫面**
4. 按新增

**Android**
1. 用 Chrome 打開網址
2. 通常會自動跳出「安裝應用程式」提示
3. 沒跳的話：右上角三個點 → **安裝應用程式** 或 **加到主畫面**

**電腦**
Chrome / Edge 網址列右側會出現一個安裝圖示，點它即可。也可以直接用瀏覽器開，不一定要安裝。

裝好之後桌面會有圖示，點開是全螢幕、沒有網址列，用起來跟 App 一樣。

---

## 之後要改版怎麼辦

這是 PWA 最大的好處：**你改，所有人自動更新，不用重傳任何東西。**

1. 修改 `index.html`
2. 把 `sw.js` 裡的 `VERSION` 數字加一，例如 `v1.0.1` 改成 `v1.0.2`
   （這步很重要，不改的話使用者會一直看到舊的快取版本）
3. 上傳到 GitHub（網頁上點檔案 → 鉛筆圖示編輯 → Commit）
4. 等 1～2 分鐘，使用者下次開啟就是新版

---

## 常見狀況

**開網址是一片空白**
Pages 還在部署，等 2 分鐘重新整理。若仍空白，確認 repo 根目錄有 `index.html`（不是放在子資料夾裡）。

**圖示沒出現 / 加到主畫面是白色方塊**
確認 4 張 `icon-*.png` 都有上傳成功，應該直接出現在 repo 檔案列表裡。

**iOS 沒有「加入主畫面」選項**
一定要用 Safari。從 LINE、Telegram 內建瀏覽器點開的話，先選「用 Safari 開啟」。

**改了東西但看不到變化**
沒改 `sw.js` 的 `VERSION`。改完再等一下，或請使用者把 App 從主畫面刪掉重裝。

**想換更好記的網址**
之後如果想用自己的網域（例如 `signal.你的網域.com`），在 Settings → Pages → Custom domain 填入即可，GitHub 免費支援，只是網域本身要另外買。不急，先用預設網址完全沒問題。

---

## 關於 Repo 公開

免費版 GitHub Pages 需要 repo 是 Public，也就是**任何人都看得到原始碼**。

以這個專案來說這是好事——你本來就打算開源。但要注意：**不要把任何私人資訊放進 repo**，例如你的 LOGO 原始檔如果不想公開、或任何 API 金鑰（這個專案沒有用到金鑰，所以不用擔心）。

使用者上傳的 LOGO 和截圖都存在他們自己的瀏覽器裡，不會進到你的 repo。
