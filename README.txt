# 教學用模擬銷售資料

兩份CSV各300筆，2026年9月30天，每天10種商品。非真實商業資料。UTF-8 BOM編碼，金額為新臺幣，未另計稅、折扣或運費。每筆是單一商品在當日指定通路的銷售彙總；未出現的商品／日期／通路組合不代表缺漏。

欄位：sale_id紀錄主鍵；sale_date日期；product_id商品編號；product_name商品名稱；category分類；channel通路；unit_price單價；quantity售出數量（含退貨）；returned_quantity退貨數量。

淨銷售額 = unit_price × (quantity - returned_quantity)。

先匯入original，再依sale_id更新為updated完整快照。不可將兩份直接串接成600筆。更新後仍為300筆；共240筆異動、60筆不變。前三種商品每筆銷量增加8件，第7至10種商品每筆增加3件，藍牙耳機每筆退貨增加1件。

驗收數值：
{
  "original": {
    "records": 300,
    "quantity": 3444,
    "returns": 33,
    "netRevenue": 3217100
  },
  "updated": {
    "records": 300,
    "quantity": 4524,
    "returns": 63,
    "netRevenue": 3970100
  },
  "changed": 240
}

圖表要求：每日淨銷售額折線圖、各商品淨銷售額長條圖、各分類淨銷售額占比圓餅圖。可增加通路比較及售出數量與淨銷售額散佈圖。更新MySQL後須重新執行Python並更新靜態網頁，GitHub Pages不會直接查詢MySQL。
