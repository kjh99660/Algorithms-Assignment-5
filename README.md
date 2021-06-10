# Algorithms-Assignment-5
중앙대학교 알고리즘 수업 과제  
* * * 
# First Case
```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers, models
import numpy as np 
import matplotlib.pyplot as plt
```


```python
mnist = keras.datasets.mnist
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
```

    Downloading data from https://storage.googleapis.com/tensorflow/tf-keras-datasets/mnist.npz
    11493376/11490434 [==============================] - 0s 0us/step
    


```python
print('Shape of Train images :',train_images.shape)
print('Shape of Train labels : ', train_labels.shape)
print('\nShape of Test images : ', test_images.shape)
print("Shape of Test labels : ",test_labels.shape)
```

    Shape of Train images : (60000, 28, 28)
    Shape of Train labels :  (60000,)
    
    Shape of Test images :  (10000, 28, 28)
    Shape of Test labels :  (10000,)
    


```python
print('Train labels : ',train_labels)
```

    Train labels :  [5 0 4 ... 5 6 8]
    


```python
print(train_images[1])
```

    [[  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0  51 159 253
      159  50   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0  48 238 252 252
      252 237   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0  54 227 253 252 239
      233 252  57   6   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0  10  60 224 252 253 252 202
       84 252 253 122   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0 163 252 252 252 253 252 252
       96 189 253 167   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0  51 238 253 253 190 114 253 228
       47  79 255 168   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0  48 238 252 252 179  12  75 121  21
        0   0 253 243  50   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0  38 165 253 233 208  84   0   0   0   0
        0   0 253 252 165   0   0   0   0   0]
     [  0   0   0   0   0   0   0   7 178 252 240  71  19  28   0   0   0   0
        0   0 253 252 195   0   0   0   0   0]
     [  0   0   0   0   0   0   0  57 252 252  63   0   0   0   0   0   0   0
        0   0 253 252 195   0   0   0   0   0]
     [  0   0   0   0   0   0   0 198 253 190   0   0   0   0   0   0   0   0
        0   0 255 253 196   0   0   0   0   0]
     [  0   0   0   0   0   0  76 246 252 112   0   0   0   0   0   0   0   0
        0   0 253 252 148   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 230  25   0   0   0   0   0   0   0   0
        7 135 253 186  12   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 223   0   0   0   0   0   0   0   0   7
      131 252 225  71   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 145   0   0   0   0   0   0   0  48 165
      252 173   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  86 253 225   0   0   0   0   0   0 114 238 253
      162   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 249 146  48  29  85 178 225 253 223 167
       56   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 252 252 229 215 252 252 252 196 130   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  28 199 252 252 253 252 252 233 145   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0  25 128 252 253 252 141  37   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]]
    


```python
print('First 10 Train images in MNIST dataset\n')
for i in range(10):
    plt.subplot(1, 10, i+1)
    plt.xticks([])
    plt.yticks([])
    plt.imshow(train_images[i])
plt.show()
print('\nTrain labels match with Train label sequentialy\n',train_labels[:10])
```

    First 10 Train images in MNIST dataset
    
    


    
![png](README_IMAGE/output_5_1.png)
    


    
    Train labels match with Train label sequentialy
     [5 0 4 1 9 2 1 3 1 4]
    


```python
train_images = tf.reshape(train_images, [-1, 28, 28, 1])
test_images = tf.reshape(test_images, [-1, 28, 28, 1])
```


```python
def select_model(model_number):
    if model_number == 1:
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape = (28, 28,1)),  # layer 1 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2 
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 3

    if model_number == 2:
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape=(28,28,1)),     # layer 1 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 3 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 4
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 5
                    
    if model_number == 3: 
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape = (28, 28,1)),  # layer 1
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 3
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 4
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 5
                    keras.layers.Conv2D(128, (3,3), activation = 'relu'),                           # layer 6
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 7
    
    return model
```


```python
model = select_model(1)
```


```python
model.summary()
```

    Model: "sequential"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    conv2d (Conv2D)              (None, 26, 26, 32)        320       
    _________________________________________________________________
    max_pooling2d (MaxPooling2D) (None, 13, 13, 32)        0         
    _________________________________________________________________
    flatten (Flatten)            (None, 5408)              0         
    _________________________________________________________________
    dense (Dense)                (None, 10)                54090     
    =================================================================
    Total params: 54,410
    Trainable params: 54,410
    Non-trainable params: 0
    _________________________________________________________________
    


```python
model.compile(
    optimizer = 'adam',
    loss = 'sparse_categorical_crossentropy',
    metrics = ['accuracy']
)
```


```python
model.fit(train_images, train_labels,  epochs = 5)
```

    Epoch 1/5
    1875/1875 [==============================] - 11s 5ms/step - loss: 0.6492 - accuracy: 0.9379
    Epoch 2/5
    1875/1875 [==============================] - 10s 6ms/step - loss: 0.0917 - accuracy: 0.9726
    Epoch 3/5
    1875/1875 [==============================] - 11s 6ms/step - loss: 0.0746 - accuracy: 0.9775
    Epoch 4/5
    1875/1875 [==============================] - 11s 6ms/step - loss: 0.0651 - accuracy: 0.9810
    Epoch 5/5
    1875/1875 [==============================] - 11s 6ms/step - loss: 0.0567 - accuracy: 0.9833
    




    <tensorflow.python.keras.callbacks.History at 0x1c8cdac1550>




```python
test_loss, accuracy = model.evaluate(test_images, test_labels, verbose = 2)
print('\nTest loss : ', test_loss)
print('Test accuracy :', accuracy)
```

    313/313 - 1s - loss: 0.1308 - accuracy: 0.9727
    
    Test loss :  0.13078248500823975
    Test accuracy : 0.9726999998092651
    


```python
test_images = tf.cast(test_images, tf.float32)
pred = model.predict(test_images)
Number = [0,1,2,3,4,5,6,7,8,9]
```


```python
print('Prediction : ', pred.shape)
print('Test labels : ', test_labels.shape)
```

    Prediction :  (10000, 10)
    Test labels :  (10000,)
    


```python
def plot_image(i, predictions_array, true_label, img):
  predictions_array, true_label, img = predictions_array[i], true_label[i], img[i]
  plt.grid(False)
  plt.xticks([])
  plt.yticks([])

  plt.imshow(img, cmap=plt.cm.binary)

  predicted_label = np.argmax(predictions_array)
  if predicted_label == true_label:
    color = 'blue'
  else:
    color = 'red'

  plt.xlabel("{} {:2.0f}% ({})".format(Number[predicted_label],
                                100*np.max(predictions_array),
                                Number[true_label]),
                                color=color)

def plot_value_array(i, predictions_array, true_label):
  predictions_array, true_label = predictions_array[i], true_label[i]
  plt.grid(False)
  plt.xticks([])
  plt.yticks([])
  thisplot = plt.bar(range(10), predictions_array, color="#777777")
  plt.ylim([0, 1])
  predicted_label = np.argmax(predictions_array)
  plt.xticks(Number)

  thisplot[predicted_label].set_color('red')
  thisplot[true_label].set_color('blue')
```


```python
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
```


```python
i = 1
plt.figure(figsize=(6,3))
plt.subplot(1,2,1)
plot_image(i, pred, test_labels, test_images)
plt.subplot(1,2,2)
plot_value_array(i, pred,  test_labels)
plt.show()
```


    
![png](README_IMAGE/output_17_0.png)
    



```python
num_rows = 5
num_cols = 3
num_images = num_rows*num_cols
plt.figure(figsize=(2*2*num_cols, 2*num_rows))
for i in range(num_images):
  plt.subplot(num_rows, 2*num_cols, 2*i+1)
  plot_image(i, pred, test_labels, test_images)
  plt.subplot(num_rows, 2*num_cols, 2*i+2)
  plot_value_array(i, pred, test_labels)
plt.show()
```


    
![png](README_IMAGE/output_18_0.png)
    



```python
def error_mnist(prediction_array, true_label):
    error_index = []
    
    for i in range(true_label.shape[0]):
        if np.argmax(prediction_array[i]) != true_label[i]:
            error_index.append(i)
    return error_index

# change num_cols, num_rows if you want to see more result.  
def plot_error(index, prediction_array, true_label):
    num_cols = 5
    num_rows = 5
    plt.figure(figsize=(2*2*num_cols, 2*num_rows))

    assert len(index) < num_cols * num_rows
    for i in range(len(index)):
        plt.subplot(num_rows, 2*num_cols, 2*i+1)
        idx = index[i]
        plt.imshow(test_images[idx])
        plt.subplot(num_rows, 2*num_cols, 2*i+2)
        plt.bar(range(10), prediction_array[idx])
        plt.xticks(Number)
```


```python
index = error_mnist(pred, test_labels)
index_slice = index[:10]
print(index[:10])
```

    [96, 211, 257, 259, 320, 321, 340, 394, 445, 490]
    


```python
plot_error(index_slice, pred, test_labels)
```


    
![png](README_IMAGE/output_21_0.png)
    


# Second Case
* * * 
```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers, models
import numpy as np 
import matplotlib.pyplot as plt
```


```python
mnist = keras.datasets.mnist
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
```


```python
print('Shape of Train images :',train_images.shape)
print('Shape of Train labels : ', train_labels.shape)
print('\nShape of Test images : ', test_images.shape)
print("Shape of Test labels : ",test_labels.shape)
```

    Shape of Train images : (60000, 28, 28)
    Shape of Train labels :  (60000,)
    
    Shape of Test images :  (10000, 28, 28)
    Shape of Test labels :  (10000,)
    


```python
print('Train labels : ',train_labels)
```

    Train labels :  [5 0 4 ... 5 6 8]
    


```python
print(train_images[1])
```

    [[  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0  51 159 253
      159  50   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0  48 238 252 252
      252 237   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0  54 227 253 252 239
      233 252  57   6   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0  10  60 224 252 253 252 202
       84 252 253 122   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0 163 252 252 252 253 252 252
       96 189 253 167   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0  51 238 253 253 190 114 253 228
       47  79 255 168   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0  48 238 252 252 179  12  75 121  21
        0   0 253 243  50   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0  38 165 253 233 208  84   0   0   0   0
        0   0 253 252 165   0   0   0   0   0]
     [  0   0   0   0   0   0   0   7 178 252 240  71  19  28   0   0   0   0
        0   0 253 252 195   0   0   0   0   0]
     [  0   0   0   0   0   0   0  57 252 252  63   0   0   0   0   0   0   0
        0   0 253 252 195   0   0   0   0   0]
     [  0   0   0   0   0   0   0 198 253 190   0   0   0   0   0   0   0   0
        0   0 255 253 196   0   0   0   0   0]
     [  0   0   0   0   0   0  76 246 252 112   0   0   0   0   0   0   0   0
        0   0 253 252 148   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 230  25   0   0   0   0   0   0   0   0
        7 135 253 186  12   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 223   0   0   0   0   0   0   0   0   7
      131 252 225  71   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 145   0   0   0   0   0   0   0  48 165
      252 173   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  86 253 225   0   0   0   0   0   0 114 238 253
      162   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 249 146  48  29  85 178 225 253 223 167
       56   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 252 252 229 215 252 252 252 196 130   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  28 199 252 252 253 252 252 233 145   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0  25 128 252 253 252 141  37   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]]
    


```python
print('First 10 Train images in MNIST dataset\n')
for i in range(10):
    plt.subplot(1, 10, i+1)
    plt.xticks([])
    plt.yticks([])
    plt.imshow(train_images[i])
plt.show()
print('\nTrain labels match with Train label sequentialy\n',train_labels[:10])
```

    First 10 Train images in MNIST dataset
    
    


    
![png](README_IMAGE/output_5_1_2.png)
    


    
    Train labels match with Train label sequentialy
     [5 0 4 1 9 2 1 3 1 4]
    


```python
train_images = tf.reshape(train_images, [-1, 28, 28, 1])
test_images = tf.reshape(test_images, [-1, 28, 28, 1])
```


```python
def select_model(model_number):
    if model_number == 1:
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape = (28, 28,1)),  # layer 1 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2 
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 3

    if model_number == 2:
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape=(28,28,1)),     # layer 1 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 3 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 4
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 5
                    
    if model_number == 3: 
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape = (28, 28,1)),  # layer 1
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 3
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 4
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 5
                    keras.layers.Conv2D(128, (3,3), activation = 'relu'),                           # layer 6
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 7
    
    return model
```


```python
model = select_model(2)
```


```python
model.summary()
```

    Model: "sequential"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    conv2d (Conv2D)              (None, 26, 26, 32)        320       
    _________________________________________________________________
    max_pooling2d (MaxPooling2D) (None, 13, 13, 32)        0         
    _________________________________________________________________
    conv2d_1 (Conv2D)            (None, 11, 11, 64)        18496     
    _________________________________________________________________
    max_pooling2d_1 (MaxPooling2 (None, 5, 5, 64)          0         
    _________________________________________________________________
    flatten (Flatten)            (None, 1600)              0         
    _________________________________________________________________
    dense (Dense)                (None, 10)                16010     
    =================================================================
    Total params: 34,826
    Trainable params: 34,826
    Non-trainable params: 0
    _________________________________________________________________
    


```python
model.compile(
    optimizer = 'adam',
    loss = 'sparse_categorical_crossentropy',
    metrics = ['accuracy']
)
```


```python
model.fit(train_images, train_labels,  epochs = 5)
```

    Epoch 1/5
    1875/1875 [==============================] - 18s 9ms/step - loss: 0.4104 - accuracy: 0.9414
    Epoch 2/5
    1875/1875 [==============================] - 17s 9ms/step - loss: 0.0731 - accuracy: 0.9784
    Epoch 3/5
    1875/1875 [==============================] - 17s 9ms/step - loss: 0.0566 - accuracy: 0.9828
    Epoch 4/5
    1875/1875 [==============================] - 17s 9ms/step - loss: 0.0493 - accuracy: 0.9854
    Epoch 5/5
    1875/1875 [==============================] - 17s 9ms/step - loss: 0.0434 - accuracy: 0.9869
    




    <tensorflow.python.keras.callbacks.History at 0x241e3be6eb0>




```python
test_loss, accuracy = model.evaluate(test_images, test_labels, verbose = 2)
print('\nTest loss : ', test_loss)
print('Test accuracy :', accuracy)
```

    313/313 - 1s - loss: 0.0550 - accuracy: 0.9839
    
    Test loss :  0.05496939644217491
    Test accuracy : 0.9839000105857849
    


```python
test_images = tf.cast(test_images, tf.float32)
pred = model.predict(test_images)
Number = [0,1,2,3,4,5,6,7,8,9]
```


```python
print('Prediction : ', pred.shape)
print('Test labels : ', test_labels.shape)
```

    Prediction :  (10000, 10)
    Test labels :  (10000,)
    


```python
def plot_image(i, predictions_array, true_label, img):
  predictions_array, true_label, img = predictions_array[i], true_label[i], img[i]
  plt.grid(False)
  plt.xticks([])
  plt.yticks([])

  plt.imshow(img, cmap=plt.cm.binary)

  predicted_label = np.argmax(predictions_array)
  if predicted_label == true_label:
    color = 'blue'
  else:
    color = 'red'

  plt.xlabel("{} {:2.0f}% ({})".format(Number[predicted_label],
                                100*np.max(predictions_array),
                                Number[true_label]),
                                color=color)

def plot_value_array(i, predictions_array, true_label):
  predictions_array, true_label = predictions_array[i], true_label[i]
  plt.grid(False)
  plt.xticks([])
  plt.yticks([])
  thisplot = plt.bar(range(10), predictions_array, color="#777777")
  plt.ylim([0, 1])
  predicted_label = np.argmax(predictions_array)
  plt.xticks(Number)

  thisplot[predicted_label].set_color('red')
  thisplot[true_label].set_color('blue')
```


```python
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
```


```python
i = 1
plt.figure(figsize=(6,3))
plt.subplot(1,2,1)
plot_image(i, pred, test_labels, test_images)
plt.subplot(1,2,2)
plot_value_array(i, pred,  test_labels)
plt.show()
```


    
![png](README_IMAGE/output_17_0_2.png)
    



```python
num_rows = 5
num_cols = 3
num_images = num_rows*num_cols
plt.figure(figsize=(2*2*num_cols, 2*num_rows))
for i in range(num_images):
  plt.subplot(num_rows, 2*num_cols, 2*i+1)
  plot_image(i, pred, test_labels, test_images)
  plt.subplot(num_rows, 2*num_cols, 2*i+2)
  plot_value_array(i, pred, test_labels)
plt.show()
```


    
![png](README_IMAGE/output_18_0_2.png)
    



```python
def error_mnist(prediction_array, true_label):
    error_index = []
    
    for i in range(true_label.shape[0]):
        if np.argmax(prediction_array[i]) != true_label[i]:
            error_index.append(i)
    return error_index

# change num_cols, num_rows if you want to see more result.  
def plot_error(index, prediction_array, true_label):
    num_cols = 5
    num_rows = 5
    plt.figure(figsize=(2*2*num_cols, 2*num_rows))

    assert len(index) < num_cols * num_rows
    for i in range(len(index)):
        plt.subplot(num_rows, 2*num_cols, 2*i+1)
        idx = index[i]
        plt.imshow(test_images[idx])
        plt.subplot(num_rows, 2*num_cols, 2*i+2)
        plt.bar(range(10), prediction_array[idx])
        plt.xticks(Number)
```


```python
index = error_mnist(pred, test_labels)
index_slice = index[:10]
print(index[:10])
```

    [95, 115, 247, 259, 321, 326, 435, 583, 591, 610]
    


```python
plot_error(index_slice, pred, test_labels)
```


    
![png](README_IMAGE/output_21_0_2.png)
    


# Third Case 
* * * 
```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers, models
import numpy as np 
import matplotlib.pyplot as plt
```


```python
mnist = keras.datasets.mnist
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
```


```python
print('Shape of Train images :',train_images.shape)
print('Shape of Train labels : ', train_labels.shape)
print('\nShape of Test images : ', test_images.shape)
print("Shape of Test labels : ",test_labels.shape)
```

    Shape of Train images : (60000, 28, 28)
    Shape of Train labels :  (60000,)
    
    Shape of Test images :  (10000, 28, 28)
    Shape of Test labels :  (10000,)
    


```python
print('Train labels : ',train_labels)
```

    Train labels :  [5 0 4 ... 5 6 8]
    


```python
print(train_images[1])
```

    [[  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0  51 159 253
      159  50   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0  48 238 252 252
      252 237   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0  54 227 253 252 239
      233 252  57   6   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0  10  60 224 252 253 252 202
       84 252 253 122   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0 163 252 252 252 253 252 252
       96 189 253 167   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0  51 238 253 253 190 114 253 228
       47  79 255 168   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0  48 238 252 252 179  12  75 121  21
        0   0 253 243  50   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0  38 165 253 233 208  84   0   0   0   0
        0   0 253 252 165   0   0   0   0   0]
     [  0   0   0   0   0   0   0   7 178 252 240  71  19  28   0   0   0   0
        0   0 253 252 195   0   0   0   0   0]
     [  0   0   0   0   0   0   0  57 252 252  63   0   0   0   0   0   0   0
        0   0 253 252 195   0   0   0   0   0]
     [  0   0   0   0   0   0   0 198 253 190   0   0   0   0   0   0   0   0
        0   0 255 253 196   0   0   0   0   0]
     [  0   0   0   0   0   0  76 246 252 112   0   0   0   0   0   0   0   0
        0   0 253 252 148   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 230  25   0   0   0   0   0   0   0   0
        7 135 253 186  12   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 223   0   0   0   0   0   0   0   0   7
      131 252 225  71   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 145   0   0   0   0   0   0   0  48 165
      252 173   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  86 253 225   0   0   0   0   0   0 114 238 253
      162   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 249 146  48  29  85 178 225 253 223 167
       56   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  85 252 252 252 229 215 252 252 252 196 130   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0  28 199 252 252 253 252 252 233 145   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0  25 128 252 253 252 141  37   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]
     [  0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
        0   0   0   0   0   0   0   0   0   0]]
    


```python
print('First 10 Train images in MNIST dataset\n')
for i in range(10):
    plt.subplot(1, 10, i+1)
    plt.xticks([])
    plt.yticks([])
    plt.imshow(train_images[i])
plt.show()
print('\nTrain labels match with Train label sequentialy\n',train_labels[:10])
```

    First 10 Train images in MNIST dataset
    
    


    
![png](README_IMAGE/output_5_1_3.png)
    


    
    Train labels match with Train label sequentialy
     [5 0 4 1 9 2 1 3 1 4]
    


```python
train_images = tf.reshape(train_images, [-1, 28, 28, 1])
test_images = tf.reshape(test_images, [-1, 28, 28, 1])
```


```python
def select_model(model_number):
    if model_number == 1:
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape = (28, 28,1)),  # layer 1 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2 
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 3

    if model_number == 2:
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape=(28,28,1)),     # layer 1 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 3 
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 4
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 5
                    
    if model_number == 3: 
        model = keras.models.Sequential([
                    keras.layers.Conv2D(32, (3,3), activation = 'relu', input_shape = (28, 28,1)),  # layer 1
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 2
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 3
                    keras.layers.Conv2D(64, (3,3), activation = 'relu'),                            # layer 4
                    keras.layers.MaxPool2D((2,2)),                                                  # layer 5
                    keras.layers.Conv2D(128, (3,3), activation = 'relu'),                           # layer 6
                    keras.layers.Flatten(),
                    keras.layers.Dense(10, activation = 'softmax')])                                # layer 7
    
    return model
```


```python
model = select_model(3)
```


```python
model.summary()
```

    Model: "sequential_1"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    conv2d_2 (Conv2D)            (None, 26, 26, 32)        320       
    _________________________________________________________________
    max_pooling2d_2 (MaxPooling2 (None, 13, 13, 32)        0         
    _________________________________________________________________
    conv2d_3 (Conv2D)            (None, 11, 11, 64)        18496     
    _________________________________________________________________
    conv2d_4 (Conv2D)            (None, 9, 9, 64)          36928     
    _________________________________________________________________
    max_pooling2d_3 (MaxPooling2 (None, 4, 4, 64)          0         
    _________________________________________________________________
    conv2d_5 (Conv2D)            (None, 2, 2, 128)         73856     
    _________________________________________________________________
    flatten_1 (Flatten)          (None, 512)               0         
    _________________________________________________________________
    dense_1 (Dense)              (None, 10)                5130      
    =================================================================
    Total params: 134,730
    Trainable params: 134,730
    Non-trainable params: 0
    _________________________________________________________________
    


```python
model.compile(
    optimizer = 'adam',
    loss = 'sparse_categorical_crossentropy',
    metrics = ['accuracy']
)
```


```python
model.fit(train_images, train_labels,  epochs = 5)
```

    Epoch 1/5
    1875/1875 [==============================] - 30s 16ms/step - loss: 0.1749 - accuracy: 0.9566
    Epoch 2/5
    1875/1875 [==============================] - 30s 16ms/step - loss: 0.0559 - accuracy: 0.9830
    Epoch 3/5
    1875/1875 [==============================] - 29s 15ms/step - loss: 0.0430 - accuracy: 0.9867
    Epoch 4/5
    1875/1875 [==============================] - 29s 15ms/step - loss: 0.0360 - accuracy: 0.9889
    Epoch 5/5
    1875/1875 [==============================] - 31s 17ms/step - loss: 0.0321 - accuracy: 0.9908
    




    <tensorflow.python.keras.callbacks.History at 0x241e0d95190>




```python
test_loss, accuracy = model.evaluate(test_images, test_labels, verbose = 2)
print('\nTest loss : ', test_loss)
print('Test accuracy :', accuracy)
```

    313/313 - 1s - loss: 0.0377 - accuracy: 0.9887
    
    Test loss :  0.03774923458695412
    Test accuracy : 0.9886999726295471
    


```python
test_images = tf.cast(test_images, tf.float32)
pred = model.predict(test_images)
Number = [0,1,2,3,4,5,6,7,8,9]
```


```python
print('Prediction : ', pred.shape)
print('Test labels : ', test_labels.shape)
```

    Prediction :  (10000, 10)
    Test labels :  (10000,)
    


```python
def plot_image(i, predictions_array, true_label, img):
  predictions_array, true_label, img = predictions_array[i], true_label[i], img[i]
  plt.grid(False)
  plt.xticks([])
  plt.yticks([])

  plt.imshow(img, cmap=plt.cm.binary)

  predicted_label = np.argmax(predictions_array)
  if predicted_label == true_label:
    color = 'blue'
  else:
    color = 'red'

  plt.xlabel("{} {:2.0f}% ({})".format(Number[predicted_label],
                                100*np.max(predictions_array),
                                Number[true_label]),
                                color=color)

def plot_value_array(i, predictions_array, true_label):
  predictions_array, true_label = predictions_array[i], true_label[i]
  plt.grid(False)
  plt.xticks([])
  plt.yticks([])
  thisplot = plt.bar(range(10), predictions_array, color="#777777")
  plt.ylim([0, 1])
  predicted_label = np.argmax(predictions_array)
  plt.xticks(Number)

  thisplot[predicted_label].set_color('red')
  thisplot[true_label].set_color('blue')
```


```python
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
```


```python
i = 1
plt.figure(figsize=(6,3))
plt.subplot(1,2,1)
plot_image(i, pred, test_labels, test_images)
plt.subplot(1,2,2)
plot_value_array(i, pred,  test_labels)
plt.show()
```


    
![png](README_IMAGE/output_17_0_3.png)
    



```python
num_rows = 5
num_cols = 3
num_images = num_rows*num_cols
plt.figure(figsize=(2*2*num_cols, 2*num_rows))
for i in range(num_images):
  plt.subplot(num_rows, 2*num_cols, 2*i+1)
  plot_image(i, pred, test_labels, test_images)
  plt.subplot(num_rows, 2*num_cols, 2*i+2)
  plot_value_array(i, pred, test_labels)
plt.show()
```


    
![png](README_IMAGE/output_18_0_3.png)
    



```python
def error_mnist(prediction_array, true_label):
    error_index = []
    
    for i in range(true_label.shape[0]):
        if np.argmax(prediction_array[i]) != true_label[i]:
            error_index.append(i)
    return error_index

# change num_cols, num_rows if you want to see more result.  
def plot_error(index, prediction_array, true_label):
    num_cols = 5
    num_rows = 5
    plt.figure(figsize=(2*2*num_cols, 2*num_rows))

    assert len(index) < num_cols * num_rows
    for i in range(len(index)):
        plt.subplot(num_rows, 2*num_cols, 2*i+1)
        idx = index[i]
        plt.imshow(test_images[idx])
        plt.subplot(num_rows, 2*num_cols, 2*i+2)
        plt.bar(range(10), prediction_array[idx])
        plt.xticks(Number)
```


```python
index = error_mnist(pred, test_labels)
index_slice = index[:10]
print(index[:10])
```

    [43, 62, 259, 381, 415, 449, 450, 582, 625, 646]
    


```python
plot_error(index_slice, pred, test_labels)
```


    
![png](README_IMAGE/output_21_0_3.png)
    

