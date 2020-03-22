***Installing docker and tensorflow/serving***
1. Install docker according to the instructions in the official docker website [Docker installation](https://docs.docker.com/install/) </br>
2. Run the command to ***docker pull tensorflow/serving*** in the command line  </br>

**To run as a server***
Run the following command in the commandline to host as a server</br>

*sudo docker run -p 8500:8500 -p 8501:8501   --mount type=bind,source=/home/likhitha/Documents/Projects/object-detection/DetectionModel/1,target=/models/detection_model/0001   --mount type=bind,source=/home/likhitha/Documents/Projects/object-detection/LabelDetector/1,target=/models/label_detector/0001  --mount type=bind,source=/home/likhitha/Documents/Projects/object-detection/config.conf,target=/models/config.conf   -t tensorflow/serving --model_config_file=/models/config.conf* </br>


Change the following: </br>
1. source - *Path to the inference graph obtained* for both void detector and label detector </br>
2. Make a config file with the follwing contents and add the path accordingly </br> 

*
model_config_list: {</br>
  config: {</br>
    name:  "detection_model",</br>
    base_path:  "/models/detection_model",</br>
    model_platform: "tensorflow",</br>
    model_version_policy: {</br>
        all: {}</br>
    }</br>
  },</br>
  config: {</br>
    name:  "label_detector",</br>
    base_path:  "/models/label_detector",</br>
    model_platform: "tensorflow",</br>
    model_version_policy: {</br>
        all: {}</br>
    }</br>
  }</br>
}</br>

*

Change the name to the target name given, and mention the base_path without the '0001'


***Program to run from the client side***
**client_request.py*** </br>

Make sure to keep the file **visualization_utils.py** in the same folder as the **client_request.py*** program.</br>


Change the paths of the resized_test_data, original test data, destination path for the inference labels as well as the category indices.</br>