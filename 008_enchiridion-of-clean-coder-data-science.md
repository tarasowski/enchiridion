# Coding habits for data scientists

* The typical code to train ML models is written in Jupyter notebooks and it's
  full of side-effects (print, .head(), .show(), plots) the code exists without
  any abstractions, modularisation and automated tests.

* What contributes to complexity? "One of the most important techniques for
  managing software complexity is to design system so that developers only need
  to face a small fraction of the overall complexity at any given time.

* Something is complex when it's composed of interconnected parts. Following
  thing increase the complexity:
  - Not having abstractions: Writing code without abstracting it into functions
    or classes we force the reader to read many lines of code.
  - Long functions that do multiple things: This forces us to have to hold all
    the intermediate data transformations in our head.
  - Not having unit tests: When we refactor, the only way to ensure that we
    haven't broken anything is to restart the kernel and run the entire notbook
    (which is wrong)

* Strategies to reduce complexity:
  * Keep code clean
  * Use functions to abstract away complexity
  * Smuggle code out of Jupyter notebooks as soon as possible (not even try to
    write there)
  * Apply test driven development
  * Make small and frequent commits

* Clean code: you can see if the code isn't clean if it contains `dead code` ->
  code smell.

```py
# bad example
df = get_data()
print(df)

# do_other_stuff()
# do_some_more_stuff()

df.head()
print(df.columns)

# do_so_much_more_stuff()

model = train_model(df)

# good example
df = get_data()
model = train_model()
```
* Rules for clean code:
  1. Design: don't expose your internals (keep implementation details hidden)
  2. Dispensables: a) remove dead code, b) avoid print statements (e.g. print,
     .head(), .describe(), .plot())
  3. Variables: variable names should reveal intent
  4. Functions: a) use functions to keep code 'DRY', b) **functions should do one thing**

> Functions simplify our code by abstracting away complicated implementation
  details and replacing them with a simpler representation - its name.

```py
# bad example
pd.qcut(df['Fare'], q=4, retbins=True)[1]) # returns array

df.loc[df['Fare'] <= 7.90, 'Fare'] = 0
df.loc[df['Fare'] > 7.90 & (df['Fare'] <= 14.454), 'Fare'] = 1
df.loc[df['Fare'] > 14.454 & (df['Fare'] <= 31), 'Fare'] = 2
df.loc[df['Fare'] > 31, 'Fare'] = 3
df['Fare'] = df['Fare'].astype(int)
df['FareBand'] = df['Fare']

# good example (after refactoring into functions)
df['FareBand'] = categorize_column(df['Fare'], num_bins=4)
``` 

* What we gain by abstracting away the complexity into functions?
  1. Readability: We just have to read the interface (i.e. categorize_column())
     to know what's doing.
  2. Testability: Because it's now a function, we can easily write a unit test
     for it.
  3. Reusability: To repeat the same operation on any column we just need one
     line.

```py
# bad example
# https://github.com/davified/clean-code-ml/blob/master/notebooks/titanic-notebook-1.ipynb

# good example
df = impute_nans(df, categorical_columns=['Embarked'],
                     Continuous_columns=['Fare', 'Age'])

df = add_derived_title(df)
df = encode_title(df)
df = add_is_alone_columns(df)
df = add_categorical_columns(df)
X, y = split_features_and_labels(df)

# an even better example. Notice how this reads like a story
prepare_data = pipe([
                impute_nans,
                add_derived_title,
                add_is_alone_columns,
                add_categorical_columns,
                split_features_and_labels)

X, y = prepare_data(df)
```

> Our goal is to move code out of notebooks into Python modules and packages as
> early as possible.

* How do we move code out of Jupyter notebooks?

![Refactor](https://insights-images.thoughtworks.com/Screenshot202019101620at20100518_df186104d85da2fc7cd6080b96327600.png)

* As for testing that the actual machine learning part of the code works as we
  expect it to, we can write functional tests to assert that the metrics of the
  model (e.g. accuracy, precision, etc.) are above our expected threshold.

```py
# https://github.com/davified/clean-code-ml/blob/master/src/tests/test_model_metrics.py
import unittest
from sklearn.metrics import precision_score, recall_score

from src.train import prepare_data_and_train_model

class TestModelMetrics(unittest.TestCase):
  def test_model_precision_score_should_abe_above_threshold(self):
    model, X_test, Y_test = prepare_data_and_train_model()
    Y_pred = model.predict(X_test)
    
    precision = precision_score(Y_test, Y_pred)

    self.assertGreaterEqual(preceision, 0.7)

  def test_model_recall_score_should_be_above_threshold(self):
    model, X_test, Y_test = prepare_data_and_train_model()
    Y_pred = model.predict(X_test)

    recall = recall_score(Y_test, Y_pred)

    self.assertGreaterEqual(recall, 0.6)

```

* Make small and frequent commits:
  1. Reduced visual distractions and cognitive load
  2. No worries about breaking the code
  3. We can do red-red-red-revert. If we were to break something, we can easily
     fall back to checkout to the latest commit and try again

* Try to commit when there is a single group of logically related changes and
  passing tests.

> I'm not a great programmer; I'm just a good programmer with great habits ~
> Kent Beck

## Sources:
* [Coding habits for data scientists](https://www.thoughtworks.com/insights/blog/coding-habits-data-scientists)
