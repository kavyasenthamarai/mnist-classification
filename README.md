# Convolutional Deep Neural Network for Digit Classification

## AIM

To Develop a convolutional deep neural network for digit classification and to verify the response for scanned handwritten images.

## Problem Statement and Dataset

## Neural Network Model

![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/709d6fe6-346c-4dc9-b778-ec66f003e5e9)


## DESIGN STEPS

### STEP 1:
Preprocess the MNIST dataset by scaling the pixel values to the range [0, 1] and converting labels to one-hot encoded format.

### STEP 2:
Build a convolutional neural network (CNN) model with specified architecture using TensorFlow Keras.

### STEP 3:
Compile the model with categorical cross-entropy loss function and the Adam optimizer.

### STEP 4:
Train the compiled model on the preprocessed training data for 5 epochs with a batch size of 64.

### STEP 5:
Evaluate the trained model's performance on the test set by plotting training/validation metrics and generating a confusion matrix and classification report. Additionally, make predictions on sample images to demonstrate model inference.


## PROGRAM

### Name:KAVYA K
### Register Number:212222230065

```
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers
from tensorflow.keras.datasets import mnist
import tensorflow as tf
import matplotlib.pyplot as plt
from tensorflow.keras import utils
import pandas as pd
from sklearn.metrics import classification_report, confusion_matrix
from tensorflow.keras.preprocessing import image

(X_train, y_train), (X_test, y_test) = mnist.load_data()
X_train.shape
X_test.shape
single_image = X_train[0]
single_image.shape
plt.imshow(single_image, cmap='gray')
y_train.shape
X_train.min()
X_train.max()
X_train_scaled = X_train / 255.0
X_test_scaled = X_test / 255.0
X_train_scaled.min()
X_train_scaled.max()
y_train[0]
y_train_onehot = utils.to_categorical(y_train, 10)
y_test_onehot = utils.to_categorical(y_test, 10)
type(y_train_onehot)
y_train_onehot.shape
single_image = X_train[500]
plt.imshow(single_image, cmap='gray')
y_train_onehot[500]
X_train_scaled = X_train_scaled.reshape(-1, 28, 28, 1)
X_test_scaled = X_test_scaled.reshape(-1, 28, 28, 1)

model = keras.Sequential()
model.add(layers.Input(shape=(28, 28, 1)))
model.add(layers.Conv2D(filters=32, kernel_size=(3, 3), activation='relu'))
model.add(layers.MaxPool2D(pool_size=(2, 2)))
model.add(layers.Flatten())
model.add(layers.Dense(16, activation='relu'))
model.add(layers.Dense(12, activation='relu'))
model.add(layers.Dense(10, activation='softmax'))  # Adjusted output layer

model.summary()

model.compile(loss='categorical_crossentropy',
              optimizer='adam',
              metrics='accuracy')

model.fit(X_train_scaled, y_train_onehot, epochs=5,
          batch_size=64,
          validation_data=(X_test_scaled, y_test_onehot))

metrics = pd.DataFrame(model.history.history)
metrics.head()

metrics[['accuracy', 'val_accuracy']].plot()

metrics[['loss', 'val_loss']].plot()

x_test_predictions = np.argmax(model.predict(X_test_scaled), axis=1)

print("Kavya K 212222230065")
print(confusion_matrix(y_test, x_test_predictions))

print("Kavya K 212222230065")
print(classification_report(y_test, x_test_predictions))

img = image.load_img('/content/img.jpeg')
type(img)

img = image.load_img('/content/six.png')
plt.imshow(img)
img_tensor = tf.convert_to_tensor(np.asarray(img))
img_28 = tf.image.resize(img_tensor, (28, 28))
img_28_gray = tf.image.rgb_to_grayscale(img_28)
img_28_gray_scaled = img_28_gray.numpy() / 255.0
x_single_prediction = np.argmax(model.predict(img_28_gray_scaled.reshape(1, 28, 28, 1)), axis=1)

print("Kavya K 212222230065")
print(x_single_prediction)
plt.imshow(img_28_gray_scaled.reshape(28, 28), cmap='gray')

img1 = image.load_img('/content/zero.jfif')
plt.imshow(img1)
img_tensor1 = tf.convert_to_tensor(np.asarray(img1))
img_28_gray1 = tf.image.resize(img_tensor1, (28, 28))
img_28_gray1 = tf.image.rgb_to_grayscale(img_28_gray1)
img_28_gray_inverted1 = 255.0 - img_28_gray1
img_28_gray_inverted_scaled1 = img_28_gray_inverted1.numpy() / 255.0

x_single_prediction1 = np.argmax(model.predict(img_28_gray_inverted_scaled1.reshape(1, 28, 28, 1)), axis=1)
print("Kavya K 212222230065")
print(x_single_prediction1)
plt.imshow(img_28_gray_inverted_scaled1.reshape(28, 28), cmap='gray')


```
## OUTPUT

### Training Loss, Validation Loss Vs Iteration Plot

![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/9eb7625e-8e7e-46a8-be8c-56c7bb789b0d)
![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/b6255e59-4730-4963-bcda-995825cb442a)



### Classification Report

![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/dc964abf-bf72-4dab-b35d-bfa638b2899f)


### Confusion Matrix

![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/7de2c8fa-51f3-4e9a-9bb3-9ceef50d5f34)

### New Sample Data Prediction
![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/13d4c3a8-5c5e-4a13-936a-ccc6dbbb2319)
![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/5fa3a405-eaea-403f-a1b3-b5ab26e05c08)
![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/a1643b6f-26fd-4c49-8f8f-18264b6a112c)

![image](https://github.com/kavyasenthamarai/mnist-classification/assets/118668727/e3805a2e-2b12-4a0b-8078-a34e3084c101)



## RESULT
Thus, a convolutional deep neural network for digit classification and to verify the response for scanned handwritten images is developed successfully.
