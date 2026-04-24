# Cat and Dog Detector

A real-time object detection system that identifies cats and dogs 
using an Arduino UNO Q board and a trained AI model.

## Hardware Requirements
- Arduino UNO Q (Qualcomm-based)
- USB Camera
- Computer with Arduino App Lab installed

## Software Requirements
- Arduino App Lab v0.6.0
- Edge Impulse model (ei-model-972844-1)

## How It Works
The system uses a VideoObjectDetection brick powered by an 
Edge Impulse trained model to analyze live camera feed and 
classify detected objects as either a cat or a dog, 
along with a confidence percentage.

## Code

from arduino.app_utils import App
from arduino.app_bricks.video_objectdetection import VideoObjectDetection

detection_stream = VideoObjectDetection(confidence=0.5, debounce_sec=0.0)

def print_detections(detections: dict):
    for key, value in detections.items():
        for detection in value:
            entry = {
                "content": key,
                "confidence": f"{round(detection.get('confidence', 0) * 100)}%"
            }
            print(entry)

detection_stream.on_detect_all(print_detections)
App.run()

## Known Issues
- Requires stable internet connection on the board
- Board DNS may need manual configuration using Google DNS (8.8.8.8)

## Author
itsmefarisi
