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

중고 거래 서비스에서 신뢰성을 높이기 위해 상품 매칭 서비스를 YOLO를 활용하여 구현하고자 한다.
YOLO를 통한 Object Detection 방법을 간단히 설명하면 아래와 같다.
(필수 준비 파일 : weight file, cfg file, names file, image file)
1) 먼저 파이썬 프로그램 실행 후 OpenCV와 numpy 모듈을 import한 후 YOLO를 로드한다.
![2021-12-06 (2)](https://user-images.githubusercontent.com/71023835/144865194-936f916e-2b87-4fad-ad10-7c716d39ba15.png)

2) 탐지할 물체가 있는 이미지 파일을 로드하고 이미지의 너비와 높이를 설정한 후, 이미지에서 물체를 탐지한다.
![2021-12-06 (4)](https://user-images.githubusercontent.com/71023835/144865235-2a49df1e-7eb4-476e-ac14-9a4648301b7a.png)

3) 신뢰도, 신뢰 임계값을 계산하고 결과를 화면에 표시하고 노이즈를 제거한다.
![2021-12-06 (5)](https://user-images.githubusercontent.com/71023835/144865259-7a013f9a-4b8a-4e65-8587-c5b356bb7d8f.png)

4) 모든 정보들을 추출하고 최종적인 결과물을 화면에 표시한다.
![2021-12-06 (6)](https://user-images.githubusercontent.com/71023835/144865306-62406472-cf12-4f86-ba72-3f34201e30fd.png)

5) 결과는 다음과 같다.
![2021-11-24 (5)](https://user-images.githubusercontent.com/71023835/144863848-728c5b75-8c63-42b9-b5a3-7908554c5438.png)

위와 같이 Object Detection으로 상품 매칭 서비스를 제공할 수 있다.

## 2. 챗봇

chatbot


## 3. 결함도 측정

defect
