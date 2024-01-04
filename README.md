# 技術報告

## 技術指標：

### 相對強弱指標 (Relative Strength Index, RSI)
⼀種⽤來衡量⼀個⾦融資產在某⼀段時間內的價格變化強度和速度的技術指標。RSI是由威爾斯·威爾德（Welles Wilder）於1978年⾸次引入的，它的主要⽬的是幫助交易者判斷⼀個資產是處於超買還是超賣的狀態，RSI的範圍在0到100之間。通常，RSI值⾼於70被視為超買，RSI值低於30被視為超賣(參數依情況⽽有所不同)，超買表⽰資產可能已經過度升值，⽽超賣表⽰資產可能已經過度貶值，交易者通常使⽤RSI的這些區域來識別潛在的反轉點，RSI超過70或低於30可能表⽰市場過熱或過冷，進⽽產⽣趨勢反轉的信號。本次策略便是使⽤RSI作為趨勢反轉信號。ꢀ

### 指數平滑異同移動平均線 (Moving Average Convergence & Divergence,MACD)
⼀種⽤來分析資產價格變動⽅向和強度的技術指標。MACD由傳奇的技術分析師威爾斯·威爾德（Welles Wilder）於1979年⾸次引入，它結合了兩個指數平滑移動平均線，以及⼀個稱為「差離值」（Divergence）的柱狀圖。MACD的主要組成部分:

1\. 快速移動平均線（MACD Line）： 這是由較短期間內的平均價格計算⽽得的⼀條曲線。通常使⽤12天的價格平均來計算。

2\. 慢速移動平均線（Signal Line）： 這是由較長期間內的平均價格計算⽽得的另⼀條曲線。通常使⽤26天的價格平均來計算。

3\. 差離值（Histogram）： 這是MACD Line和Signal Line之間的差異，以柱狀圖的形式呈現。差離值的計算為MACD Line減去Signal Line。MACD的主要⽤途是測量趨勢的強弱。當MACD Line位於Signal Line之上，可能表⽰市場處於多
頭趨勢（bullish）；反之，當MACD Line位於Signal Line之下，可能表⽰市場處於空頭趨勢。

布林通道（Bollinger Bands）：⼀種⽤來衡量價格波動性和價格趨勢的技術指標，由約翰·布林格（John Bollinger）於1980年提出。它由三條線組成，上中下三條線分別是：ꢀ

1\. 上軌（Upper Band）: 這是以移動平均數加上兩倍標準差所計算的上限。上軌反映了價格的⾼波動性和趨勢的強度。ꢀ

2\. 中軌（Middle Band）: 這是價格的N⽇移動平均線。N通常設定為20，但可以根據交易者的需求進⾏調整。ꢀ

3\. 下軌（Lower Band）: 這是以移動平均數減去兩倍標準差所計算的下限。下軌反映了價格的低波動性和趨勢的強度。ꢀ

當價格突破布林帶的上軌時，這可能表明價格處於過度買入的狀態，即超過市場的期望，從逆勢觀點來看，股價會回歸均值，並在均值上下徘徊，因此認為市場已經過度激動，可能會發⽣反轉。相對的，當價格突破布林帶的下軌時，這可能表明價格處於過度賣出的狀態，即市場情緒過於悲觀，市場可能會反轉。

## 策略概述：

這個策略的⽬標是在市場的過度賣出或過度買入情況下，並結合趨勢指標和動能指標的信號，進⾏逆勢操作。該策略結合了相對強弱指標 (RSI) 、指數平滑異同移動平均線 (MACD)和布林通道（Bollinger Bands）來進⾏交易決策。具體來說，當RSI低於過賣標誌、MACD柱狀圖為正並且股價低於布林帶的下界時，策略會進⾏買入操作。相反，當RSI⾼於過買標誌、MACD柱狀圖為負並且股價⾼於布林通道的上界時，策略會進⾏賣出操作。 在其中以rsi指標作為主要的動能指標，⽤以判斷趨勢反轉的可能性，⽽macd則做為輔助的動能指標確認rsi指標的信號是否正確，並由布林通道確定趨勢反轉的位置。

## 參數優化：

本次參數優化使⽤Optuna，Optuna是⼀個⽤於超參數優化的函式庫，它通常⽤於機器學習模型，但同樣適⽤於參數調優。

## 參數設置（優化後結果）：

RSI週期（rsi\_period）：11（⼀般設置為14）
RSI過賣標誌（rsi\_oversold）：40（⼀般設置為30）
RSI過買標誌（rsi\_overbought）：83（⼀般設置為70）
MACD短週期（macd\_short\_period）：11（⼀般設置為12）
MACD長週期（macd\_long\_period）：35（⼀般設置為26）
MACD信號線週期（macd\_signal\_period）：9（⼀般設置為9）
BBANDS週期（time\_lenght）:10（⼀般設置為20）

## 交易條件：

### 買入條件
RSI低於過賣標誌、MACD柱狀圖為正並且股價低於布林帶的下界。

### 賣出條件
RSI⾼於過買標誌、MACD柱狀圖為負並且股價⾼於布林帶的上界。

## 回測結果：

Start                     		2017-01-02 02:00:00<br />
End                       		2022-12-30 16:58:00<br />
Duration                  		2188 days 14:58:00<br />
Exposure Time [%]      	      99.980148<br />
Equity Final [$]             	132956842.774846<br />
Equity Peak [$]             	133175101.834326<br />
Return [%]                    32.956843<br />
Buy & Hold Return [%]       	1.772032<br />
Return (Ann.) [%]             3.895633<br />
Volatility (Ann.) [%]         3.449552<br />
Sharpe Ratio                 	1.129316<br />
Sortino Ratio                 1.968533<br />
Calmar Ratio                 	1.038283<br />
Max. Drawdown [%]           	-3.751996<br />
Avg. Drawdown [%]           	-0.117821<br />
Max. Drawdown Duration        975 days 19:30:00<br />
Avg. Drawdown Duration       	2 days 02:27:00<br />
#Trades                     	6<br />
Win Rate [%]                  100.0<br />
Best Trade [%]               	11.723222<br />
Worst Trade [%]              	0.140024<br />
Avg. Trade [%]               	7.384097<br />
Max. Trade Duration         	975 days 14:03:00<br />
Avg. Trade Duration         	417 days 19:14:00<br />
Profit Factor                	NaN<br />
Expectancy [%]               	7.446673<br />
SQN                          	2.160243<br />
_strategy                 		OptimizedStrategy<br />
_equity_curve                	...<br />
_trades                      	Size  En...<br />
dtype: object<br />


## 策略優點：

### 多重指標過濾
結合多個指標可以增加對市場狀況的全⾯理解。RSI可以提供超買和超賣信號，MACD⽤於捕捉趨勢變化，⽽ Bollinger Bands 可以顯⽰趨勢反轉的位置。
### 提⾼準確性
這種結合可以在多個層⾯上確認交易信號，從⽽提⾼交易系統的準確性。例如，當 RSI 顯⽰超買時，同時 MACD 顯⽰趨勢轉變並且價格位於 Bollinger Bands 的邊緣時，可能會更有⼒的信號。

## 策略缺點：

### 忽略趨勢
若策略偏向逆勢操作，主要關注超買或超賣條件，⽽較為忽略了趨勢的⽅向，它可能在強勢或弱勢趨勢中錯失潛在的利潤機會。趨勢追踪有助於捕捉並參與市場的長期趨
勢。
### 提⾼綁定條件過多
由於結合多個指標，因此交易次數偏低，在部分極端情況下可能導致交易次數為零。


