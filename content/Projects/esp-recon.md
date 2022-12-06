# Handwritten Digit Recognition
The goal of the project is to implement CNN based digit-recognition system in a edge and resource constrained device. More specifically, I used a esp32-cam module, which have 2mp camera, 512kb RAM and 4Mb flash memory. My object is to capture image in a loop, crop that image, send to the cnn model’s input tensor, run the model ( invoke ) and output the result based on maximum probability returned


### Install the ESP IDF
- Guide : https://rupakbiswas-2304.github.io/esp32/installation/

### File Structure:
- main.cc : main file that runs
- model_data.h : contains the model’s input and output tensor
- model_data_archive.h : contains the old model’s weights and bias ( not used )
- CMakeLists.txt : cmake file to build the project
- Makefile : make file to build the project
- README.md : this file
- image_provider.h : contains the image provider function definition
- image_provider.cc : contains the image provider function implementation

### Dependencies
- IDF 
- ESP32-CAM
- ESP32-CAM Arduino Library
- Tensorflow Lite for Microcontrollers
- Tensorflow
- Matplotlib
### Building the Model
- Goto the python folder
- run the main.py file 
- It will download the mnist dataset and train the model
- It will save the model in the models folder
- Next for converting the model, run the convert_lite.py file
- It will convert the model to tflite format
- For testing the file, run `python test.py`
### Load and run the example

To flash (replace `/dev/ttyUSB0` with the device serial port):
```
idf.py --port /dev/ttyUSB0 flash
```

Monitor the serial output:
```
idf.py --port /dev/ttyUSB0 monitor
```

Use `Ctrl+]` to exit.

The previous two commands can be combined:
```
idf.py --port /dev/ttyUSB0 flash monitor
```

### Some Output Dump 
    Getting image...
    Image Captured ... Image Size: 320 x 240
    Printing Image 
    -89 -88 -90 -88 -90 -85 -83 -90 -88 -86 -84 -85 -88 -85 -87 -84 -84 -86 -88 -85 -83 -86 -86 -85 -83 -85 -84 -89 
    -92 -92 -90 -92 -93 -91 -88 -87 -99 -92 -93 -93 -93 -93 -95 -93 -91 -91 -90 -94 -90 -89 -94 -95 -93 -94 -95 -96 
    -88 -89 -87 -93 -91 -91 -98 -91 -92 -91 -92 -94 -93 -93 -91 -91 -92 -92 -93 -96 -92 -93 -94 -85 -89 -92 -93 -92 
    -91 -89 -89 -96 -92 -89 -96 -82 -90 -91 -94 -92 -92 -93 -90 -89 -93 -87 -93 -92 -87 -96 -94 -90 -93 -94 -92 -91 
    -93 -85 -79 -94 -93 -94 -92 -86 -85 -92 -92 -90 -90 -94 -92 -90 -92 -95 -94 -92 -96 -85 -91 -94 -94 -92 -94 -89 
    -94 -90 -86 -91 -93 -92 -93 -93 -83 -90 -89 -91 -93 -93 -92 -90 -91 -95 -94 -95 -96 -83 -92 -91 -93 -92 -93 -91 
    -94 -91 -89 -90 -93 -89 -92 -93 -89 -94 -92 -89 -92 -91 -91 -89 -87 -95 -93 -92 -95 -93 -94 -92 -91 -95 -95 -93 
    -92 -93 -92 -92 -91 -90 -90 -92 -92 -94 -92 -87 -91 -91 -89 -94 -95 -93 -93 -92 -95 -92 -92 -90 -91 -94 -96 -91 
    -91 -88 -90 -91 -92 -91 -94 -94 -94 -95 -89 -84 -91 -94 -97 -94 -95 -82 -89 -93 -92 -93 -94 -92 -95 -95 -94 -90 
    -96 -88 -88 -90 -91 -92 -91 -91 -92 -93 -88 -90 -89 -93 -82 -82 -89 -88 -88 -92 -92 -94 -93 -92 -94 -94 -93 -90 
    -97 -93 -92 -92 -90 -90 -93 -92 -92 -98 -92 -92 -92 -95 -95 -90 -92 -91 -92 -90 -91 -94 -93 -93 -92 -94 -94 -98 
    -93 -89 -91 -92 -91 -90 -92 -93 -93 -94 -94 -93 -94 -93 -94 -94 -93 -94 -93 -92 -91 -93 -94 -92 -92 -94 -93 -97 
    -92 -91 -93 -89 -91 -91 -92 -93 -92 -93 -90 -91 -94 -93 -94 -94 -94 -93 -93 -94 -92 -93 -93 -92 -92 -92 -91 -92 
    -92 -91 -93 -94 -91 -92 -93 -95 -92 -93 -90 -89 -92 -92 -92 -93 -94 -91 -91 -93 -94 -93 -89 -88 -93 -89 -89 -88 
    -90 -90 -91 -92 -92 -90 -91 -91 -93 -93 -93 -93 -95 -92 -93 -92 -91 -92 -93 -91 -92 -93 -90 -92 -88 -90 -94 -93 
    -95 -91 -90 -91 -91 -90 -91 -93 -93 -93 -91 -92 -91 -90 -94 -92 -88 -86 -92 -87 -91 -93 -90 -89 -90 -92 -92 -87 
    -95 -93 -93 -93 -92 -93 -93 -94 -93 -94 -91 -91 -86 -84 -93 -90 -88 -87 -91 -92 -93 -93 -91 -92 -92 -93 -91 -86 
    -88 -88 -90 -94 -92 -89 -90 -91 -91 -94 -90 -89 -89 -93 -93 -90 -90 -89 -91 -93 -93 -84 -90 -91 -91 -93 -91 -87 
    -85 -90 -89 -95 -92 -91 -89 -90 -91 -93 -89 -88 -88 -88 -90 -90 -88 -88 -91 -82 -89 -88 -88 -86 -88 -91 -90 -96 
    -89 -76 -90 -89 -91 -90 -93 -93 -92 -91 -90 -90 -88 -88 -87 -92 -91 -90 -92 -89 -92 -91 -91 -89 -88 -88 -89 -95 
    -88 -90 -91 -90 -90 -91 -89 -85 -92 -84 -86 -89 -92 -86 -95 -96 -92 -92 -92 -92 -91 -89 -89 -89 -96 -89 -87 -93 
    -96 -94 -89 -88 -91 -91 -94 -88 -85 -83 -89 -90 -91 -89 -90 -88 -91 -91 -90 -89 -90 -92 -91 -92 -92 -91 -88 -91 
    -92 -91 -92 -88 -92 -93 -87 -88 -90 -92 -89 -88 -89 -91 -91 -90 -90 -87 -91 -88 -91 -92 -90 -89 -91 -90 -92 -90 
    -91 -92 -93 -93 -92 -91 -90 -88 -84 -92 -89 -82 -91 -89 -91 -89 -88 -84 -90 -88 -90 -90 -89 -87 -90 -92 -92 -89 
    -95 -82 -93 -90 -88 -85 -89 -87 -86 -96 -88 -87 -87 -90 -90 -87 -81 -92 -87 -90 -92 -91 -89 -89 -91 -94 -88 -90 
    -93 -90 -90 -87 -87 -87 -90 -88 -89 -93 -88 -86 -80 -87 -85 -88 -91 -91 -91 -90 -87 -86 -88 -85 -90 -88 -86 -90 
    -91 -91 -91 -88 -81 -86 -91 -91 -82 -90 -88 -87 -85 -87 -86 -92 -88 -89 -90 -89 -88 -93 -88 -87 -88 -87 -87 -88 
    -91 -92 -91 -88 -86 -85 -87 -86 -84 -92 -86 -86 -82 -88 -86 -86 -85 -88 -89 -88 -89 -90 -90 -90 -88 -83 -87 -93 

    Quantized !
    Number of Elements = 10 
    prediction = 7

