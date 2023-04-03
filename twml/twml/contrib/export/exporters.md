[View code on GitHub](https://github.com/misbahsy/the-algorithm/twml/twml/contrib/export/exporters.py)

This file contains three classes that are wrappers around `tf.estimator.Exporters` to export models and save checkpoints. The purpose of these classes is to provide additional functionality to the existing `BestExporter` and `LatestExporter` classes. 

The `_AllSavedModelsExporter` class is an internal exporter class that is used for exporting models for different modes. It takes in a unique name, a map of `tf.estimator.ModeKeys` to `input_receiver_fns`, a flag to specify if backups of checkpoints need to be made, additional assets to be included in the exported model, and a flag to specify if the exported model should be in a human-readable text format. It exports all saved models to the specified export path and returns the export result.

The `BestExporter` and `LatestExporter` classes inherit from `tf.estimator.BestExporter` and `tf.estimator.LatestExporter`, respectively. They both create a backup of the best/latest checkpoint and can export the model for multiple modes. A backup/export is performed every time the evaluated metric is better than previous models. The `BestExporter` class takes in the same arguments as `tf.estimator.BestExporter`, with an additional flag to specify if backups of checkpoints need to be made. The `LatestExporter` class takes in the same arguments as `tf.estimator.LatestExporter`, with an additional flag to specify if backups of checkpoints need to be made.

Overall, these classes provide additional functionality to the existing `BestExporter` and `LatestExporter` classes by creating backups of checkpoints and exporting models for multiple modes. They can be used in the larger project to provide more robust model exporting and checkpoint saving capabilities. 

Example usage:
```
best_exporter = BestExporter(name='best_exporter', input_receiver_fn_map=input_receiver_fn_map, backup_checkpoints=True)
latest_exporter = LatestExporter(name='latest_exporter', input_receiver_fn_map=input_receiver_fn_map, backup_checkpoints=True)
```
## Questions: 
 1. What is the purpose of this code?
- This code provides wrappers around `tf.estimator.Exporters` to export models and save checkpoints.

2. What are the differences between `BestExporter` and `LatestExporter`?
- `BestExporter` and `LatestExporter` both create a backup of the best/latest checkpoint and can export the model for multiple modes. The main difference is that `BestExporter` exports the model every time the evaluated metric is better than previous models, while `LatestExporter` exports the latest model every time a new checkpoint is saved.

3. What is the purpose of the `_AllSavedModelsExporter` class?
- The `_AllSavedModelsExporter` class is an internal exporter class used for exporting models for different modes. It takes in a map of `tf.estimator.ModeKeys` to `input_receiver_fns` and can export all saved models to a specified export path. It also has an option to create backups of checkpoints.