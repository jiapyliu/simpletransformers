---
title: Binary Classification
permalink: /docs/binary-classification/
excerpt: "Binary text classification."
last_modified_at: 2020-05-02 17:58:16
---

The goal of binary text classification is to classify a text sequence into one of two classes. A transformer-based binary text classification model typically consists of a transformer model with a classification layer on top of it. The classification layer will have two output neurons, corresponding to each class.

**Tip:** Refer to [ClassificationModel](/docs/classification-models/#classificationmodel) for details on configuring a classification model.
{: .notice--success}

## Minimal Start

```python
from simpletransformers.classification import ClassificationModel
import pandas as pd
import logging


logging.basicConfig(level=logging.INFO)
transformers_logger = logging.getLogger("transformers")
transformers_logger.setLevel(logging.WARNING)

# Preparing train data
train_data = [
    ["Aragorn was the heir of Isildur", 1],
    ["Frodo was the heir of Isildur", 0],
]
train_df = pd.DataFrame(train_data)
train_df.columns = ["text", "labels"]

# Preparing eval data
eval_data = [
    ["Theoden was the king of Rohan", 1],
    ["Merry was the king of Rohan", 0],
]
eval_df = pd.DataFrame(eval_data)
eval_df.columns = ["text", "labels"]

# Optional model configuration
model_args = {
    "num_train_epochs": 1,
}

# Create a ClassificationModel
model = ClassificationModel(
    "roberta", "roberta-base", args=model_args
)

# Train the model
model.train_model(train_df)

# Evaluate the model
result, model_outputs, wrong_predictions = model.eval_model(eval_df)

# Make predictions with the model
predictions, raw_outputs = model.predict(["Sam was a Wizard"])

```
