# Credit Card Fraud Anamoly detection

Class Imbalance: 99.82 - o.18

## Tactics for class imbalance

Undersampling

Oversampling

mixed-sampling - challenge is model learns a different distribution than the actual one

## Ideas for modelling

1. train a neural network - at first with an equal distribution of data at the start and gradually moving to the actual distributions in later training instances.

2. Isolation Forest

3. Autoencoders

4. One-class SVM

## comments on ideas

Autoencoders don't need oversampling as they don't look at minority class.

For isolation forest, oversampling might be counter-productive as the model tries to isolate anamolies. When spatial based imputing is done, it effectively means points are added near to other anamolies making it difficult for the isolation forest to isolate the points. Dimensionality reduction might be a good idea.

One-class SVM might be a good idea after a feature reduction step through t-SNE or UMAP. Oversampling is needed.

Training a neural network with equal distibution at first and later moving to actual distribution is a decent idea. However, it is not my first choice right now. It's worth trying it but I wouldn't bet on it over others

## Further Ideas

Moving average of frauds across Time

