[View code on GitHub](https://github.com/misbahsy/the-algorithm/twml/twml/contrib/layers/hashed_percentile_discretizer.py)

The `HashedPercentileDiscretizer` layer is a part of the `The Algorithm from Twitter` project and is used to convert sparse continuous features to sparse binary features. This layer is constructed by `PercentileDiscretizerCalibrator` after accumulating data and performing minimum description length (PercentileDiscretizer) calibration. The layer takes sparse continuous features and converts them to sparse binary features. Each binary output feature is associated with a `HashedPercentileDiscretizer` bin. Each `HashedPercentileDiscretizer` input feature is converted to `n_bin` bins. Each `HashedPercentileDiscretizer` calibration tries to find bin delimiters such that the number of feature values per bin is roughly equal (for each given `HashedPercentileDiscretizer` feature). 

The layer is useful when an input feature is rarely used, so will its associated output bin/features. The difference between this layer and `PercentileDiscretizer` is that the `DeterministicPercentileDiscretize` always assigns the same output id in the `SparseTensor` to the same input feature id + bin. This is useful if you want to use transfer learning on pre-trained sparse to dense embedding layers but re-calibrate your discretizer on newer data.

The layer is initialized with `n_feature`, `n_bin`, `out_bits`, `bin_values`, `hash_keys`, `hash_values`, `bin_ids`, `feature_offsets`, and `hash_fn`. The `n_feature` is the number of unique features accumulated during `HashedPercentileDiscretizer` calibration. This is the number of features in the hash map. The `n_bin` is the number of `HashedPercentileDiscretizer` bins used for `HashedPercentileDiscretizer` calibration. The `out_bits` determines the maximum value for output feature IDs. The `bin_values` is a 1D Tensor aligned with `bin_ids`. The `hash_keys` contains the features ID that `HashedPercentileDiscretizer` discretizes and knows about. The `hash_values` translates the feature IDs into hash_feature IDs for `HashedPercentileDiscretizer`. The `bin_ids` is a 1D Tensor of size `n_feature * n_bin + 1` which contains unique IDs to which the `HashedPercentileDiscretizer` features will be translated to. The `feature_offsets` is a 1D Tensor specifying the starting location of bins for a given feature id. The `hash_fn` is a function that takes in `feature_ids`, `bucket_indices`, and `output_size` and hashes the bucketed features into the `output_size` buckets.

The layer has a `call` method that implements `HashedPercentileDiscretizer` inference where inputs are intersected with a hash_map. Part of the inputs are discretized using `twml.discretizer` to produce a `discretizer_output SparseTensor`. This `SparseTensor` is then joined with the original inputs `SparseTensor`, but only for the inputs keys that did not get discretized. The output is a `SparseTensor` of the same type as `inputs`. Its dense_shape is `[shape_input.dense_shape[0], 1 << output_bits]`.

Example usage:
```python
from twitter.deepbird.util.hashing import integer_multiplicative_hashing_uniform, integer_multiplicative_hashing
from libtwml import percentile_discretizer_bin_indices
import numpy as np
import tensorflow.compat.v1 as tf
import twml
from twml.layers.layer import Layer
from twml.layers.partition import Partition
from twml.layers.stitch import Stitch

n_feature = 10
n_bin = 5
out_bits = 10

# Initialize the layer
hashed_percentile_discretizer = HashedPercentileDiscretizer(n_feature=n_feature, n_bin=n_bin, out_bits=out_bits)

# Call the layer
inputs = tf.SparseTensor(indices=[[0, 0], [1, 2]], values=[1.0, 2.0], dense_shape=[3, 4])
output = hashed_percentile_discretizer(inputs)
```
## Questions: 
 1. What is the purpose of the `HashedPercentileDiscretizer` layer and how does it work?
- The `HashedPercentileDiscretizer` layer takes sparse continuous features and converts them to sparse binary features. Each binary output feature is associated with a `HashedPercentileDiscretizer` bin. The layer converts each `HashedPercentileDiscretizer` input feature to `n_bin` bins and tries to find bin delimiters such that the number of feature values per bin is roughly equal.
2. What are the required and optional arguments for initializing a `HashedPercentileDiscretizer` object?
- The required arguments are `n_feature`, `n_bin`, and `out_bits`. The optional arguments are `hash_keys`, `hash_values`, `bin_ids`, `bin_values`, `feature_offsets`, and `hash_fn`.
3. What is the output of the `call` method of the `HashedPercentileDiscretizer` layer?
- The `call` method of the `HashedPercentileDiscretizer` layer returns a `SparseTensor` of the same type as the input `SparseTensor`. Its dense shape is `[shape_input.dense_shape[0], 1 << output_bits]`. The method implements `HashedPercentileDiscretizer` inference where inputs are intersected with a hash map. Part of the inputs are discretized using `twml.discretizer` to produce a discretizer output `SparseTensor`. This `SparseTensor` is then joined with the original inputs `SparseTensor`, but only for the input keys that did not get discretized.