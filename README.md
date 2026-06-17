# 114-2-machine
1. 題目
基於時序資料之桌球戰術與結果預測研究

2. Introduction
2.1 動機
    近年來人工智慧（Artificial Intelligence, AI）與機器學習（Machine Learning）快速發展，並逐漸應用於運動分析領域。透過分析選手在比賽中的表現資料，可以協助教練與選手了解戰術模式，提升訓練效率與比賽表現。
    桌球是一項節奏快速且戰術變化豐富的運動，每一次擊球都會受到前幾拍的動作、旋轉及比分狀態影響，因此具有明顯的時序特性。AI CUP 提供完整的桌球逐拍資料集，讓我們能夠利用機器學習技術分析比賽過程中的戰術行為，因此選擇本主題作為研究方向。

2.2 目的
本研究主要目標如下：
  1.	建立桌球戰術與結果預測模型。
  2.	分析不同特徵對預測結果的影響。
  3.	探討時序資料在桌球比賽中的重要性。
  4.	比較不同機器學習模型之效能。
  5.	提升桌球比賽結果預測的準確率。
     
3. 文獻探討
3.1 Random Forest
Random Forest 是一種集成學習方法，透過多棵決策樹投票產生最終結果。
優點：
  •	訓練速度快
  •	不容易過度擬合
  •	適合表格型資料

缺點：
  •	難以學習長距離時序關係
  •	無法充分利用序列資訊

3.2 ExtraTrees
ExtraTrees 與 Random Forest 類似，但在節點切分時加入更多隨機性。
優點：
  •	訓練速度快
  •	泛化能力較佳
  
缺點：
  •	對時序資料學習能力有限
  •	容易忽略前後擊球關聯
  
3.3 Transformer
Transformer 利用 Attention 機制學習資料之間的關聯性。
優點：
  •	適合處理時序資料
  •	能學習長距離依賴關係

缺點：
  •	訓練時間較長
  •	需要較大的資料量
  •	計算資源需求較高

4. 我的方法
    主要採用特徵工程與集成學習方法進行預測。
4.1 資料前處理
  •	缺失值處理
  •	類別特徵編碼
  •	依照 rally_uid 與 strikeNumber 排序

4.2 特徵工程
(1) scoreDiff
scoreDiff = scoreSelf − scoreOther
表示目前比分差距。

(2) Long Rally
判斷是否為長回合。

(3) 時序特徵
建立前一拍與前兩拍資訊：
  •	prev1_actionId
  •	prev1_spinId
  •	prev1_pointId
  •	prev2_actionId
  •	prev2_spinId
  •	prev2_pointId
讓模型能學習擊球之間的關聯性。

4.3 模型訓練
本研究比較：
  •	Random Forest
  •	ExtraTrees
  •	Transformer
  •	Soft Voting Ensemble

最後使用 Soft Voting Ensemble 作為最佳模型。

5. 實驗結果
5.1 資料集
Training Set：
  •	約 84,707 筆資料

Testing Set：
  •	約 5,668 筆資料

5.2 實驗結果
    方法	                      Public Score
    Baseline	                  0.170
    Transformer	                0.200
    ExtraTrees	                0.230
    Random Forest	              0.257
    Random Forest + 時序特徵	    0.270
    Soft Voting Ensemble	      0.278

5.3 結果分析
實驗結果顯示：
  1.	加入時序特徵後能有效提升模型表現。
  2.	前一拍與前兩拍資訊對桌球戰術預測具有重要影響。
  3.	Soft Voting Ensemble 能降低單一模型誤差。
  4.	集成學習方法獲得最佳預測結果。

6. 參考資料
[1] AI CUP 競賽官方網站
[2] Breiman, L. (2001). Random Forests. Machine Learning.
[3] Geurts, P., Ernst, D., & Wehenkel, L. (2006). Extremely Randomized Trees.
[4] Vaswani, A. et al. (2017). Attention Is All You Need.
[5] Scikit-learn Documentation.
https://scikit-learn.org
[6] TensorFlow Documentation.
https://www.tensorflow.org
[7] Keras Documentation.
https://keras.io
