# Weed-Detection: Real-Time Serverless Weed Detection

## Requirements

Please use Yolov8 on Python 3.11 and not Python 3.12. At the time of writing, TFjs has issues in Python 3.12 which prevents successful conversion of the model to TF.js

```bash
$ pip install ultralytics
```

## Modeling

The data for model training was combined from two Kaggle datasets and can be found [here](https://app.roboflow.com/weeddetection-dab2e/cw-6rehh/1)

The modeling steps were performed on Pycharm, while the web deployment was performed on Visual Studio Code.

### 1. Training

Run this code to train the model based on the pretrained weights **yolov8n** from COCO.
```bash
$ yolo detect train data=coco8.yaml model=path/to/yaml epochs=100 imgsz=640
```
To train the on a custom dataset, on your custom data file, replace path/to/yaml with the path from you current directory to the yaml with your data file.

After training, you can get the model weights from runs/detect/your most recent run/best.pt

To export the model to TFjs format, make sure tensorflow and all its depedencies are installed and run 

```bash
$ yolo export model=path/to/best.pt format=tfjs
```
The model will be ran on 


### 2. Inference 

To test the models performance, you can run 
```bash
$ yolo detect val model=path/to/best.pt
```
To test it on the testing dataset, change the validation path in the yaml to your testing path

## Deployment

Clone this repository

Copy `nameofyourwebmodel` to `./public`

Update `modelName` in `App.jsx` to new model name
```jsx
...
// model configs
const modelName = "nameofyourwebmodel"; // change to new model name
...
```
**Scripts for testing/building**

**Make sure you change the base parameter in the vite.config.js file to the name of your github repository or else the source page will look for the wrong file**

```bash
yarn start # Start dev server
yarn build # Build for productions
```
## Acknowledgement

The starting model used is modified from the [Ultralytics](https://github.com/ultralytics/ultralytics) model. Thanks to [Hyuto](https://github.com/Hyuto), for his creation of the initial javascript implementation.




