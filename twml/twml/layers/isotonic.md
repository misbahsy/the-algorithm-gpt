[View code on GitHub](https://github.com/misbahsy/the-algorithm/twml/twml/layers/isotonic.py)

The Isotonic layer is a type of layer used in machine learning models for calibration of probabilities. It is typically used instead of sigmoid activation on the output unit. The purpose of this layer is to calibrate the probabilities output by a model to make them more accurate. 

The Isotonic layer takes in several arguments, including the number of input units to the layer (which is the same as the number of output units), the number of bins used for isotonic calibration, and tensors containing the boundaries of the bins and calibrated values for the corresponding bins. The output of the layer is a layer containing calibrated probabilities with the same shape and size as the input. 

The Isotonic layer is created by the IsotonicCalibrator and is used to improve the accuracy of machine learning models. It is particularly useful in situations where the probabilities output by a model are not well-calibrated, meaning that they do not accurately reflect the true probabilities of the events being predicted. 

Here is an example of how the Isotonic layer might be used in a machine learning model:

```
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from TheAlgorithmFromTwitter import Isotonic

model = Sequential()
model.add(Dense(64, activation='relu', input_dim=100))
model.add(Dense(1, activation='sigmoid'))
model.add(Isotonic(n_unit=1, n_bin=10))
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```

In this example, the Isotonic layer is added to the model after the output layer. This will calibrate the probabilities output by the model to make them more accurate. The n_unit and n_bin arguments are set to 1 and 10, respectively, which means that the Isotonic layer will have one input and one output, and will use 10 bins for calibration. 

Overall, the Isotonic layer is an important tool for improving the accuracy of machine learning models by calibrating the probabilities output by the model.
## Questions: 
 1. What is the purpose of the Isotonic layer and how is it typically used?
- The Isotonic layer is typically used instead of sigmoid activation on the output unit, and it contains calibrated probabilities with the same shape and size as the input.
2. What are the expected sizes and types of the xs_input and ys_input tensors?
- The expected sizes of xs_input and ys_input are [n_unit, n_bin], and their expected types are the same as the input.
3. Why is the compute_output_shape method raising a NotImplementedError?
- It is unclear why the compute_output_shape method is raising a NotImplementedError, as there is no explanation or implementation provided in the code.