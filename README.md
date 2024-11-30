# Introduction-of-Text-Mining

# 文字探勘初論期末專題 - 獨領風騷地走在時代尖端—預測新興網路詞彙

## 組員
- 李昀熹（資管二，B11705046@g.ntu.edu.tw）
- 陳庭宇（資管二，B11705053@g.ntu.edu.tw）
- 陳奕廷（資管二，B11705051@g.ntu.edu.tw）
- 陳泊華（資管一，B12705014@g.ntu.edu.tw）

## 動機與目的
在當今網際網路世代，許多潮流在網上產生。隨著網路語言的發展，我們對於不同於傳統日常用語的新興網路詞彙感到好奇，並希望能夠透過分析過往的網路用語來預測未來可能出現的新興網路詞彙。透過此專題，我們希望訓練一個模型，能在一篇輸入文章中發現潛在的新興網路詞彙，並對未來潮流進行預測。

## 解法架構
我們的解法架構如下圖所示：

### 1. 爬蟲資料取得
使用爬蟲從PTT八卦版獲取資料，並將資料進行清理。接著，手動標註每篇文章中的新興詞彙，並建立訓練資料集。

### 2. 資料處理
利用Python中的Selenium函式庫抓取PTT八卦版的資料，並對抓取到的文章進行處理，過濾掉無用字詞（如標點符號、停用詞等），將文章標註為是否包含新興詞彙。

### 3. 模型訓練
使用BERT-Chinese_L-12_H-768_A-12模型，將文章中的每個Token轉換為Embedding，並與人工標註的標籤進行配對，訓練模型進行新興詞彙的預測。

## 資料獲取
我們選擇PTT作為資料來源，因為它是年輕人常用的討論平台，且有足夠的討論度。通過Python爬蟲從八卦版收集文章資料。

## 資料處理與清洗
- 我們只選取PTT八卦版中的正文內容，並過濾掉無用的字詞（如「推」、「噓」等）。
- 因為BERT模型對輸入字數有上限，我們將文章長度限制在512字以內，避免文章被壓縮。

## 人工標籤
我們手動標註了每篇文章中的新興詞彙，並將其作為訓練集的一部分。以下是標籤的格式：

## 模型訓練
我們使用BERT模型的CLS向量作為每篇文章的特徵，並將其與標註的新興詞彙進行對比。使用神經網路來學習文章的語意和新興詞彙的關聯。

### 訓練邏輯
- 使用BERT模型生成文章的CLS向量和詞彙的Embedding。
- 將詞彙Embedding取平均，並用來訓練神經網路，預測文章中是否包含新興詞彙。

## 預測方式
在預測階段，我們將輸入文章並提取其CLS向量，並將其與新興詞彙的Embedding進行比較。如果文章中某些詞彙的MSE低於指定閾值（0.6），我們認為它們是新興詞彙。

## 模型結果
- 我們的模型能夠有效預測文章中的新興詞彙，並且在某些情況下，對沒有新興詞彙的文章，模型會輸出`[CLS]`，表示沒有預測到新興詞彙。
- 我們還發現，文章的可讀性和結構會顯著影響預測的準確度。經過篩選後，模型的效能有了明顯提高。

## 訓練結果
在特定的測試資料集上，我們觀察到模型能夠準確地預測出新興詞彙，例如「萌新」等。同時，在一些無新興詞彙的文章中，模型正確地未預測任何新興詞彙。

## 檢討與改進
本專題中，我們的模型在一些情況下還存在預測噪聲的問題，需要進一步改善模型以提高預測的準確性和過濾噪聲的能力。

