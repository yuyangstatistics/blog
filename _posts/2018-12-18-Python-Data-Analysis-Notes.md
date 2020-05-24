---
title: Python Data Analysis Notes
date: 2018-12-18 12:28:12 -0500
categories: [Data_Science]
tags: [python]
---

1. Notes in STAT 8051 project

    - Dataset description
    ``` python
        train_data.describe(include=["object", "category"])
        train_data.info()
    ```

    - Check the number of NA values
    ``` python
        train_data.shape[0] - train_data.dropna().shape[0]
    ```

    - Set index
    ``` python
        train_data = train_data.set_index('claim_number')
    ```

    - Extract rows
    ``` python
        train_data.loc[train_data.annual_income==-1, 'annual_income'] = np.nan
    ```

    - Transform into categorical variables
    ``` python
        train_data["marital_status"] = pd.Categorical(train_data["marital_status"])
    ```

    - Print the list of missing columns
    ``` python
        print(list(itertools.compress(list(train_data), list(train_data.isna().any()))))
    ```

    - Use mean and mode to do imputation
    ``` python
        annual_income_mean = train_data.annual_income.mean()
        train_data['annual_income'].fillna(annual_income_mean, inplace=True)

        marital_status_mode = train_data.marital_status.mode().values[0]
        train_data['marital_status'].fillna(marital_status_mode, inplace=True)
    ```

    - One-hot encoding
    ``` python
        # one-hot encoding for state
        state_dummies = pd.get_dummies(test_data['state'],
                                    prefix='state', drop_first=True)
        test_data = pd.concat([test_data, state_dummies], axis=1)
        test_data.drop(["state"], axis=1, inplace=True)

        ### clean up variable names by making them all lowercase with underscore separators.
        train_data.columns = map(
            lambda s: s.lower().replace(' ', '_'), 
            train_data.columns
        )
    ```

    - Add grouped-by means as the new feature
    ``` python
        ## marital_status
        grouped_marital_status = train["fraud"].groupby(train['marital_status'])
        grouped_marital_status_mean = grouped_marital_status.mean().to_frame()
        grouped_marital_status_mean['marital_status']=grouped_marital_status_mean.index
        grouped_marital_status_mean['fraud_marital_status'] = grouped_marital_status_mean['fraud']
        grouped_marital_status_mean.drop('fraud', axis = 1, inplace = True)
        train = pd.merge(train, grouped_marital_status_mean, on = "marital_status", how = "left")
        test = pd.merge(test, grouped_marital_status_mean, on = "marital_status", how = "left")
    ```

    - Seperate dataset into training data and validation data
    ``` python
        ## generate row indexes
        random.seed(300)
        rindex =  np.array(sample(range(len(train)), round(0.7 * len(train))))

        train_df = train.iloc[rindex, :]
        validation_df = train.drop(train.index[rindex])
    ```

    - Drop a list of variables at once
    ``` python
        train_df.drop(["claim_year", "claim_day", "zip_code", "claim_date", "claim_number"], axis =1, inplace=True)
    ```

    - Show the head and tail of a dataframe
    ``` python
        data.head()
        data.tail()
    ```

2. Plots

    - Barplot with the values as the labels.
    ``` python
        import matplotlib.pyplot as plt; plt.rcdefaults()
        import numpy as np
        import matplotlib.pyplot as plt
        import matplotlib.axes as ax
        
        objects = ('Adaboost', 'Random Forest', 'Logistic Regression',
                'XGBoost', 'LightGBM', 'XGBoost_LightGBM')
        y_pos = np.arange(len(objects))
        performance = (0.719963411, 0.711689776, 0.709100835, 0.725387261,
                    0.729196909, 0.730128054)

        plt.figure(figsize=(8, 6))
        plt.ylim(0.70, 0.74)
        rects = plt.bar(y_pos, performance, align='center', alpha=0.5)
        plt.xticks(y_pos, objects)
        plt.xticks(rotation=30)
        plt.ylabel('AUC')
        plt.title('Model Performance')

        def autolabel(rects):
            for rect, perf in zip(rects, performance):
                height = rect.get_height()
                plt.text(rect.get_x() - rect.get_width()/6, 1.001*perf, '%s' % float(perf))
        autolabel(rects)

        plt.show()
    ```

    - Plot binned average
    ``` python
        grouped_safty_rating = train["fraud"].groupby(train['safty_rating'])
        grouped_safty_rating_mean = grouped_safty_rating.mean().to_frame()
        grouped_safty_rating_mean['safty_rating'] = grouped_safty_rating_mean.index
        plt.scatter(grouped_safty_rating_mean["safty_rating"], grouped_safty_rating_mean['fraud'])
        plt.xlabel("safty_rating")
        plt.ylabel("fraud rate")
    ```
