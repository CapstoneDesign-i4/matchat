# matchat

**딥러닝 기반 중고거래 플랫폼**  
***match**ing + **chat**bot = **matchat***  

팀명 : i4 아이포 (**i**ntelligent한 4명으로 구성된 팀)  
팀원 : 설유진, 원소윤, 이현주, 조하연   


# 프로젝트 소개

프로젝트 배경
```

```

타겟
```
target
```


# 주요기술

📌 [상품 매칭](#1-상품-매칭)  
📌 [챗봇](#2-챗봇)  
📌 [결함도 측정](#3-결함도-측정)    


## 1. 상품 매칭

matching  

YOLO를 통한 Object Detection 방법은 아래와 같다.
(필수 준비 파일 : weight file, cfg file, names file, image file)
1) 먼저 파이썬 프로그램 실행 후 OpenCV와 numpy 모듈을 import한 후 YOLO를 로드한다.
import cv2
import numpy as np 

net = cv2.dnn.readNet("yolov3.weights", "yolov3.cfg")
classes = []
with open("coco.names", "r") as f:
    classes = [line.strip() for line in f.readlines()]
layer_names = net.getLayerNames()
output_layers = [layer_names[i - 1] for i in net.getUnconnectedOutLayers()]
colors = np.random.uniform(0, 255, size=(len(classes), 3))

2) 이후 탐지할 물체가 있는 이미지 파일을 로드하고 이미지의 너비와 높이를 설정한 후, 이미지에서 물체를 탐지한다.
img = cv2.imread("images.jpg")
img = cv2.resize(img, None, fx=0.4, fy=0.4)
height, width, channels = img.shape

blob = cv2.dnn.blobFromImage(img, 0.00392, (416, 416), (0, 0, 0), True, crop=False)
net.setInput(blob)
outs = net.forward(output_layers)

3) 신뢰도, 신뢰 임계값을 계산하고 결과를 화면에 표시하고 노이즈를 제거한다.
class_ids = []
confidences = []
boxes = []
for out in outs:
    for detection in out:
        scores = detection[5:]
        class_id = np.argmax(scores)
        confidence = scores[class_id]
        if confidence > 0.5:
            # Object detected
            center_x = int(detection[0] * width)
            center_y = int(detection[1] * height)
            w = int(detection[2] * width)
            h = int(detection[3] * height)
            # Rectangle coordinates
            x = int(center_x - w / 2)
            y = int(center_y - h / 2)
            boxes.append([x, y, w, h])
            confidences.append(float(confidence))
            class_ids.append(class_id)

indexes = cv2.dnn.NMSBoxes(boxes, confidences, 0.5, 0.4)

4) 모든 정보들을 추출하고 최종적인 결과물을 화면에 표시한다.
font = cv2.FONT_HERSHEY_PLAIN
for i in range(len(boxes)):
    if i in indexes:
        x, y, w, h = boxes[i]
        label = str(classes[class_ids[i]])
        color = colors[i]
        cv2.rectangle(img, (x, y), (x + w, y + h), color, 2)
        cv2.putText(img, label, (x, y + 30), font, 3, color, 3)
cv2.imshow("Image", img)
cv2.waitKey(0)
cv2.destroyAllWindows()

5) 결과는 다음과 같다.
![2021-11-24 (2)](https://user-images.githubusercontent.com/71023835/144863277-b51971f2-9c54-46f0-8476-7dc8af3848b1.png)


## 2. 챗봇

chatbot


## 3. 결함도 측정

defect
