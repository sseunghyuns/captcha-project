# captcha_project
## Opencv 라이브러리를 활용하여 이미지 속의 수식 추출하기

captcha_project는  유튜버 '동빈나'님의 [Python 데이터 분석과 이미지 처리](https://www.youtube.com/watch?v=V8Lpf3WCZ4g&list=PLRx0vPvlEmdBx9X5xSgcEk4CEbzEiws8C) 영상을 참고하여 진행했습니다.  

---

### 소개

이번 프로젝트에서는 아래의 이미지에서처럼 수식이 그려진 이미지를 풀어 답을 제출하는 것을 목표로 하고 있습니다. 80초의 주어진 시간 동안 100개의 수식에 대한 답을 해야하기  직접 눈으로 문제를 보면서 푸는 것은 불가능합니다. 따라서 이러한 문제를 풀기 위해, 문제로 나온 이미지를 다운로드 받아 이미지가 담고 있는 수식을 해독을 한 다음, 자동으로 연산을 하여 해당 결과를 웹사이트로 보내주는 자동화 프로그램을 개발해야 합니다.  
<img width="500" alt="스크린샷 2021-10-04 오후 3 14 32" src="https://user-images.githubusercontent.com/63924704/135802395-99361bf0-dd51-43c0-b18b-7ee6daf978de.png">

---

### 알고리즘  

문제 해결을 위해 `OpenCV`를 사용하여 이미지 처리하는 방법들을 공부했습니다. 아래는 문제를 해결하기 위한 단계입니다.
* 1. 수식이 담긴 이미지를 OpenCV를 통해 각 문자를 하나씩 분리합니다. 
* 2. 분리된 각 문자가 어떤 문자에 해당하는지 인식합니다. 문자 인식을 위해 kNN모델을 사용하였는데, 이를 위해 우선 `make_train_data.py`로 0~9까지의 숫자와 +,-,x 연산의 이미지들을 수집하여 학습 가능한 형태로 가공하였습니다. 그후 kNN 모델을 학습하여 특정한 숫자 혹은 연산자를 나타내는 이미지가 들어왔을때, 어떤 숫자/연산  모델의 추출값을 통해 알 수 있게 하였습니다.
* 3. 인식된 수식을 계산하여 답을 도출합니다. 

<img width="500" alt="captcha" src="https://user-images.githubusercontent.com/63924704/135803243-2198f49d-1022-4584-93df-bef9abce0919.png">

---

### 결과  
이번 프로젝트에서 배우고 적용한 부분들을 요약하면 아래와 같습니다.

* 이미지 속의 숫자들을 정확히 분류하기 위해 KNN모델을 적용
* 이미지 속의 수식을 문자열 형태로 추출하여 자동으로 연산하는 알고리즘을 구성

결과는 아래의 이미지에서 확인할 수 있듯, 100개의 문제를 약 5초만에 풀어낼 수 있었습니다.

<img width="700" alt="result" src="https://user-images.githubusercontent.com/63924704/135809401-0583cc37-99dc-4626-8f6c-2a3436df16ae.png">

---

### 파일 설명
1. utils.py  
이미지 및 이미지 속에서 추출한 문자를 처리하는 함수들이 포함되어있습니다. 


2. make_train_data.py  
이미지를 추출하여 train data를 직접 만들어내는 함수가 포함되어있습니다.

3. knn_trainer.py  
knn모델을 적용하기 위해 데이터를 전처리하는 함수가 포함되어있습니다. 전처리된 데이터는 trained.npz에 저장했습니다.

4. run.py  
knn모델 학습, 새로운 데이터에 적용하여 수식을 풀어내는 함수, 도출된 답을 사이트에 자동으로 제출하게 하는 자동화 함수가 포함되어있습니다. 마지막 단계에서 실행하는 파일입니다.

---

### 실행 방법

1. 프로젝트를 받아옵니다.  
~~~
git clone https://github.com/sseunghyuns/captcha-project.git
~~~


2. `captcha-project/captcha/src` 폴더로 이동한 후, 아래의 코드를 실행하여 테스트 서버를 킵니다.  

~~~
python3 run.py
~~~


3. `captcha-project/captcha` 폴더로 이동하여 아래의 코드를 실행합니다.  

~~~
python3 run.py
~~~


---

### 참고  
나동빈 - [Python 데이터 분석과 이미지 처리](https://www.youtube.com/watch?v=V8Lpf3WCZ4g&list=PLRx0vPvlEmdBx9X5xSgcEk4CEbzEiws8C)
