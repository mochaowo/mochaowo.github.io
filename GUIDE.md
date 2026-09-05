# mochaowo 部落格工作流程教學

> 部落格位置：`~/code/blog`　線上網址：https://mochaowo.github.io
> 架構：Hexo + Redefine 主題，部署在 GitHub Pages

---

## 1. 專案結構（先看懂這個）

```
~/code/blog
├── _config.yml            ← 網站設定（標題、作者、網址、部署方式）
├── _config.redefine.yml   ← 主題設定（外觀、橫幅、社交連結）
├── source/
│   ├── _posts/            ← 你的文章（.md 檔）
│   └── .nojekyll          ← GitHub Pages 需要的空檔案，別刪
├── scaffolds/             ← 新文章的範本
├── themes/、node_modules/ ← 主題和套件，不用動
└── public/                ← 建置結果，自動產生，不用動
```

**Git 分支**：
- `source` 分支 = 原始碼（Markdown、設定檔）→ 已推上 GitHub 備份
- `master` 分支 = 建置後的靜態網頁 → 這是 GitHub Pages 讀的，由 `hexo deploy` 自動更新

平常**不需要**自己操作 git，`hexo deploy` 會處理 master；想要備份原始碼時才 `git add -A && git commit && git push origin source`。

---

## 2. 寫一篇文章（最常用的流程）

### 步驟 1：建立新文章

```bash
cd ~/code/blog
hexo new post "我的文章標題"
```

會產生 `source/_posts/我的文章標題.md`。

### 步驟 2：編輯文章

打開那個 .md 檔，最上面是 front-matter（文章的 metadata）：

````markdown
---
title: 我的第一篇文章
date: 2026-09-05 14:20:00
categories:
  - 生活
tags:
  - 隨筆
---

正文從這裡開始，用 Markdown 語法寫。

## 這是標題

- 這是清單
- [這是連結](https://example.com)

```python
print("程式碼區塊會自動上色")
```

<!-- more -->

這行以上是摘要（首頁列表會顯示），以下是全文。
````

常用 front-matter 欄位：

| 欄位 | 說明 |
|---|---|
| `title` | 文章標題 |
| `date` | 發文時間（決定排序） |
| `categories` | 分類（階層式，一篇文章通常一個） |
| `tags` | 標籤（可多個） |
| `toc` | 是否顯示目錄（預設跟主題設定） |
| `excerpt` | 自訂摘要文字 |

### 步驟 3：本機預覽

```bash
hexo server
```

打開 http://localhost:4000 看結果，按 `Ctrl+C` 停止。
改文章存檔後重新整理就會更新（不用重跑指令）。

### 步驟 4：發佈

```bash
hexo clean && hexo deploy
```

- `hexo clean`：清掉舊的建置結果（避免奇怪的快取問題）
- `hexo deploy`：重新建置並推上 GitHub Pages

約 30 秒後刷新 https://mochaowo.github.io 就會看到新文章。

### 想草稿發文？

```bash
hexo new draft "還沒想好的標題"   # 存到 source/_drafts/，不會發佈
hexo server --draft               # 預覽時包含草稿
hexo publish "還沒想好的標題"     # 草稿完成後轉正
```

---

## 3. 插入圖片

**建議做法**：把圖放到 `source/images/` 底下（資料夾不存在就建一個），文章裡這樣引用：

```markdown
![圖片說明](/images/my-photo.png)
```

`source/images/` 底下的檔案會原樣複製到網站，路徑就是 `/images/檔名`。

---

## 4. 修改網站設定

### 網站基本設定 → `_config.yml`

| 設定 | 目前的值 | 說明 |
|---|---|---|
| `title` | mochaowo | 網站標題 |
| `author` | mochaowo | 作者名 |
| `language` | zh-TW | 語言 |
| `url` | https://mochaowo.github.io | 網站網址，**不要改** |
| `deploy` | git → master | 部署目標，**不要改** |

### 主題外觀 → `_config.redefine.yml`

目前只設了標題/副標，其他用主題預設值。常用的調整（改完要 `hexo clean && hexo deploy`）：

```yaml
info:
  title: mochaowo
  subtitle: 歡迎來到我的部落格
  author: mochaowo

# 首頁大橫幅
home_banner:
  enable: true
  title: mochaowo
  # 換首頁背景圖（圖放 source/images/ 底下）
  # image:
  #   light: /images/banner-light.jpg
  #   dark: /images/banner-dark.jpg
  # subtitle:
  #   text: ["這裡會輪播打字機效果"]

# 社交連結
social:
  github: https://github.com/mochaowo
```

完整的可調選項非常多（字體、配色、側欄、程式碼樣式…），參考官方文件：
https://redefine-docs.ohevan.com/

> 小技巧：改主題設定的時候，先在本機 `hexo server` 預覽滿意了再 deploy。

### 新增獨立頁面（例如「關於我」）

```bash
hexo new page about
```

編輯產生的 `source/about/index.md`，然後在 `_config.redefine.yml` 加進導覽列：

```yaml
navbar:
  links:
    Home:
      path: /
    關於我:
      path: /about/
      icon: fa-regular fa-user
```

---

## 5. 備份原始碼（換電腦也不怕）

文章寫完、deploy 之後，建議把原始碼也備份：

```bash
cd ~/code/blog
git add -A
git commit -m "新增文章：文章標題"
git push origin source
```

> 注意：本機 git 目前沒設身分，第一次 commit 前先設定一次：
> ```bash
> git config --global user.name "mochaowo"
> git config --global user.email "你的GitHub信箱"
> ```

---

## 6. 常見問題排解

| 症狀 | 解法 |
|---|---|
| 改了設定但網站沒變 | 先 `hexo clean` 再 `hexo deploy` |
| deploy 後網頁 404 | 等 1–2 分鐘，GitHub Pages 部署有延遲 |
| CSS/樣式整個跑掉 | 確認 repo 有 `.nojekyll`（`source/.nojekyll` 在，就會自動帶上） |
| deploy 出現權限錯誤 | GitHub 登入過期，重跑 `hexo deploy` 會提示，或用 `gh auth login` |
| 文章沒出現在首頁 | 檢查 front-matter 的 `---` 有沒有寫齊、`date` 格式對不對 |

---

## 快速指令卡

```bash
hexo new post "標題"     # 寫新文章
hexo new draft "標題"    # 寫草稿
hexo publish "標題"      # 草稿轉正
hexo new page 名稱       # 獨立頁面
hexo server              # 本機預覽 localhost:4000
hexo clean && hexo deploy  # 發佈上線
```