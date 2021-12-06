# matchat

**딥러닝 기반 중고거래 플랫폼**  
***match**ing + **chat**bot = **matchat***  

팀명 : i4 아이포 (**i**ntelligent한 4명으로 구성된 팀)  
팀원 : 설유진, 원소윤, 이현주, 조하연   


# 프로젝트 소개


기존의 다양한 중고거래 플랫폼의 경우, 구매자와 판매자 간의 소통을 중요시하며 직거래를 통한 거래를 권장하고 있다. 
하지만 이런 거래 방식이 불편한 이용자들 또한 존재한다. 직거래가 부담스러운 이용자들은 상품의 전달의 위해 택배를 이용하게 되는데 이때 정확한 상품이 전달되지 않는다는 문제점이 발생한다. 
또한 판매자와 구매자 간의 상품에 대한 문의가 이루어 지는 과정에서 늦은 시간까지 문의가 이어지거나 터무니없는 요구를 하는 등의 비매너적인 태도가 문제가 되고 있으며 문의에 대한 즉각적으로 답변이 서로 이루어지기 어려워 소통이 원활하지 않다는 문제점 또한 발생하고 있다. 

본 프로젝트는 하드웨어 기술이 접목된 딥러닝 기반 중고거래 플랫폼으로 이와 같은 문제점들을 해결하고자 한다.
하드웨어 기술로는 판매할 상품을 스캔할 수 있는 환경을 제공하고자 카메라와 조명, 턴테이블, 잠금장치가 설치된 사물함을 설계하였고 딥러닝 기술을 이용한 상품 매칭, 결함도 측정, 챗봇 기능을 통해 
새로운 중고거래 플랫폼을 구상하였다.

문제점을 해결하기 위해 설계한 시나리오는 아래와 같다.

[판매자] : 판매할 상품의 사진과 기본 정보들을 앱을 통해 사전 등록한다. 상품을 사물함에 넣어 스캔 과정을 거친 후, 사물함에 넣은 상품과 사전 등록한 상품이 동일한지 확인한다. 동일한 상품이라면 판매 상품으로 확정되며 상품의 결함도 분석이 진행된다. 이 모든 과정을 마치면 상품에 대한 종합적인 정보들은 앱에 판매 상품으로 자동 등록된다.

[구매자] : 앱을 통해 상품 목록을 확인할 수 있으며 구매하고자 하는 상품이 있으면 챗봇을 통해 문의할 수 있다.

따라서, 본 플랫폼에는 상품 매칭, 결함도 분석, 챗봇 3가지 주요 기능을 가진다.

# 프로젝트 아키텍쳐

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FH1Fbm%2FbtrneZqWv0G%2FOGi6Ca4GjRWr0vDTmkVhs0%2Fimg.jpg"  width="60%" height="60%"/>

# 주요기능 및 기술

📌 [상품 매칭](#1-상품-매칭)  
📌 [챗봇](#2-챗봇)  
📌 [결함도 측정](#3-결함도-측정)    


## 1. 상품 매칭

중고 거래 서비스에서 신뢰성을 높이기 위해 상품 매칭 서비스를 YOLO를 활용하여 구현하고자 한다.

YOLO를 통한 Object Detection 방법을 간단히 설명하면 아래와 같다.
(필수 준비 파일 : weight file, cfg file, names file, image file)
#### 1. 먼저 파이썬 프로그램 실행 후 OpenCV와 numpy 모듈을 import한 후 YOLO를 로드한다.
![2021-12-06 (2)](https://user-images.githubusercontent.com/71023835/144865194-936f916e-2b87-4fad-ad10-7c716d39ba15.png)
#### 2. 탐지할 물체가 있는 이미지 파일을 로드하고 이미지의 너비와 높이를 설정한 후, 이미지에서 물체를 탐지한다.
![2021-12-06 (4)](https://user-images.githubusercontent.com/71023835/144865235-2a49df1e-7eb4-476e-ac14-9a4648301b7a.png)
#### 3. 신뢰도, 신뢰 임계값을 계산하고 결과를 화면에 표시하고 노이즈를 제거한다.
![2021-12-06 (5)](https://user-images.githubusercontent.com/71023835/144865259-7a013f9a-4b8a-4e65-8587-c5b356bb7d8f.png)
#### 4. 모든 정보들을 추출하고 최종적인 결과물을 화면에 표시한다.
![2021-12-06 (6)](https://user-images.githubusercontent.com/71023835/144865306-62406472-cf12-4f86-ba72-3f34201e30fd.png)
#### 5. 결과는 다음과 같다.
<img src="https://user-images.githubusercontent.com/71023835/144863848-728c5b75-8c63-42b9-b5a3-7908554c5438.png"  width="40%" height="40%"/>

위와 같이 YOLO를 통한 Object Detection으로 판매자가 앱에 등록한 물건과 실제 물건을 비교하여 동일 상품인지 판별해 낼 예정이다.


## 2. 챗봇

chatbot


## 3. 결함도 측정

<img width="500" alt="딥러닝" src="https://user-images.githubusercontent.com/71023835/144868608-e8a2b1fa-e6e8-47c7-be3f-42d1927d853e.png">
추후 CNN을 이용해 결함도 분석 모델을 만들 예정이다.  


## 참고자료
### YOLO
- weight file  
https://drive.google.com/drive/folders/134DOgNAlOXORLMOxeh9ysrxjV23LCFbR?usp=sharing  
- weight file custom_heel  
https://drive.google.com/drive/folders/1dsoOYzUN85VswM3KSvK2cydDm6q8a9p8?usp=sharing  
- how to use yolo?    
https://pysource.com/2019/06/27/yolo-object-detection-using-opencv-with-python/  
- how to customize yolo?  
https://www.youtube.com/watch?v=51fZ2FTau7E  

### Dialogflow
- dialogflow  
https://dialogflow.cloud.google.com/  
- how to use dialogflow?  
https://m.blog.naver.com/spring1a/221386879776  
