# Currency rates prediction

This repo contains my diploma project code on topic *"Comparative analysis of supervised learning algorithms in currency trading"* a.k.a. "Сравнительный анализ алгоритмов обучения с учителем в валютном трейдинге"

**Table of Contents**
- [](#)
- [About](#about)
- [What do files in this repo are trying to tell me?](#what-do-files-in-this-repo-are-trying-to-tell-me)
- [Motivation](#motivation)
- [Data preparation](#data-preparation)
- [Machine Leaning](#machine-leaning)
- [Trading part](#trading-part)
- [Results](#results)


## About

All this work is about **currency rates prediction** that is basicly time sires prediction problem. 
I used several architecture to solve it, afterwards I compared the results.  
Prediction were made based on **daily data from Forex for EURUSD pair**.  

Work itself consisted of several steps:
1. Reading related literature about currency trading
2. Reading some papers on ML in trading
3. Gaining the data and Making new features
4. Making Models and training them
5. Analyzing results
6. Improving Model

Last three steps were repeated several times.
A short description of some of the steps can be find below.

## What do files in this repo are trying to tell me?
Main files:
* Summary 
    * [Best Models](Best_models.ipynb) (may not be up to date)
* Working with Data
    * [Analysing data](Data_Preparation.ipynb)
    * [Making new features](Features_Engineering.ipynb)
* Models
    - [SVM](SVM.ipynb)
    - [Linear regression](Regressions.ipynb)
    - [Ensembles Classification](Ensembles_classification.ipynb)
    - [Ensembles regression](Ensembles.ipynb)
    - [RNN](RNN.ipynb) (just started to improve it)

---


## Motivation

**Personal motivation**  
As sphere is attached to with finance and people it surely has its own specific. Capturing this specificity was a real challenge. It was necessary to make some sort of understanding what's going on and only then collect the data, prepare it and make a bunch of models. So, I just have been doing everything from scratch - this is my first kinda big project.


**From papers**   
I've analized bunch of papers and that is the main conclusion that was made based on it: 
1. **It's got guaranteed that models will be profitable**
2. It's extrimely difficlut to predict what will hapend with currency rate during day due to random walk
3. Most profitable models are able to predict rate changes for the next 20 day
4. RNN and assembly seems to be most promising architectures

<!---
![](images/paper_1_models_stat.png)

![](images/paper_RNN_stat.png)  
Sourse: [Extreme Market Prediction for Trading Signal with Deep Recurrent Neural Network](https://www.researchgate.net/publication/325703947) 
-->

## Data preparation 

**Iinitial data** consists of historical Forex data from 19.01.2015 to 19.05.2021 for a currency pair EURUSD. That gives 1860 rows of data because the market closed on weekends. The raw data contained five classic metrics for each day: open, close, highest, lowest prices and volume.

I'm not an economist, nevertheless i've read couple of books on related topic. Moreower, supervisor of the diploma project is a professional currency trader.
He helped with **new features** selection so that they indicated such aspects of finantial time series as:

* General characteristics  – Bollinger bands
* Trend – Ichimoku Kinko Hyo, Vortex Indicator
* Volatility - Average True Range
* Momentum – Rate of Change

Most of indicators were taken for 20, 40, 60 and 120 days. More information about this can be found at *Features_Engineering.ipynb*.
**As a result get 24 columns and 1860 rows of data**.

## Machine Leaning

As title of the diploma says, The main purpose of this work is to compare several supervised leaning concepts. 
Specific of the task - prediction of finance data series - output of the models may be a real number or a digit from bounded set. 
That's why on the one hand problem may be treated as **regression task**. In this case model precuts the exact currency quotation. 
On the other hand, the problem is a **classification task**. Model's output is 1 for increasing quotation and -1 if it's falling. 

As a main **comparison parameter I used percentage of profitable deals** because This parameter is applicable for both regression and classification tasks. 
The most promising results were shown by Assembly methods.
Most of them has ~40% of profitable deals.  
**Core of the project** is a competition of all models architecture trained with best parameters found by greed search.

## Trading part

Simple trading algorithms was also made as a part of the project. This part is as simple as that: 
1. buy currency if price will increase tomorrow  
2. sell currency if price will decrease tomorrow and holding some
3. do nothing if it isn’t clear what will happen


---

## Results

Following list of models were tested:
- Linear Regression
- SVM
- Random Forest Classification (RFC)
- Random Forest Regression (RFR)
- Gradient Boostion Classification (GBC)
- Gradient Boosting Regressor (GBR)

MAX PD corresponds to the indicator of the maximum amount of profitable
transactions as a percentage of all deals. 

|   | accuracy  | precision |  recall |  MAE | MSE | RMSE | r2 |  Max PD, % |
|---|---|---|---|---|---|---|---|---|
| LR   | 0.69 | 0.75  | 0.7  | - | - | - | - | 40 | 
| SVM  | 0.72 | 0.72  | 0.84 | - | - | - | - | 40 |
| RFC  | 0.58 | 0.64  | 0.56 | - | - | - | - | 43 |
| GBC  | 0.65 | 0.67  | 0.71 | - | - | - | - | 48 |
| RFR  | -  | -  | -  | 0.48 | 0.24 | 0.49 | 0.033 | 32 |
| GBR  | -  | -  | -  | 0.46 | 0.23 | 0.48 | 0.05 | 40 |

Good news is Gradient boosting Classifier got 48% of profitable deals - this pretty close to making any profit, BUT STILL.  
Not good enough yet, work in progress.

<!---
## References

[1] [Predicting Stock Price Direction using Support Vector Machines](https://www.cs.princeton.edu/sites/default/files/uploads/saahil_madge.pdf) 
Saahil, M. Predicting Stock Price Direction using Support Vector Machines/ 
M. Saahil, B. Swati - Independent Work Report Spring, 2015. – 14 p.  

[2] [Extreme Market Prediction for Trading Signal with Deep Recurrent Neural Network](https://www.researchgate.net/publication/325703947) _Extreme_Market_Prediction_for_Trading_Signal_with_Deep_Recurrent_Neural_Network 
Zhichen, L. Extreme Market Prediction for Trading Signal with Deep Recur-
rent Neural Network/ L. Zhichen, L. Wen, G. Ying, - Beijing: Extreme Market Predic-
tion for Trading School of Economics and Management, 2018. – 10 p.  

[3] [Investigating Algorithmic Stock Market Trading using Ensemble Machine Learning Methods]() 
Khaled Sharif
Mohammad Abu-Ghazaleh
Ramzi Saifan 

[4] [Stock selection with random forest: An exploitation of excess return in the Chinese stock market](https://www.sciencedirect.com/science/article/pii/S2405844019359705)
Predicting Stock Price Direction using Support Vector
Machines
Zheng, T. Stock selection with random forest: An exploitation of excess re-
turn in the Chinese stock market/ T. Zheng, Y. Ziqin, Z. Guangwei – Sichuan: Institute 
of Chinese Financial Studies, 2019 – 10 p. 

[5] [Financial volatility trading using recurrent neural networks]()
Tino, P.: Financial volatility trading using recurrent neural networks/ P. Tino, 
G. Dorffner,  C. Schittenkopf – Vienna: Austrian Research University of Artificial In-
telligence, 2001 – 32 p. 

[6] Ładyżyński, P. [Stock Trading With Random Forests, Trend Detection Tests and Force IndexVolume Indicators]()/ P. Ładyżyński, K. Żbikowski, P.Grzegorzewski,- 
Warsaw: Warsaw University of Technology, 2013. – 12 p.   
-->


