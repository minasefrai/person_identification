# person_identification
These are the steps for preparing the data, training a classification model, and executing the program for real-time face detection using a webcam. 
## Setup

1. Download the jetson-inference container from github to a jetson-nano: https://github.com/dusty-nv/jetson-inference

2. Change directories into `jetson-inference/python/training/classification/data`

3. Create a directory called `id`

4. Run this command in the terminal to download the data

5. Make 3 directories called `train`, `test`, and `val` in the `id` directory

6. Make a .txt file called `labels.txt` in the `id` directory and write down the following (in exactly that order) `Minas` `Sam` `backround`

7. Make 3 more directories called `Minas`, `Sam` and `backround` in each directory: `train`, `val`, and `test`

### Gathering Images

1. Take around 200 photos for each person and 100 for the backround in the train directory

2. Take around 80 photos for each person and 40 for the backround in the val directory

3. Take around 80 photos for each person and 40 for the backround in the test directory

4. Make a new directory called `id` in `jetson-inference/python/training/classification/models`

## Execution

1. Change directories to `jetson-inference`

2. Type and run `./docker/run.sh` in the terminal

3. Then change directories to `jetson-inference/python/training/classification`

4. Now train the model by running this command in the terminal `python3 train.py --model-dir=models/id data/id --epochs=35`

5. Once done, export the model by running this script `python3 onnx_export.py --model-dir=models/id`
(If you are in the docker container, exit it by pressing `ctrl-d`)

6. Change directories to `jetson-inference/python/training/classification`

7. In the terminal enter in `NET=models/id` and `DATASET=data/id`

### Testing for final result

* To run the program in real time using a webcam type `imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt /dev/video0`
