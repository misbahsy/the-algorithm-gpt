[View code on GitHub](https://github.com/misbahsy/the-algorithm/trust_and_safety_models/nsfw/nsfw_media.py)

This code is designed to train a neural network model for classifying content as Not Safe For Work (NSFW) using TensorFlow and Keras. The model is trained on a dataset of preprocessed embeddings from Twitter data and evaluated on a separate test dataset. The code also includes hyperparameter tuning using Keras Tuner's Bayesian Optimization.

The main steps in the code are as follows:

1. Import necessary libraries and set up GPU configuration.
2. Define functions for decoding and preprocessing the input data.
3. Load and preprocess the training, validation, and test datasets.
4. Define the model architecture and compile it with appropriate loss function and metrics.
5. Perform hyperparameter tuning using Keras Tuner's Bayesian Optimization.
6. Train the best model on the training dataset and evaluate it on the validation dataset.
7. Save the trained model and upload it to Google Cloud Storage.
8. Evaluate the model's performance on the test dataset and plot the precision-recall curve.

The model architecture consists of a sequential neural network with Dense layers and BatchNormalization. The activation function, kernel initializer, and the number of layers are tuned using Keras Tuner. The model is compiled with the Adam optimizer and binary_crossentropy loss function. The performance metrics include PrecisionAtRecall and AUC (Area Under the Curve) for the precision-recall curve.

Example usage of the code in the larger project would involve training the model on a dataset of preprocessed embeddings from Twitter data, tuning the hyperparameters, and evaluating the model's performance on a separate test dataset. The trained model can then be used to classify new content as NSFW.
## Questions: 
 1. **Question**: What is the purpose of the `decode_fn_embedding` function and how does it work?
   **Answer**: The `decode_fn_embedding` function is used to decode the example protocol buffer from the input dataset. It defines the feature description with "embedding" and "labels" fields and then parses the example protocol buffer using `tf.io.parse_single_example` with the given feature description.

2. **Question**: What is the role of the `preprocess_embedding_example` function and how is it used in the code?
   **Answer**: The `preprocess_embedding_example` function is used to preprocess the input example dictionary by extracting the label and embedding from the example. It checks if the label is equal to the positive label and casts it to an integer. The function returns the features (embedding) and the label as a tuple. It is used in the code when mapping the input datasets (train_ds, test_ds, eval_ds, etc.) to preprocess the examples.

3. **Question**: How does the hyperparameter tuning work in this code and what are the hyperparameters being tuned?
   **Answer**: The hyperparameter tuning is done using Keras Tuner's Bayesian Optimization. The `build_model` function is defined to create a Sequential model with hyperparameters such as activation function, kernel initializer, number of layers, and units in each layer. The tuner is then set up with the build_model function, objective function (minimizing validation loss), and other configurations. The tuner searches for the best hyperparameters by training the model on the train_ds dataset and validating on the eval_ds dataset.