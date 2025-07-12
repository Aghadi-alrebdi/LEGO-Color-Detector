# LEGO-Color-Detection

---

## Project Title  
**Real-Time Detection of LEGO Brick Colors using OpenCV**

---

## Objective  
The objective of this project is to create a real-time color detection system that identifies **LEGO brick colors** using a webcam. The program uses **OpenCV** to process video frames and classify colors based on HSV ranges.

---

## Description  
This project detects LEGO bricks based on their colors using color thresholding in HSV color space. It identifies six different LEGO colors:

- **Red**
- **Blue**
- **Green**
- **Yellow**
- **Black**
- **White**

The webcam feed is processed in real-time, and a rectangle at the center of the screen is used to analyze the region of interest (ROI). The detected color is displayed on the video feed.

---

## Tools and Platform  
- **Language**: Python  
- **Libraries**:
  - OpenCV
  - NumPy  
- **Platform**: Local Machine with a webcam  
- **Color Model**: HSV (Hue, Saturation, Value)

---

## LEGO Color Detection Code  

```python
import cv2
import numpy as np


LEGO_COLORS = {
    "Red":    [[0, 100, 100], [10, 255, 255]],
    "Blue":   [[100, 100, 50], [130, 255, 255]],
    "Green":  [[40, 50, 50], [80, 255, 255]],
    "Yellow": [[20, 100, 100], [30, 255, 255]],
    "Black":  [[0, 0, 0], [180, 255, 50]],      
    "White":  [[0, 0, 200], [180, 50, 255]]     
}

def detect_color(frame):
    
    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
    
    for color_name, (lower, upper) in LEGO_COLORS.items():
        
        mask = cv2.inRange(hsv, np.array(lower), np.array(upper))
        
        if cv2.countNonZero(mask) > 100:  
            return color_name
    
    return "Unknown"

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret: break
    
    height, width = frame.shape[:2]
    roi = frame[height//2-100:height//2+100, width//2-100:width//2+100]
    
    color_name = detect_color(roi)
    
    cv2.rectangle(frame, (width//2-100, height//2-100), 
                 (width//2+100, height//2+100), (0, 255, 0), 2)
    cv2.putText(frame, f"Color: {color_name}", (10, 30), 
               cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 0, 0), 2)
    
    cv2.imshow('LEGO Color Detector', frame)
    if cv2.waitKey(1) == 27: break  

cap.release()
cv2.destroyAllWindows()

```

---

## Project Screenshot  
Below are screenshots of the LEGO color detection interface at different moments:

![Screenshot 1 - Red Brick Detection](screenshot-red.jpg)

![Screenshot 2 - Green Brick Detection](screenshot-green.jpg)

![Screenshot 3 - Blue Brick Detection](screenshot-blue.jpg)


---

## Created By  
- **Name**: Aghadi Saleh Al-rebdi   
- **Department**: Computer Science  
- **Year**: 2025  
