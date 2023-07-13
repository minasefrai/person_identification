# person_identification
These are the steps for preparing the data, training a classification model, and executing the program for real-time face identification using a webcam. 
## Setup
Download the jetson-inference container from github to a jetson-nano: https://github.com/dusty-nv/jetson-inference

Change directories into `jetson-inference/python/training/classification/data`

Create a directory called `id`

Run this command in the terminal to download the data

Make 3 directories called `train`, `test`, and `val` in the `id` directory

Make a .txt file called `labels.txt` in the `id` directory and write down the following (in exactly that order) `Minas` `Sam` `backround`

Make 3 more directories called `Minas`, `Sam` and `backround` in each directory: `train`, `val`, and `test`

### Gathering Images

Take around 200 photos for each person and 100 for the backround in the train directory

Take around 80 photos for each person and 40 for the backround in the val directory

Take around 80 photos for each person and 40 for the backround in the test directory

Make a new directory called `id` in `jetson-inference/python/training/classification/models`

## Execution

Change directories to `jetson-inference`

Type and run `./docker/run.sh` in the terminal

Then change directories to `jetson-inference/python/training/classification`

Now train the model by running this command in the terminal `python3 train.py --model-dir=models/id data/id --epochs=35`

Once done, export the model by running this script

`python3 onnx_export.py --model-dir=models/id`

(If you are in the docker container, exit it by pressing `ctrl-d`)

Change directories to `jetson-inference/python/training/classification`

In the terminal enter in `NET=models/id` and `DATASET=data/id`

### Testing for final result

To run the program in real time using a webcam type `imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt /dev/video0`
