# Credit Card Fraud Anamoly detection

Practice problem

Class Imbalance: 99.82 - 0.18

## preprocessing

Feature_engineering

added the following variables

'is_round' - derived from the decimal value of Amount - intuition "fraudster might prefer round number or stay away from round numbers. both will be reflected in the Amount variable"

log_amount - p1log transformation of amount variable to get it to normal distribution

Rest of the variables are masked and hence couldn't be creative with them

## Further Ideas

During initial analyses frauds seems to come in clusters with big spaces in between

![images/fraud_hm](https://github.com/Lohith-reddy/CreditCardFraud/assets/26896217/106b8aae-ef30-482a-b7ee-fecb1d003fde)

Moving average of frauds across Time

## Ideas for modelling

Unsupervised

1. Isolation Forest

2. Autoencoders

3. One-class SVM

Supervised

1. train a neural network - at first with an equal distribution of data at the start and gradually moving to the actual distributions in later training instances.

If supervised techniques are used, then data imbalance must be handled.

## Tactics for class imbalance

Undersampling

Oversampling

mixed-sampling - challenge is model learns a different distribution than the actual one

## comments on ideas

Autoencoders don't need oversampling as they don't look at minority class.

For isolation forest, oversampling might be counter-productive as the model tries to isolate anamolies. When spatial based imputing is done, it effectively means points are added near to other anamolies making it difficult for the isolation forest to isolate the points. However, dimensionality reduction might be a good idea. t-SNE is a good option.

One-class SVM might be a good idea after a feature reduction step through t-SNE or UMAP. Oversampling is needed.

Training a neural network with equal distibution at first and later moving to actual distribution is a decent idea. However, it is not my first choice right now. It's worth trying it but I wouldn't bet on it over others

### Results with Autoencoder

![images/loss_ae](https://github.com/Lohith-reddy/CreditCardFraud/assets/26896217/41f6fd4d-ec32-4dda-83c5-eb1a69b08eaf)

Ideally the thresh should be determined from the training data results
It should be selected in such a way that most of the fraud cases are caught while still keeping the false positives to a minimum.

i.e. maximise the fraud detection while minimising false positives

![images/threshold_chart](https://github.com/Lohith-reddy/CreditCardFraud/assets/26896217/e8365eea-b6c7-4a55-8a6a-a3e33720a476)

If we draw a vertical line at any threshold point we get the relevant fraud detection accuracy and the cost (false detection rate)

Since we are sensitive to fraud detection, we might want to capture a lot more fraud cases.
looking at the graphs 2.8 seems like a good number.

![images/image-1](https://github.com/Lohith-reddy/CreditCardFraud/assets/26896217/716fa464-db93-4a62-9143-e847d0082902)

### results with iForest

![images/image-3](https://github.com/Lohith-reddy/CreditCardFraud/assets/26896217/03a8abdd-4a8e-452d-8e64-1cfdf1a3a45d)

Though iForest seems to do a good job, it doesn't provide flexibility that autoencoders do. One cannot prioritise fraud detection over false-positives.
