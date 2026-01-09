# FTC DECODE 自動計分系統

FTC (FIRST Tech Challenge) DECODE 2025-2026 賽季自動計分程式。透過影片分析，自動偵測場上的紫色和綠色球，計算各隊得分。

## 系統需求

- Java 17 或以上
- Maven 3.6+
- 作業系統：Windows / macOS / Linux

## 安裝

```bash
# 複製專案
git clone https://github.com/stevehelloworld/FTC-scoring.git
cd FTC-scoring

# 編譯
mvn clean compile
```

## 使用方式

### 啟動程式

```bash
mvn exec:java -Dexec.mainClass=com.telearn.ftc.ui.FTCMainWindow
```

### 操作步驟

1. **載入影片**
   - 點擊「載入影片」按鈕
   - 選擇比賽錄影檔案（支援 mp4, avi 等格式）

2. **標註球門區域**
   - 載入影片後，畫面會顯示第一幀
   - 選擇「藍方球門」，點擊「標註球門 (4點)」
   - 在畫面上依序點擊坡道的 4 個角點
   - 重複上述步驟標註「紅方球門」
   - 兩個球門都標註完成後，播放按鈕才會啟用

3. **播放與計分**
   - 點擊「播放」開始分析
   - 系統會自動偵測紫色和綠色球
   - 當球進入坡道區域時自動計分
   - 分數會即時顯示在右側面板

4. **其他功能**
   - 暫停/繼續：隨時暫停查看
   - 進度條：拖曳跳轉到指定時間
   - 重置計分：清除目前分數重新計算
   - 截圖：儲存當前畫面

## 計分規則

根據 FTC DECODE 2025-2026 規則：

- **CLASSIFIED**: 球進入坡道得 3 分
- 每個坡道最多容納 9 顆球
- 超過 9 顆會 OVERFLOW

## 專案結構

```
src/main/java/com/telearn/ftc/
├── model/          # 資料模型
│   ├── Alliance.java
│   ├── ArtifactType.java
│   └── DetectedArtifact.java
├── vision/         # 影像處理
│   ├── ArtifactDetector.java
│   ├── AprilTagDetector.java
│   └── BallTracker.java
├── scoring/        # 計分邏輯
│   └── ScoringEngine.java
└── ui/             # 使用者介面
    └── FTCMainWindow.java
```

## 技術說明

- **顏色偵測**：使用 HSV 色彩空間偵測紫色和綠色球
- **球追蹤**：最近鄰匹配法追蹤同一顆球的移動
- **區域判斷**：多邊形內點測試判斷球是否在坡道內

## 開發紀錄

詳見 [CHANGELOG.md](CHANGELOG.md)

## 授權

MIT License
