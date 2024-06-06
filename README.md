# Temporal_CNN

## Convolutional Neural Networks
<img src="https://github.com/colurw/temporal_CNN/assets/66322644/100a003f-288d-4e00-98b7-de1f8aecf0ac" align="right" width="300px"/>

Convolutional Neural Networks (CNN's) are commonly used in image classifcation tasks because they are able to take into account the spatial structure of an image.  This contrasts with a standard neural network, which would treat every pixel as an independent feature.

Just as a 2-D image has red, green and blue channels (which are best interpreted when analysed together) a price-data time-series can be assigned channels representing open/high/low/close prices, and traded volume.

By treating a price-data time-series as a 1-dimensional image, we hope to improve the model's ability to recognise temporal correlations, and therefore predict profitable trading opportunities.  

Whilst attempting to predict price movements is a hard problem due to the highly stochastic nature of markets, even weak models can provide enough of a 'gambler's edge' to be profitable, assuming a large enough number of trades, and providing certain caveats are accounted for.

## Multi-modal Networks 

It may be true that markets behave differently at different times of the day or week.  By expanding the index of the time series into a one-hot encoded categorical dataset, we can feed this into a separate branch of the CNN, in the hope of increasing its predictive power. <br clear="right"/>

## 1_data_preparation.py

Converts 'open-high-low-close' (OHLC) price data into a format suitable for machine learning.  It uses the variance, first-order filters, and significant levels to extract learnable features from the raw data.

Target labels are generated according to (potential) profitable trading conditions being met, whilst time and day labels are separated out and one-hot encoded.  

The working dataframe is then transformed into a tensor of dimensions [batch_size, steps, channels] by using a rolling window.  Appropriate target labels are selected to match the last timestep in each window, and transformed into a tensors of dimensions [batch_size, categories].

## 2_train_model.py
<img src="https://github.com/colurw/temporal_CNN/assets/66322644/7c7c89df-c071-48b1-8361-8ca29ae1142b" align="right" width="500px"/>
Defines the neural network, trains it on the prepared data, then assesses the predictive abilities of the model by generating precision-recall graphs for each class ('market up' and 'market down'). <br>
<br>
We can see there are no prediction thresholds where the model is able to unambigously identify the positive class... This is unsurprising given the highly stocastic nature of market movements.  <br>
<br>
However, it also shows that the model does have a small edge over random guesswork, which may be exploitable given a number of suitably sized/risk-adjusted positions. <br>
<br>
Many potential optimisations of the model and training data can also be explored, in particular the predictive lengths and time-series 'bucket' sizes. <br clear="right"/>

## To Do list

<<<<<<< HEAD
Calculate profit factor and drawdown for chosen thresholds, and including commision costs.
=======
* Calculate profit factor and drawdown for chosen thresholds, and including commision costs.
* Improve trade closing routines with stops, as opposed to a fixed time period.
>>>>>>> 98b6b2dcfb1a0d14b783fb113ccbfd837d49b3e7

