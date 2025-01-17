+++
title = "Trying (and failing) to build my own race predictor"
date = 2025-01-17
description = "Sometimes you just need more data"
draft = false

[taxonomies]
tags = ["machine-learning"]
+++

One of the core features I originally envisioned for [KineticAI](/pages/portfolio#KineticAI) was an automated race predictor.
My original idea was to essentially re-implement the [SuperPower Calculator](https://www.alextran.org/superpower-calculator/), using historical training data to calculate an individual running effectiveness value and Riegel exponent.
But I also wanted a project to learn more about machine learning, and race prediction seems like a textbook ML model - with enough data about how different aspects of training correlate with race times, it should be possible to train a highly accurate race prediction model.

# Data collection

The first problem was finding the data I'd need to train the model.
It took some digging, but I managed to find a [study](https://pmc.ncbi.nlm.nih.gov/articles/PMC5000509/) investigating the same problem that had publicly shared their data.
Once I downloaded the provided XLSX file, converted it to CSV, and decoded the cryptic column names, I was off to the races.

# First attempt

My first approach used XGBoost, a popular decision tree-based ML library.
To start out, I decided to train it to predict 10k times, and use other race times as model inputs - just as other predictors allow you to use past performance to predict future ones.
It was dead simple to set up:

```python
model = xgb.XGBRegressor(
    n_estimators=100,
    learning_rate=0.05,
    max_depth=4,
    min_child_weight=3,
    subsample=0.8,
    colsample_bytree=0.8,
    random_state=42,
    # Enable built-in missing value handling
    missing=np.nan,
    eval_metric=['rmse'],
)

model.fit(
    X_train, y_train,
    eval_set=[(X_train, y_train), (X_test, y_test)],
    verbose=True
)
```

Evaluated on the test set, this model had a mean absolute error (MAE) of about 190 seconds, or just over 3 minutes.
That's ... not great.
Could I do better with another approach?

# Neural network approach

In the spirit of learning, I next tried building a neural network-based predictor.
This model was a little bit more complex, though still nothing crazy:

```python
model = Sequential([

    layers.Input(shape=(input_dim,)),

    layers.Dense(64, activation='relu'),
    layers.BatchNormalization(),
    layers.Dropout(0.2),

    layers.Dense(32, activation='relu'),
    layers.BatchNormalization(),
    layers.Dropout(0.1),

    layers.Dense(1)
])

model.compile(
    optimizer=optimizers.Adam(learning_rate=0.001),
    loss='mean_squared_error',
    metrics=['mean_absolute_error']
)

early_stopping = keras.callbacks.EarlyStopping(
    monitor='val_loss',
    patience=10,
    restore_best_weights=True
)

history = model.fit(
    X_train, y_train,
    validation_data=(X_test, y_test),
    epochs=1000,
    batch_size=32,
    callbacks=[early_stopping],
    verbose=1
)
```

This set up a model with:

- 2 hidden layers
- Dropout in each layer randomly turning some neurons off to prevent overfitting
- Early stopping if model performance plateaued

The initial NN-based prediction had an MAE on the training set of 212 seconds (~3.5 minutes), and on the validation set of 189 seconds (~3 minutes).
In other words, it performed better in validation than in training!
This suggested that it was actually *under*fitting the data, and that the dropout values I had set were too high - the dropout could be reduced without causing overfitting.

I made a couple of tweaks to the model, one at a time, to try and improve its performance:

- Reduced dropout
- Added another hidden layer
- Dynamically adjusted the learning rate using `ReduceLROnPlateau`

After making these changes, the MAE was ... virtually identical.
Nothing I did - adjusting hyperparameters or switching model architectures entirely - seemed capable of producing a model more accurate than 3 minutes.

Looking at the data I had available, this really shouldn't have been surprising.
The dataset provided by the study only had about 2000 entries, about half of which included 10k times - so I only had 1000 data points to train from.
Given the number of features in the dataset and the inherent complexity of what determines race performance, it's clear that this simply wasn't enough data.

# Learning from failure

This was, unfortunately, the largest (and only) dataset of its kind I was able to find - no other public dataset exists that correlates running training with race performances.
As a result, I had no choice but to abandon the idea of an ML-based race predictor, at least until I'm able to find more data.

But I'm still glad I did this project!
It's been far too long since I did any machine learning work, and this was a fantastic way for me to re-introduce myself to the field.
It gave me the idea for my next project, modeling the impact on weather on running and cycling performance - a task for which I've generated ample data through hundreds of hours of outdoor activity.
In a narrow sense, building an ML-based race predictor was a failure.
But working on it taught me what I needed to know for my next project.
