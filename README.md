# 道路標誌與車輛偵測

本專案為《電腦視覺應用實務》期末報告，主題為利用深度學習進行**道路區域偵測**，應用於智慧交通、標誌辨識。<br>
P.S. 使用colab去實作，但是因為課堂結束時整理雲端硬碟將程式碼清理掉了，只有找到舊版

## 使用資料集

資料集來源：[Prince Khunt 的 Road Detection - IMGs & Labels](https://www.kaggle.com/datasets/princekumar25/road-detection-dataset)

- 包含城市、郊區、筆直與彎道等多樣道路場景
- 標註格式完全相容 YOLOv8，無需繁複前處理

## 🛠️ 專案流程

1. 資料準備與前處理
2. 模型選擇與載入（YOLOv8n、YOLOv11n）
3. 模型訓練（Epoch: 5、100、200）
4. 模型驗證與評估（Confusion Matrix、F1 Curve、Results）
5. 模型推論與展示

## 實驗比較（YOLOv8n vs YOLOv11n）

| 模型 | Epoch | F1 Score | Confidence 閾值 | mAP 表現 | Loss 曲線 | 備註 |
|------|-------|----------|------------------|-----------|-------------|------|
| YOLOv8n | 5 | 0.67 | 0.263 | 上升中 | 波動較大 | 初步訓練 |
| YOLOv8n | 100 | 0.83 | 0.436 | 穩定提升 | 趨於穩定 | 成熟模型 |
| YOLOv8n | 200 | 0.85 | 0.663 | 穩定優異 | 收斂 | 推薦版本 |
| YOLOv11n | 5 | 0.72 | 0.460 | 上升中 | 波動大 | 類別混淆較多 |
| YOLOv11n | 100 | 0.82 | 0.470 | 提升快速 | 穩定下降 | 表現良好 |
| YOLOv11n | 200 | **0.86** | **0.485** | 穩定優異 | 收斂 | **最佳表現** |

> 結論：YOLOv11n Epoch 200 表現最佳，精度與泛化能力最穩定。

## 衍伸應用：違規偵測

利用 YOLOv11n (Epoch 200) 模型，實作監視器畫面中**車輛是否超出停止線**的自動偵測與數量計算。

功能包括：

- 車輛與紅綠燈偵測與框選
- 違規車輛統計輸出

## 評估指標

- Confusion Matrix
- F1 Confidence Curve
- mAP（mean Average Precision）
- Precision / Recall
- Training & Validation Loss
