# Hand-Gesture-Recognition-using-Mediapipe
Estimate hand pose using MediaPipe (Python version).<br> This is a sample 
program that recognizes hand signs and finger gestures with a simple MLP using the detected key points.


![102222442-c452cd00-3f26-11eb-93ec-c387c98231be](https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/ac3bd184-6a5c-4876-8dec-5db5cb33454b)

This repository contains the following contents.
* Sample program
* Hand sign recognition model(TFLite)
* Finger gesture recognition model(TFLite)
* Learning data for hand sign recognition and notebook for learning
* Learning data for finger gesture recognition and notebook for learning

# Requirements
* mediapipe 0.8.1
* OpenCV 3.4.2 or Later
* Tensorflow 2.3.0 or Later<br>tf-nightly 2.5.0.dev or later (For creating a TFLite for an LSTM model)
* scikit-learn 0.23.2 or Later (for displaying the confusion matrix) 
* matplotlib 3.3.2 or Later (For displaying the confusion matrix)

# Demo
Run app.py for the demo.
The following options can be specified when running the demo.
* --device<br>Specifying the camera device number (Default：0)
* --width<br>Width at the time of camera capture (Default：960)
* --height<br>Height at the time of camera capture (Default：540)
* --use_static_image_mode<br>Whether to use static_image_mode option for MediaPipe inference (Default：Unspecified)
* --min_detection_confidence<br>
Detection confidence threshold (Default：0.5)
* --min_tracking_confidence<br>
Tracking confidence threshold (Default：0.5)

# Details
### app.py
This is a sample program for inference.<br>
In addition, learning data (key points) for hand sign recognition,<br>
You can also collect training data (index finger coordinate history) for finger gesture recognition.

### keypoint_classification.ipynb
This is a model training script for hand sign recognition.

### point_history_classification.ipynb
This is a model training script for finger gesture recognition.

### model/keypoint_classifier
This directory stores files related to hand sign recognition.<br>
The following files are stored.
* Training data(keypoint.csv)
* Trained model(keypoint_classifier.tflite)
* Label data(keypoint_classifier_label.csv)
* Inference module(keypoint_classifier.py)

### model/point_history_classifier
This directory stores files related to finger gesture recognition.<br>
The following files are stored.
* Training data(point_history.csv)
* Trained model(point_history_classifier.tflite)
* Label data(point_history_classifier_label.csv)
* Inference module(point_history_classifier.py)

### utils/cvfpscalc.py
This is a module for FPS measurement.

# Training
Hand sign recognition and finger gesture recognition can add and change training data and retrain the model.
### Hand sign recognition training
#### 1.Learning data collection
Press "k" to enter the mode to save key points（displayed as 「MODE:Logging Key Point」）<br>
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/fba821ef-9bf4-40e1-bcf3-9c11a1c28526" width="60%"><br><br>

If you press "0" to "9", the key points will be added to "model/keypoint_classifier/keypoint.csv" as shown below.<br>
1st column: Pressed number (used as class ID), 2nd and subsequent columns: Key point coordinates<br>
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/ab3b2d39-3a5f-48f0-9a96-4aba1545782f" width="80%"> <br><br>

The key point coordinates are ---.<br>
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/0aa027c8-5bcd-4ade-8eb0-fd96bc9a0de3" width="80%"> <br><br>

In the initial state, three types of learning data are included: open hand (class ID: 0), close hand (class ID: 1), and pointing (class ID: 2).<br>

<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/44cf6691-9333-43d6-ab3b-793f13646240" width="25%">　<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/29ec8c64-50f6-4599-b27e-83a3e6b46d7c" width="25%">　<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/53bd3c25-aaf5-4bef-b80b-d61ae4c405a2" width="25%">

#### 2.Model training
The "[keypoint_classification.ipynb](keypoint_classification.ipynb)" contains the model training details. <br><br>

#### 3.Model structure
The image of the model prepared in "[keypoint_classification.ipynb](keypoint_classification.ipynb)" is as follows.
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/d7df6701-a1fb-441d-9ab2-a5c4c05fa5bb" width="50%"><br><br>

### Finger gesture recognition training
#### 1.Learning data collection
Press "h" to enter the mode to save the history of fingertip coordinates (displayed as "MODE:Logging Point History").<br>
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/1d844647-8c0e-409f-a558-86da5a038dec" width="60%"><br><br>
If you press "0" to "9", the key points will be added to "model/point_history_classifier/point_history.csv" as shown below.<br>
1st column: Pressed number (used as class ID), 2nd and subsequent columns: Coordinate history<br>
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/dca5b241-ab2f-46fc-b76e-c931c4968cf2" width="80%"><br><br>

In the initial state, 4 types of learning data are included: stationary (class ID: 0), clockwise (class ID: 1), counterclockwise (class ID: 2), and moving (class ID: 4). <br><br>
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/9f5ad166-8cc9-4791-8225-d9a031e4758a" width="20%">　<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/ba8dc561-1070-4941-8e94-6cf3c5cdcc78" width="20%">　<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/15c7043b-e614-4932-bf79-c2fdafbfd6f9" width="20%">　<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/90072df1-235d-45bd-8fbe-e63d5294afec" width="20%">

#### 2.Model training
The "[point_history_classification.ipynb](point_history_classification.ipynb)" contains model training details.<br><br>

#### X.Model structure
The image of the model prepared in "[point_history_classification.ipynb](point_history_classification.ipynb)" is as follows.
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/23f66382-0796-4aa2-9d79-d65e2d10e594" width="50%"><br>
The model using "LSTM" is as follows. <br>
<img src="https://github.com/flawed-hooman/Hand-Gesture-Recognition-using-MediaPipe/assets/117461708/0f444ef8-77f0-49ac-9451-9f64bb91b22f" width="60%">

# Reference
* [MediaPipe](https://mediapipe.dev/)

# License 
Hand-Gesture-Recognition-using-Mediapipe is under [Apache v2 license](LICENSE).

