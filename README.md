### I use
```
python version 3.6.X
pip version 18.1
tensorflow version 1.12.0
stable cpu
```

### download catdog dataset https://drive.google.com/file/d/1YfOsfS7kO6HJeA7hzmJ4vHmCV3MavyXh/view

### extract file dataset and move folder trainingCatDog to .../tensorflow_model_for_android_ios/tf_files

## use terminal windows

### changes the current directory to project
```
cd .../tensorflow_model_for_android_ios
```

### set IMAGE_SIZE and ARCHITECTURE
```
SET IMAGE_SIZE=224
SET ARCHITECTURE=”mobilenet_0.50_%IMAGE_SIZE%”
```

### train model
```
python -m scripts.retrain --bottleneck_dir=tf_files/bottlenecks --how_many_training_steps=500 --model_dir=tf_files/models/ --summaries_dir=tf_files/training_summaries/%ARCHITECTURE% --output_graph=tf_files/retrained_graph.pb --output_labels=tf_files/retrained_labels.txt --architecture="%ARCHITECTURE%" --image_dir=tf_files/trainingCatDog
```

### test model
```
python -m scripts.label_image --graph=tf_files/retrained_graph.pb --image=tf_files/trainingCatDog/dogs/dog.19.jpg
```

## use terminal linux

### changes the current directory to project
```
cd .../tensorflow_model_for_android_ios
```

### covert file .pb to .lite
```
IMAGE_SIZE=224
tflite_convert --graph_def_file=tf_files/retrained_graph.pb --output_file=tf_files/optimized_graph.lite --input_format=TENSORFLOW_GRAPHDEF --output_format=TFLITE --input_shape=1,${IMAGE_SIZE},${IMAGE_SIZE},3 --input_array=input --output_array=final_result --inference_type=FLOAT --input_data_type=FLOAT
```

### Reference: https://github.com/googlecodelabs/tensorflow-for-poets-2
