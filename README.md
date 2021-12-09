# matchat

**딥러닝 기반 중고거래 플랫폼**  
***match**ing + **chat**bot = **matchat***  

팀명 : i4 아이포

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
프로젝트 구조는 크게 HW와 SW 로 나눌 수 있다.

HW구조는 상품을 넣을 사물함이 있고 외부에는 잠금장치, 내부에는 카메라, 조명, 턴테이블 ,모터를 설치해 상품을 촬영할 환경을 갖춘 사물함을 설계했다.

SW구조로는 판매자와 구매자 모두가 이용할 앱을 만들어 인터넷과 연결하고 서버의 데이터에는 앱과 HW에서 전달받은 각종 정보들을 저장할 수 있도록 한다. 

# 주요기능 및 기술

📌 [상품 매칭](#1-상품-매칭)  
📌 [챗봇](#2-챗봇)  
📌 [결함도 측정](#3-결함도-측정)    


## 1. 상품 매칭

중고 거래 서비스에서 신뢰성을 높이기 위해 상품 매칭 서비스를 YOLO를 활용하여 구현하고자 한다.
YOLO는 real-time object detection system으로 입력 이미지를 여러 grid로 나누고 
grid별로 탐지한 물체의 신뢰도를 비교하여 물체를 인식한다.
YOLO는 단일 신경망 구조를 가져 단순하고 빠르다는 특징이 있다.
우리팀은 보편적으로 많이 사용되는 YOLO 3를 사용하여 Object Detection을 검증하였다.

YOLO를 통한 Object Detection 방법을 간단히 설명하면 아래와 같다.  
(필수 준비 파일 : weight file, cfg file, names file, image file)  
weight file의 경우, 하단 [참고자료](#참고자료)에서 다운로드 가능하다  

#### 1. 먼저 파이썬 프로그램 실행 후 OpenCV와 numpy 모듈을 import한 후 YOLO를 로드한다.
![1](https://user-images.githubusercontent.com/71023835/145358928-40af8cbd-82e0-48eb-af89-db7a5a730c48.png)
#### 2. 탐지할 물체가 있는 이미지 파일을 로드하고 이미지의 너비와 높이를 설정한 후, 이미지에서 물체를 탐지한다.
![2](https://user-images.githubusercontent.com/71023835/145358953-4462807c-ea02-44f9-ac4a-34c4b5891a0c.png)
#### 3. 신뢰도, 신뢰 임계값을 계산하고 결과를 화면에 표시하고 노이즈를 제거한다.
![3](https://user-images.githubusercontent.com/71023835/145358968-8f32ce4d-c607-43ce-bfd1-528e65fe356b.png)
#### 4. 모든 정보들을 추출하고 최종적인 결과물을 화면에 표시한다.
![4](https://user-images.githubusercontent.com/71023835/145358991-4d21617f-e585-4c75-bd59-01ce6e064628.png)
#### 5. 결과는 다음과 같다.
<img src="https://user-images.githubusercontent.com/71023835/144863848-728c5b75-8c63-42b9-b5a3-7908554c5438.png"  width="50%" height="50%"/>

위와 같이 YOLO를 통한 Object Detection으로 판매자가 앱에 등록한 물건과 실제 물건을 비교하여 동일 상품인지 판별해 낼 예정이다.


## 2. 챗봇

Dialogflow는 구글에서 제공하는 자연어 이해 플랫폼으로 대화형 사용자 인터페이스를 설계하고 통합할 수 있다. 챗봇 기술을 검증하기 위해 Dialogflow에서 챗봇을 생성하였다. 상품 구매 전후로 예상되는 사용자의 질문을 선정하고, 챗봇이 질문에 적절하게 응답할 수 있는 지 확인해보았다.  

#### 1. 질문의 핵심 단어가 되는 entity를 설정한다. 상품 문의에 자주 쓰이는 단어인 사용기간이나 횟수, 포장, 수령지 등을 entity로 설정하였다. 이때 Define synonyms 기능으로 동의어도 한 entity로 인식할 수 있도록 다양하게 등록한다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGw1WT%2FbtrnpewGmAz%2FalD11Ra4k2mx1skjxVbGKK%2Fimg.png"  width="50%" height="50%"/>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmDFgp%2Fbtrnv3fNZt3%2FdenHSeieAwRZvj2buRyP3K%2Fimg.png"  width="50%" height="50%"/>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPwuHG%2Fbtrnw8VhGg8%2FSwVhRuq6ImwyekzjRXKthK%2Fimg.png"  width="50%" height="50%"/>

#### 2. 각 entity를 포함하는 사용자의 질문인 intent를 생성한다. 질문은 모델의 정확도를 높일 수 있도록 다양한 형태로 생성한다. 
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmKhyA%2FbtrnxlUAjJO%2FeWkCBqNWdlB5LE4NXa95D0%2Fimg.png"  width="50%" height="50%"/>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbs00gK%2FbtrnwyzQQGi%2FtGrPVnSyPNYosZIIXH4pGk%2Fimg.png"  width="50%" height="50%"/>

#### 3. 각 질문에 해당하는 대답인 response를 생성한다. 
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcB2Jv5%2FbtrnvpwRChP%2F3BRgj5MvHnaKdLyERWajqK%2Fimg.png"  width="50%" height="50%"/>

#### 4. 챗봇을 실행시켜본 결과, 챗봇이 사용자의 질문에 적절하게 답변하는 모습을 볼 수 있다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtM3N5%2FbtrnwyNo3rv%2FbRqMOgpRNnbFL3KdvQEYtK%2Fimg.png"  width="50%" height="50%"/>

#### 결과 영상 링크 : https://youtu.be/7JS65KC21m4    

![image](https://user-images.githubusercontent.com/66419086/145352721-0595dbbf-1444-4907-b968-6683cb796ace.png)

프로젝트에 챗봇을 적용할 때에는 챗봇이 개별 상품의 정보를 불러와 대답할 수 있어야 하기 때문에, Dialogflow와 외부간의 데이터 이동이 필요하다. 추후 프로젝트를 진행하며 Dialogflow와 상품 정보가 저장된 DB간의 연결, fulfillment 기능을 사용한 Webhook 연동 등을 구현할 예정이다.

## 3. 결함도 측정

<img width="500" alt="딥러닝" src="https://user-images.githubusercontent.com/71023835/144868608-e8a2b1fa-e6e8-47c7-be3f-42d1927d853e.png">
추후 CNN을 이용해 결함도 분석 모델을 만들 예정이다.  


## 참고자료
### YOLO
- weight file  
https://drive.google.com/drive/folders/134DOgNAlOXORLMOxeh9ysrxjV23LCFbR?usp=sharing  
- weight file custom_heel  
https://drive.google.com/drive/folders/1dsoOYzUN85VswM3KSvK2cydDm6q8a9p8?usp=sharing  
- what is YOLO? (demo video)  
https://www.youtube.com/watch?v=MPU2HistivI&t=2s  
- how to use yolo?    
https://pysource.com/2019/06/27/yolo-object-detection-using-opencv-with-python/  
- how to customize yolo?  
https://www.youtube.com/watch?v=51fZ2FTau7E  

### Dialogflow
- dialogflow  
https://dialogflow.cloud.google.com/  
- how to use dialogflow?   
https://m.blog.naver.com/spring1a/221386879776  
- about dialogflow database - dialogflow fulfillment webhook  
https://medium.com/@jwlee98/gcp-dialogflow-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EA%B0%84%EB%8B%A8-%EC%B1%97%EB%B4%87-%EB%A7%8C%EB%93%A4%EA%B8%B0-2%ED%83%84-7183888d0af5  
- about dialogflow fulfillment  
https://cloud.google.com/dialogflow/es/docs/fulfillment-overview  
- how to make a webhook for dialogflow fulfillment?   
https://medium.com/@pallavtrivedi03/how-to-make-a-webhook-for-dialogflow-fulfillment-d02835cc50bf  

### MATCHAT
- prototype  
https://youtu.be/WCe3IZg5uL4

- demo video  
https://youtu.be/Dn5SUPLCS60
