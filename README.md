다음과 같은 코드를 스파이더에서 돌려서
쉬프트, 로테이트를 연산해주어 새로운 사진들을 폴더에 넣으려고 했다
어쩐일인지 압축을 풀어도 100개 그대로 여서 정확도는 똑같이 33프로 정도가 나왔다
하지만, 테스트용 사진을 보니 보 사진을 다른 분이 옆으로 손날같이 한 사진이 많아서 그런 것 같다.....
열심히 노력했으니 잘 봐주셨으면 


import tensorflow as tf
from tensorflow import keras

from keras.preprocessing.image import ImageDataGenerator
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import load_img
import numpy as np
from keras.preprocessing.image import ImageDataGenerator
from keras.preprocessing.image import img_to_array
from keras.preprocessing.image import load_img

image_dir_path = "/Users/parksunghun/Downloads/paper"




tf.keras.preprocessing.image.ImageDataGenerator(
    featurewise_center=False,
    samplewise_center=False,
    featurewise_std_normalization=False,
    samplewise_std_normalization=False,
    zca_whitening=False,
    zca_epsilon=1e-06,
    rotation_range=0,
    width_shift_range=0.0,
    height_shift_range=0.0,
    brightness_range=None,
    shear_range=0.0,
    zoom_range=0.0,
    channel_shift_range=0.0,
    fill_mode="nearest",
    cval=0.0,
    horizontal_flip=False,
    vertical_flip=False,
    rescale=None,
    preprocessing_function=None,
    data_format=None,
    validation_split=0.0,
    dtype=None,
)


IMAGE_PATH = "/Users/parksunghun/Downloads/paper/80.jpg"
OUTPUT_DIRECTORY = image_dir_path


image = load_img(IMAGE_PATH)
image = img_to_array(image)
image = np.expand_dims(image, axis=0) 

datagen = ImageDataGenerator(height_shift_range=0.2, width_shift_range=0.2)
PREFIX = 'Shifted'
imGen = datagen.flow(image, batch_size=1, save_to_dir = OUTPUT_DIRECTORY, 
                    save_prefix=PREFIX, save_format='jpg')
for i in range(6):
    batch = imGen.next()
    
datagen2 = ImageDataGenerator(rotation_range=30)
PREFIX2 = 'Rotated'
imGen2 = datagen2.flow(image, batch_size=1, save_to_dir = OUTPUT_DIRECTORY, 
                    save_prefix=PREFIX2, save_format='jpg')
for i in range(6):
    batch = imGen2.next()
    
    # PaperScissorRock__KERAS
    


