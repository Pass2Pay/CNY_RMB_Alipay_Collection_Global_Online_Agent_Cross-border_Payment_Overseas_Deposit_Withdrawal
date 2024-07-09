---
title: "API 請求"
slug: "request"
excerpt: "👀 了解 PassToPay API"
hidden: false
createdAt: "Sun Mar 10 2024 07:01:24 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Mar 28 2024 01:27:29 GMT+0000 (Coordinated Universal Time)"
---
PassToPay API 是基於 REST 風格組織的。我們的 API 使用可預測的資源導向 URL，接受表單編碼的請求主體，返回 JSON 編碼的響應，並使用標準的 HTTP 響應碼、身份驗證。

***

下圖以客戶使用支付寶掃碼支付為例，展示各個系統之間的交互流程：

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9d56db2-image.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


### 關鍵字定義和術語

| 關鍵字                 | 定義                           |
| :------------------ | :--------------------------- |
| Merchant            | PassToPay'的商家（可能意味著伺服器或網站本身） |
| Customer            | 商家的客戶或網路使用者                  |
| Deposit Submission  | 商家在存款過程中向網關(Gateway) 提交的有效提交 |
| Deposit Result      | 存款流程完成後，網關傳回商家的結果            |
| Transfer Submission | 商家在轉帳過程中向網關提交的有效提交           |
| Transfer Result     | 轉帳流程完成後，網關傳回商家的結果            |
| Verification        | 提供給商家用於**簽名**目的的私鑰           |

### 參數規格

[block:parameters]
{
  "data": {
    "h-0": "關鍵參數",
    "h-1": "描述",
    "0-0": "sign ",
    "0-1": "每個請求都是由商家唯一的私鑰發出的，主要用於做簽名驗證。  \n (一個私鑰提供給商家的金鑰，以確保請求是透過該私鑰產生的簽名發送的）  \n請參閱**請求簽名**",
    "1-0": "Merchant ID",
    "1-1": "各商家對應的唯一ID",
    "2-0": "Transaction amount",
    "2-1": "預設為人民幣交易，單位為分，參數值不能包含小數",
    "3-0": "Time parameters",
    "3-1": "所有時間參數均使用精確到毫秒的13位數值，如：1622016572190。定時器具體是指從GMT 00:00:00開始的毫秒數從1970年1月1日至今。"
  },
  "cols": 2,
  "rows": 4,
  "align": [
    "left",
    "left"
  ]
}
[/block]


### API常用請求參數

| 參數   | 類型     | 描述                                                                          |
| :--- | :----- | :-------------------------------------------------------------------------- |
| sign | string | 請參閱**[請求簽名](https://pass2pay-zh-hk.readme.io/reference/signing-a-request)** |

### API常用回應參數

[block:parameters]
{
  "data": {
    "h-0": "參數",
    "h-1": "類型",
    "h-2": "例子",
    "h-3": "描述",
    "0-0": "code",
    "0-1": "int",
    "0-2": "0",
    "0-3": "成功 (0)  \n其他-處理有誤，具體錯誤詳見msg字段",
    "1-0": "msg",
    "1-1": "string",
    "1-2": "format error",
    "1-3": "結果資訊  \n或具體錯誤原因，例如：簽章失敗、參數格式驗證錯誤",
    "2-0": "sign",
    "2-1": "string",
    "2-2": "4A5078DABBCE0D9C4",
    "2-3": "資料內容的簽名。如果資料為空，則不會傳回。",
    "3-0": "data",
    "3-1": "string",
    "3-2": "{}",
    "3-3": "傳回json格式的結果數據"
  },
  "cols": 4,
  "rows": 4,
  "align": [
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


### API常用回應參數代碼定義

| Value | Description    |
| :---- | :------------- |
| 0     | 成功             |
| 9999  | 異常，具體錯誤詳見msg字段 |
