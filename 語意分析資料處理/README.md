# 期中報告 : 股價漲跌關鍵字與預測準確率
詳細介紹如[PPT]( https://github.com/ugotsuyokunaru/BigDataBusinessAnalysis/blob/master/%E8%AA%9E%E6%84%8F%E5%88%86%E6%9E%90%E8%B3%87%E6%96%99%E8%99%95%E7%90%86/%E8%82%A1%E5%83%B9%E6%BC%B2%E8%B7%8C%E9%97%9C%E9%8D%B5%E5%AD%97%E8%88%87%E9%A0%90%E6%B8%AC%E6%BA%96%E7%A2%BA%E7%8E%87(%E7%B0%A1%E8%A6%81%E7%89%88).pptx)
，以下大致說明 : 

## 資料集簡介
教授提供了四個資料集，皆為新聞、論壇或ptt等網站上爬下來的200多萬筆資料，
資料時間為2016、2017兩年，
並提供這兩年間的近2000家上市櫃公司的實際股價。

## 實驗流程設計
我主要是負責寫 1.資料處理 與 2.建立漲跌關鍵字集 的code。

1. 資料處理
  - [選股](https://github.com/ugotsuyokunaru/BigDataBusinessAnalysis/blob/master/%E8%AA%9E%E6%84%8F%E5%88%86%E6%9E%90%E8%B3%87%E6%96%99%E8%99%95%E7%90%86/step0_df_choose_stock.py)
  - [判斷每日股價是漲or跌](https://github.com/ugotsuyokunaru/BigDataBusinessAnalysis/blob/master/%E8%AA%9E%E6%84%8F%E5%88%86%E6%9E%90%E8%B3%87%E6%96%99%E8%99%95%E7%90%86/step1_actual_updown.py)
  - [使用 D+n 方法，將200多萬筆篇文章歸類定義為漲文章or跌文章](https://github.com/ugotsuyokunaru/BigDataBusinessAnalysis/blob/master/%E8%AA%9E%E6%84%8F%E5%88%86%E6%9E%90%E8%B3%87%E6%96%99%E8%99%95%E7%90%86/step2_doc_updown.py)

2. 建立漲跌關鍵字集
  - [將每篇分類好的文章切 2~6 gram關鍵字集，輸出至excel](https://github.com/ugotsuyokunaru/BigDataBusinessAnalysis/blob/master/%E8%AA%9E%E6%84%8F%E5%88%86%E6%9E%90%E8%B3%87%E6%96%99%E8%99%95%E7%90%86/step3_choose_keyword.py)
  - 利用 "全部TF-IDF" 、 "TF-IDF" 、 "DF卡方" 等指標，排序漲跌關鍵字
  - 挑選漲跌各300關鍵字建成 "漲關鍵字集向量" 與 "跌關鍵字向量"


3. 模型訓練與實驗

  - 使用模型套件去跑 scikit-learn 的 logistic regression
  - 5-fold測試出最有效適用(準確率最高)的模型參數
  - 將模參數餵進去，建立個股股價預測模型
  - 用testing data去實驗模型，並判斷預測準確度
