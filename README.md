# CH7-Serialcmd
硬體連接 (Wiring)
根據程式碼中的 #define 定義，請將 LED 連接至以下 GPIO 引腳
功能	GPIO 引腳	說明
Blink LED	GPIO 0	週期性閃爍指示燈
Binary LED 1	GPIO 2	二進位計數器 - 位元 0 (LSB)
Binary LED 2	GPIO 3	二進位計數器 - 位元 1
Binary LED 3	GPIO 4	二進位計數器 - 位元 2
Binary LED 4	GPIO 5	二進位計數器 - 位元 3 (MSB)
IO Agent LED	GPIO 15	外部觸發/通訊狀態指示燈
系統架構
程式採用模組化的 Agent 設計模式，各任務優先權配置如下：
MainThread	TASK_PRIORITY (1)	初始化硬體、啟動各 Agents 並循環列印系統狀態。
Blink	TASK_PRIORITY (1)	控制系統狀態燈。
Counter	TASK_PRIORITY (1)	計算並更新二進位隨機數值。
Decode	TASK_PRIORITY (1)	解析 Counter 數據並驅動 LED 顯示。
IO Agent	TASK_PRIORITY + 1 (2)	高優先權任務，確保輸入輸出響應無延遲。
透過 USB 序列埠（Serial over USB）輸出的統計資訊範例：
Plaintext
Number of tasks 5
Task: 1   cPri:1   bPri:1   hw:412   Blink
Task: 2   cPri:1   bPri:1   hw:380   Counter
Task: 4   cPri:2   bPri:2   hw:450   IO Agent
...
HEAP avl: 25600, blocks 12, alloc: 48, free: 36
