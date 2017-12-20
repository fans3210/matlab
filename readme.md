## 20171219
## fix the ranking model we have


Using my simulated data (alpha vector=[23 4 2 1]), extract the Bayesian moment matching part code from the published code of CrowdBT, tune the parameters alpha 8 beta 2.   Result: converge quickly, get about 90% accuracy.


Baby face branch -- Using the baby face data set, my previous CrowBT method also gets a reasonable result 85% -- even though the data is not sufficient as the paper used, and the ground truth is generated by myself ranking the whole 18 baby faces. If I get the original ground truth data, the accuracy can be higher. 

Based on the prject code struct, replace the BMM part with that of OnlineBT, and OnlinePL, also get a good result, accuracy is higher than 90%.  

But ROPAL still can not get that accuracy. Finally, with the support of Yuangang, I know the trick of initialisation of the parameters about ROPAL.

In conclusion, the 4 ranking models to process my simulated data (alpha vector=[23 4 2 1]) have accuracy about 90%.

the accuracy of the 4 ranking models to aggregate my simulated data (alpha vector=[23 4 2 1])
![Image of the 4 ranking model accuracy](https://github.com/TaoStarlit/matlab/blob/master/ACML_Code/reOrganizeExpert/4%20Method%20accuracy-budget.png)


## experiments of EEG
Although I have doubt upon the data, I do some experiments, assuming the data is all right.

FFT of each subject each channel each trails
(Of course, before processing all the data set, I had test the way I get the single sided amplitude spectrum is all right: 
https://github.com/TaoStarlit/matlab/blob/master/BCIprocessedData/test_Amplitude_Spectrum.m)


From the last graph of figure 4, in the paper: identifying changes in EEG information transfer during drowsy driving by transfer entropy.
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4615826/figure/F4/
In most channels, (the author only chose 6 channels, but including all front-centre-left-right-top-behind region), the power of beta(13-20hz) has negative relation with DP(normalised reaction time). 
So I do experiments to aggregate the beta preference, in order to rank the RT, then get the quality of each channel (detect the noised workers). But the accuracy is never larger than 60% or less than %40, so there are nearly no relation with beta Powder and DP based on the data we have.
https://github.com/TaoStarlit/matlab/blob/master/BCIprocessedData/DetectNoise.m
Even I extract the data whose DP<2, (from 1st graph of figure 4,the power of Delta is totally positive relation to the DP.) but the results is still not good.
https://github.com/TaoStarlit/matlab/blob/master/BCIprocessedData/DPless2file.m

Using rank correlation coefficient to find the top related channels of each data files(one data file at most have only one subject) with respect of DP and energy-delta-theta-alpha-beta, save the channel number, correlation coefficients and the data source files' name in https://github.com/TaoStarlit/matlab/blob/master/BCIprocessedData/corr/top3chs_PowerOfBand.mat
But the result is unreasonable, because the top 3 related channels with DP of each file (same subject), is varied. And I asked Avi, the explaination about the data has many inconsistency from the paper or even our previous discussion.

In conclusion, I do some experiments(amplitude spectrum, aggregation, correlation analysis), assuming the data and its explaination is all right.  The code is ready, so once there is no problem or inconsistency in the data or its explaination, I can the reasonable result.




## 2017120x
## for the ROPAL Ranking
As the simulated datas of origin source code are not found now, I must generate the data by myself, need repeated comfirm with the Auther.

Finish: generate 3-ray perference <-- eta of W work, (ground-true) Scores of L object. each worker has T task of annotating the 3-ray object.

But using the data, I run the original project, the performance was not very well, so must comfirm the data again with the Auther


## Pairwise Crowdsource Ranking

1. 10 object VS many many echochs of EEG:
    计划，里面10个object，现在试着对第0个替换新的数据（theta0），然后重新训练（mu sigma try result 通通都要更新）
    显示他们的mu
1. 完成从数据文件，转化为频谱图信息（频率点，赋值 -- Frequence Amplitude），可以选择去掉高频，减少数据量
    多次测试过频谱函数；可一选择处理过程画出频谱图
