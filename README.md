<!--- Licensed to the trainML under one -->
<!--- or more contributor license agreements.  See the NOTICE file -->
<!--- distributed with this work for additional information -->
<!--- regarding copyright ownership.  The trainML this file -->
<!--- to you under the Apache License, Version 2.0 (the -->
<!--- "License"); you may not use this file except in compliance -->
<!--- with the License.  You may obtain a copy of the License at -->

<!---   http://www.apache.org/licenses/LICENSE-2.0 -->

<!--- Unless required by applicable law or agreed to in writing, -->
<!--- software distributed under the License is distributed on an -->
<!--- "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY -->
<!--- KIND, either express or implied.  See the License for the -->
<!--- specific language governing permissions and limitations -->
<!--- under the License. -->

<div align="center">
  <a href="https://www.trainml.ai/"><img src="https://www.trainml.ai/static/img/trainML-logo-purple.png"></a><br>
</div>


trainML Tutorials - Hyperparameter Tuning an Object Detection Model with MXNet on VOC
=====
Before beginning this tutorial, ensure you have created an account on the [trainML platform](https://app.trainml.ai) and you have [Docker](https://docs.docker.com/get-docker/) installed.

> This tutorial should cost less than 150 credits (\$15) if you use the small or medium instance type and the same setting as the guide. Tuning takes approximately 15 hours using 4 medium GPUs or 30 hours using 4 small GPUs.

This tutorial uses the [MXNet Faster-RCNN object detection example](https://gluon-cv.mxnet.io/build/examples_detection/train_faster_rcnn_voc.html) to perform a parallelized hyperparameter tuning job on [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) using the [hyperopt](https://github.com/hyperopt/hyperopt) library.

## Instructions

1. Clone this repo to a local directory and place it in a new python virtual environment
2. Install the prerequisites `pip install -r requirements.txt`
3. Prepare the local directory and download the dataset:

```
mkdir mongodb
python pascal_voc.py
rm ~/.mxnet/datasets/voc/*.tar
rm ~/.mxnet/datasets/voc/benchmark.tgz
```
4. In a new terminal window, navigate to the root of the repository and run:

```
docker run -v $(pwd)/mongodb:/data/db -p 27017:27017 mongo
```
5.  In the previous terminal window, run `python tune.py`
6. Create a job on the [trainML platform](https://app.trainml.ai) with the settings documented in the [tutorial guide](https://docs.trainml.ai/tutorials/basic/mxnet-voc-object-detection-hyperparameter-tuning#starting-trainml-workers)
7. Connect to the job by following the instructions in the [getting started guide](https://docs.trainml.ai/getting-started/running-training#monitoring-the-job) in a separate terminal window.

> You must keep the trainML connect utility, the `python tune.py` script, and the MongoDB docker container running for the full duration of the experiment. If any one of the 3 stop, the workers will no longer be able to report their results and find new workloads and will eventually terminate.

8. Once all 50 trials are evaluated, the final statement should print out the results of the experiment,