# 畢業專題週報站

學生每週回報專題進度、遇到的問題、下週計畫與需要的材料；老師即時看全班。
學生用「學生連結」在自己的裝置上填寫，不需要帳號。

## 部署（GitHub Pages）

1. 把這個資料夾的所有檔案放進一個公開的 repo（`index.html`、`config.js`、`lib/` 兩個檔案）。
2. 在 repo 的 Settings → Pages，來源選 Deploy from a branch，分支選 `main`、資料夾選 `/ (root)`。
3. 等一兩分鐘，開啟 Pages 給的網址，會看到「老師第一次使用：連接資料庫」。

## 連接資料庫（老師做一次）

網頁上有同樣的步驟。資料存在老師自己的 Firebase 專案（Firestore）。

Firestore 規則：

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /classes/{classId}/{coll}/{docId} {
      allow read, write: if true;
    }
  }
}
```

建立班級後，「名單與設定」會出現兩個連結：

- 學生連結：給全班。可以填寫週報、看自己的歷程和老師的回覆。
- 老師連結：自己留著。可以看全班總覽、回覆、改名單。

## 請注意

- 連結就是鑰匙。拿到學生連結的人都能讀寫這個班的週報；老師和學生的差別只在畫面上，資料庫本身不會擋。
- 名單請用座號、暱稱或代稱。不要輸入姓名、電話、住址，也不要把班級資料檔放進這個 repo。
- 想讓分享連結變短：把 Firebase 設定填進 `config.js`。
