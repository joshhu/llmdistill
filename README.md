# LLM Knowledge Distillation 示範

這是一個完整的語言模型知識蒸餾（Knowledge Distillation）示範專案，展示如何讓小型學生模型從大型老師模型生成的資料中學習。

## 📚 專案簡介

Knowledge Distillation 是一種模型壓縮技術，透過讓較小的「學生模型」學習較大的「老師模型」的知識，來獲得接近大模型的效能，同時大幅減少參數量和計算資源需求。

### 核心概念

1. **老師模型（Teacher Model）**: GPT-2 (117M 參數) - 用來生成高品質的訓練資料
2. **學生模型（Student Model）**: 自定義小型 GPT-2 (40M 參數) - 從老師生成的資料學習
3. **評估指標**: Perplexity - 衡量語言模型的效能

## 🚀 特色功能

- ✅ 完整的端到端實驗流程
- ✅ 可在 Google Colab Free Tier (16GB GPU) 上執行
- ✅ 使用 Perplexity 評估模型效能
- ✅ 視覺化比較結果
- ✅ 實際文本生成效果展示
- ✅ 訓練時間約 15-20 分鐘

## 📋 實驗流程

1. **載入老師模型**: 使用預訓練的 GPT-2
2. **生成訓練資料**: 老師模型生成 500 個文本樣本
3. **建立學生模型**: 設計較小的模型架構（參數減少 66%）
4. **訓練學生模型**: 使用老師生成的資料進行訓練
5. **評估與比較**: 計算訓練前後的 Perplexity
6. **視覺化結果**: 圖表呈現效能比較
7. **生成測試**: 比較老師與學生的文本生成能力

## 💻 使用方式

### 在 Google Colab 上執行

1. 開啟 Google Colab: https://colab.research.google.com/
2. 上傳 `llm_distillation_demo.ipynb`
3. 設定 Runtime 類型為 GPU (T4)
   - Runtime → Change runtime type → Hardware accelerator → GPU
4. 依序執行所有 cells
5. 查看訓練結果和視覺化圖表

### 本地執行

如果你有 CUDA GPU (建議 16GB+ VRAM)：

```bash
# 安裝相依套件
pip install transformers datasets torch accelerate sentencepiece matplotlib

# 使用 Jupyter 開啟 notebook
jupyter notebook llm_distillation_demo.ipynb
```

## 📊 預期結果

執行完成後，你會看到：

- **模型規格比較**: 參數量、壓縮比
- **Perplexity 結果**:
  - 老師模型的 baseline
  - 學生模型訓練前後的改善
- **達成率分析**: 學生模型相對於老師模型的效能
- **視覺化圖表**: 柱狀圖比較三種情況的 Perplexity
- **文本生成比較**: 老師與學生模型的實際輸出對比

## 🎯 典型結果範例

```
📊 模型規格:
  • 老師模型: GPT-2 (117.0M 參數)
  • 學生模型: GPT-2-Small (40.0M 參數)
  • 參數壓縮比: 2.93x

📈 Perplexity 結果:
  • 老師模型: ~25-30
  • 學生模型 (訓練前): ~1500-2000
  • 學生模型 (訓練後): ~35-45
  • 改善率: ~97%

🎯 達成率分析:
  • 學生模型達成率: 60-75%
    (相對於老師模型的 perplexity 表現)
```

## 🔧 模型架構

### 老師模型 (GPT-2)
- 參數量: 117M
- 層數: 12
- 隱藏層維度: 768
- 注意力頭數: 12

### 學生模型 (Custom GPT-2)
- 參數量: 40M
- 層數: 6 (減少 50%)
- 隱藏層維度: 512 (減少 33%)
- 注意力頭數: 8 (減少 33%)

## 📝 技術細節

- **框架**: PyTorch + HuggingFace Transformers
- **訓練技術**: Mixed Precision Training (FP16)
- **優化器**: AdamW
- **學習率**: 5e-5 with warmup
- **批次大小**: 8
- **訓練輪數**: 3 epochs

## 🎓 學習重點

這個專案展示了：

1. **知識蒸餾的基本原理**: 如何讓小模型學習大模型的能力
2. **資料生成技巧**: 使用老師模型生成多樣化的訓練資料
3. **模型壓縮**: 在保持效能的同時大幅減少參數量
4. **評估方法**: 使用 Perplexity 量化語言模型效能
5. **實務應用**: 在資源受限環境下部署 LLM 的方法

## 📖 延伸閱讀

- [Distilling the Knowledge in a Neural Network (Hinton et al., 2015)](https://arxiv.org/abs/1503.02531)
- [DistilBERT: A distilled version of BERT (Sanh et al., 2019)](https://arxiv.org/abs/1910.01108)
- [HuggingFace Transformers Documentation](https://huggingface.co/docs/transformers/)

## ⚠️ 注意事項

1. **記憶體需求**: 確保有足夠的 GPU 記憶體（建議 16GB+）
2. **訓練時間**: 在 T4 GPU 上約需 15-20 分鐘
3. **隨機性**: 由於生成過程有隨機性，每次執行結果可能略有不同
4. **資料品質**: 老師模型的品質直接影響學生模型的學習效果

## 🤝 貢獻

歡迎提出 Issues 和 Pull Requests！

## 📄 授權

MIT License

## 👨‍💻 作者

這是一個教學示範專案，用於展示 LLM Knowledge Distillation 的完整流程。

---

**Happy Learning! 🚀**
