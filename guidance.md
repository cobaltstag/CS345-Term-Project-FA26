I got this very sensible guidance from our grader when we submitted our proposal PDF:

1. Vectorization via TF-IDF should be after the test-train split and within a pipeline. This allows tuning TF-IDF hyperparameters in the same GridSearchCV with classifier hyperparameter tuning. It also prevents data leakage - the vocabulary and IDF weights should be learned from train data only.


2. You propose using a kernel with SVM as your baseline, but because the data is sparse and high-dimensional (tens of thousands of features from vectorization) a linear SVM (LinearSVC without kernel) may be more appropriate (and much faster).


3. F1 score by itself is by default the positive class F1 score so you'll want to score the GridSearchCV either on Macro F1 or negative class F1 by setting pos_label=-1 (to match your negative class label). Macro-F1 balances the two. 


4. Be sure not to look at the test set when assessing the baseline model accuracy. It's unclear from your proposal whether you intended to do this. Assess the baseline with cross_val_score or a validation split carved from the training portion. You can report the baseline’s test score at the end, next to the tuned model’s. Move forward with GridSearchCV regardless.