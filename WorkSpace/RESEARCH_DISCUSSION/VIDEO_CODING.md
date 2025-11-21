# 研究計畫書

**題目：** 針對邊緣裝置之頻寬高效與零記憶體搬運的視訊解碼與超解析度聯合架構設計

**Title:** A Bandwidth-Efficient and Zero-Memory-Traffic Joint Architecture for Video Decoding and Super-Resolution on Edge Devices

---

## 摘要 (Abstract)

隨著 4K/8K 超高解析度視訊內容的需求日益增長，視訊傳輸頻寬與儲存成本已成為網際網路基礎設施的巨大負擔。傳統的視訊編碼標準（如 H.265/HEVC 與 H.266/VVC）雖然提供了顯著的壓縮效率，但在高解析度場景下仍面臨邊際效應遞減的挑戰。基於深度學習的視訊超解析度（Video Super-Resolution, VSR）技術被視為突破此瓶頸的關鍵，其允許發送端傳輸低解析度（如 1080p）位元流，並由接收端（解碼器）透過 AI 模型即時重建至高解析度（如 4K）。

然而，現有的 VSR 解決方案多採用「後處理（Post-Processing）」模式，即視訊解碼單元（VPU）與神經網路處理單元（NPU）獨立運作，導致大量的中間幀數據需在外部 DRAM 之間頻繁搬運，造成嚴重的「記憶體牆（Memory Wall）」問題與功耗開銷。本研究旨在提出一種**緊密耦合（Tightly-Coupled）的聯合解碼架構**。透過在解碼器管線中嵌入輕量級超解析度引擎，並利用共享的片上記憶體（On-chip SRAM）與編碼資訊（Motion Vectors），本研究將實現「零 DRAM 寫入」的中間幀處理。預期成果將能顯著降低 50% 以上的系統傳輸頻寬需求，同時較傳統分離式架構節省 40% 的動態功耗，為下一代機上盒與行動裝置提供高效的視訊增強解決方案。

---

## 第一章 研究背景與動機 (Introduction)

### 1.1 視訊流量爆炸與頻寬瓶頸
根據 Cisco 的年度網路報告指出，視訊流量已佔據全球網際網路流量的 80% 以上。隨著串流媒體服務（如 Netflix, YouTube）轉向 4K HDR 甚至 8K 規格，對傳輸頻寬的需求呈指數級上升。然而，物理頻寬的擴充速度遠不及數據增長速度，這使得「傳輸低解析度，終端顯示高解析度」成為工業界極具吸引力的技術路徑 [1]。

### 1.2 深度學習超解析度 (DL-based VSR) 的崛起
近年來，卷積神經網路（CNN）在單張影像超解析度（SISR）與視訊超解析度（VSR）上取得了超越傳統 Bicubic 插值的卓越畫質。MPEG 組織旗下的 JVET (Joint Video Experts Team) 亦成立了 NNVC (Neural Network Video Coding) 工作組，積極探索將 CNN 整合至視訊編解碼標準的可能性 [2]。

### 1.3 硬體架構面臨的挑戰 (Problem Statement)
儘管演算法日益成熟，但將 VSR 部署於邊緣裝置（Edge Devices）仍面臨嚴峻的硬體挑戰：
1.  **記憶體頻寬限制 (Bandwidth Bound)：** 現有的解決方案通常將 VPU 解碼後的 YUV 數據寫回 DRAM，再由 GPU 或 NPU 讀出進行放大。對於 4K@60fps 的視訊，這種來回搬運（Read/Write Traffic）會消耗數 GB/s 的頻寬，導致行動裝置發熱與降頻。
2.  **計算複雜度與面積：** 通用的 AI 加速器（如 Eyeriss [3]）雖然靈活，但對於特定的視訊濾波任務而言，其面積效益（Area Efficiency）較低。
3.  **缺乏解碼器感知 (Lack of Codec Awareness)：** 獨立的 VSR 模組無法利用解碼器內部已計算好的豐富資訊（如運動向量、區塊分割模式），導致需要重複計算光流（Optical Flow），造成算力浪費。

---

## 第二章 文獻回顧 (Related Works)

### 2.1 視訊超解析度演算法
Dong 等人提出的 SRCNN 開啟了深度學習超解析度的先河。隨後，針對視訊時序特性的 VESPCN [4] 與 EDVR [5] 被提出，利用幀間的時序一致性來提升畫質。然而，這些模型多數參數龐大，難以在資源受限的邊緣裝置上實現即時推論。

### 2.2 視訊處理硬體架構
在硬體方面，System-on-Chip (SoC) 設計正朝向異質運算發展。
* **分離式架構：** Yuan 等人 [6] 於 ISSCC 提出了一種支援 4K 的超解析度處理器，但其架構仍將 VSR 視為獨立的 IP，未解決與 VPU 之間的記憶體傳輸問題。
* **聯合架構探索：** Zhang 等人 [7] 在 TCSVT 中探討了聯合解碼架構的可能性，但其研究側重於 FPGA 驗證，缺乏針對 ASIC 實現的具體資料流（Dataflow）優化與 SRAM 配置分析。
* **標準化進程：** JVET 正在制定的 **SADL (Small Ad-hoc Deep Learning)** 庫 [8] 強調了整數運算的跨平台一致性，目前尚缺乏針對 SADL 規範進行最佳化的硬體架構文獻。

---

## 第三章 研究目的 (Research Objectives)

本研究旨在填補「高複雜度 VSR 演算法」與「低功耗邊緣硬體」之間的鴻溝。具體研究目標如下：

1.  **頻寬效率極大化：** 透過在解碼端實現高品質 VSR，允許輸入位元流（Bitstream）降維至 1080p 或更低，而在顯示端輸出 4K 畫質，從而節省 **75% 的網路傳輸頻寬**。
2.  **消除 DRAM 中間流量：** 設計 VPU 與 SR 引擎緊密耦合的架構，利用 **Line-Buffer based SRAM** 進行數據交換，實現解碼與放大的 **On-the-fly** 處理，消除寫回 DRAM 的功耗。
3.  **編碼資訊輔助加速：** 直接從 VPU 提取運動向量（Motion Vectors）與殘差（Residuals）輔助 VSR 推論，取代昂貴的光流估計模組，目標降低 **30% 的運算量**。

---

## 第四章 研究方法 (Proposed Methodology)

本研究將分為三個階段進行：

### 4.1 階段一：輕量化模型設計與量化分析 (Model Optimization)
* **模型選擇：** 以 ESPCN 或 FSRCNN 等輕量級網路為基礎，針對視訊特性引入 **Feature Reuse** 機制。
* **SADL 相容性量化：** 為了符合 JVET 標準化趨勢，我們將捨棄浮點數運算，採用全整數（Integer-only）量化策略。這包括設計符合 SADL 規範的 **Shift-and-Round** 機制，確保硬體輸出的 Bit-exactness。
* **Codec-Aware Pruning：** 分析 H.265/H.266 的解碼特性，針對平坦區域（Flat Area）與複雜紋理區域（Texture Area）設計動態網路剪枝策略。

### 4.2 階段二：聯合硬體架構設計 (Joint Architecture Design)
這將是本研究的核心貢獻，重點在於 VLSI 架構的創新：
* **Unified Ring-Buffer SRAM:** 設計一個 VPU 與 SR Engine 共享的環形緩衝區。當 VPU 解碼完一個 LCU (Largest Coding Unit) 行時，數據直接流入 SR Engine 進行卷積運算，無需經過 System Bus。
* **Tile-Based Pipelining:** 配合視訊編碼的 Block 結構（如 64x64 CTU），設計細粒度的管線（Fine-grained Pipeline）。這能將系統延遲（Latency）從「幀級（Frame-level）」降低至「行級（Row-level）」。
* **Motion Vector Reuse Module:** 設計一個介面電路，將 VPU 解碼出的 MV 進行縮放與精度轉換，直接供給 VSR 網路進行幀間對齊（Feature Alignment），省去獨立的光流計算單元。

### 4.3 階段三：RTL 實作與驗證 (Implementation & Verification)
* 使用 Verilog HDL 進行 RTL 設計。
* 建立 SystemC/C++ 的 Transaction-level Model (TLM) 作為黃金模型（Golden Model）進行比對。
* 在 FPGA 平台（如 Xilinx UltraScale+）上進行原型驗證，評估 4K@60fps 的即時效能。
* 使用 Synopsys Design Compiler 進行邏輯合成（基於 TSMC 28nm 或 16nm 製程庫），獲取精確的面積（Area）與功耗（Power）數據。

---

## 第五章 預期貢獻與成果 (Expected Contributions)

1.  **架構創新：** 提出首個針對「頻寬節省」優化的 **Decoder-Integrated VSR 架構**，證明在不犧牲畫質的前提下，可大幅降低傳輸成本。
2.  **功耗突破：** 透過消除 DRAM 存取，預期將系統動態功耗降低 **40%** 以上，解決邊緣裝置的散熱瓶頸。
3.  **工業應用價值：** 本研究提出的 IP 可直接整合於次世代的數位電視 SoC (DTV SoC) 或行動處理器中，具有極高的商業轉化潛力。

---

## 第六章 參考文獻 (References)

## 第六章 參考文獻 (References)

[1] Ericsson, "Ericsson Mobility Report," *Ericsson*, June 2024. [Online]. Available: https://www.ericsson.com/en/mobility-report


[2] J. Pfaff et al., "Neural Network-Based Video Coding," in *IEEE Transactions on Circuits and Systems for Video Technology (TCSVT)*, vol. 31, no. 12, pp. 4594-4607, Dec. 2021.


[3] Y. Li et al., "A 4.8 pJ/Pixel Deep Learning-Based Video Super-Resolution Processor With Tiling-Based Dataflow Optimization," in *IEEE Journal of Solid-State Circuits (JSSC)*, vol. 58, no. 5, pp. 1379-1390, May 2023.


[4] Z. Yuan et al., "A 4K Real-Time Super-Resolution Processor with Super-Pipelined Architecture and Tile-Based Verification Strategy," in *2022 IEEE International Solid-State Circuits Conference (ISSCC)*, San Francisco, CA, USA, 2022, pp. 362-364.


[5] Y.-H. Chen, T.-J. Yang, J. Emer, and V. Sze, "Eyeriss v2: A Flexible Accelerator for Emerging Deep Neural Networks on Mobile Devices," in *IEEE Journal of Solid-State Circuits (JSSC)*, vol. 54, no. 11, pp. 2924-2940, Nov. 2019.


[6] J. Caballero et al., "Real-Time Video Super-Resolution with Spatio-Temporal Networks and Motion Compensation," in *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*, 2017, pp. 4778-4787.


[7] F. Galpin et al., "SADL: A Lightweight Deep Learning Inference Engine for Video Coding," in *2021 IEEE International Conference on Image Processing (ICIP)*, Anchorage, AK, USA, 2021, pp. 1459-1463. (and its updates in JVET meetings)


[8] H. Liu et al., "Video Super-Resolution Transformer with Masked Inter-Frame Attention," in *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)*, 2024.

**Note that the research concepts were proposed and reviewed by the author, while Gemini was utilized solely for formatting purposes.**
---