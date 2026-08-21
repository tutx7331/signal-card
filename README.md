# 報單圖產生器 · Signal Card

把交易分析變成一張可以直接發群的 1080×1080 圖。

填入商品、方向、進場區間、停損、目標，拖一張盤面截圖進去，選一個版型，下載 PNG。**24 種版型**，從極簡票券到映像管電視、拍立得、登機證、黑膠唱片封套都有。

適用於股票、期貨、外匯、加密貨幣——任何需要把「一筆交易的計畫」講清楚的場合。

## 特點

- **零後端**：所有運算都在瀏覽器裡。你的截圖和資料不會上傳到任何伺服器。
- **可離線**：安裝成 PWA 後沒有網路也能用。
- **25 種版型**：不只換配色，每套的外框、版面骨架、資訊層級都不同。
- **圖片 1:1 精準控制**：截圖以原生像素顯示，拖曳定位、滾輪縮放，所見即所得。
- **記住你的設定**：品牌名、LOGO、慣用版型、免責聲明都會保留。
- **單一檔案**：核心就是一個 `index.html`，沒有建置流程、沒有相依套件管理。

## 使用

### 線上版

部署後直接開網址即可。

### 安裝到手機主畫面

- **iOS Safari**：分享 → 加入主畫面
- **Android Chrome**：選單 → 安裝應用程式

安裝後全螢幕執行，沒有網址列，體驗接近原生 App。

### 本機執行

因為用到 Service Worker，直接用 `file://` 開啟會有部分功能受限。建議起一個本機伺服器：

```bash
git clone https://github.com/<你的帳號>/signal-card.git
cd signal-card
python3 -m http.server 8080
# 瀏覽器開 http://localhost:8080
```

## 部署

任何靜態託管都行，不需要任何後端設定。

**GitHub Pages**：Settings → Pages → Source 選 `main` 分支根目錄，等一分鐘即可。

**Cloudflare Pages / Netlify / Vercel**：連結 repo，建置指令留空，輸出目錄填 `/`。

> Service Worker 需要 HTTPS 才會註冊（`localhost` 除外）。上述平台都預設提供 HTTPS。

## 自訂

### 換成你的品牌

在控制面板底部上傳 LOGO、填入品牌名與標語，設定會被記住。建議使用**去背 PNG**，深淺版型都能適應。

### 新增版型

每個版型就是一組 CSS 變數加上可選的版面規則，加在 `index.html` 的 `<style>` 裡：

```css
#card[data-theme="yourtheme"]{
  --ink:#0B0D10;      /* 卡片底色 */
  --panel:#12161C;    /* 面板底色 */
  --line:#2A323D;     /* 分隔線 */
  --dim:#7C8899;      /* 次要文字 */
  --paper:#EDEFF2;    /* 主要文字 */
  --long:#22C58B;     /* 做多色 */
  --short:#FF5C5C;    /* 做空色 */
  --gold:#D8A24A;     /* 標籤強調色 */
  --chartbg:#080A0D;  /* 圖表區底色 */
  --note:#C6CEDA;     /* 說明文字 */
  --disc:#5A6472;     /* 免責聲明 */
  --stampbg:rgba(11,13,16,.72); /* 方向章底色 */
}
```

再到導覽列加一顆按鈕：

```html
<button data-t="yourtheme">你的版型</button>
```

想改版面骨架（而不只是配色），可以覆寫 `.head` `.chart` `.grid` `.foot` 這些區塊，用 `order` 調整順序、用 `::before` / `::after` 做外框裝飾。可以參考現有的 `crt`、`boarding`、`vinyl` 幾套的寫法。

### 匯出注意事項

輸出用 [html2canvas](https://html2canvas.hertzen.com/)，它**不支援** `backdrop-filter`、`mask-composite`、`conic-gradient`。做新版型時請避開這些屬性，否則螢幕上正常但匯出會走鐘。`box-shadow`、`linear-gradient`、`radial-gradient`、`text-shadow` 都可以正常使用。

## 授權

MIT License。可自由使用、修改、商用。

## 免責

本工具只負責排版，不產生任何交易訊號，也不對任何交易結果負責。使用者應自行確認所發布內容符合當地法規——在部分司法管轄區，公開發布投資建議需要相應牌照。
