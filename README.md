Title: 코로나 확진자 수 예측과 그에 따른 물가 동향
https://youtu.be/05xhT1yyr9U

Members: 안준민,원자력공학과 2021086235, redpetj@gmail.com


I. 개요
- Motivation: 코로나 시대에 들어서 과거에 비해 주목받고,
 열광하고 있는 분야가 주식 투자 분야인 것 같다는 생각이 들고 있다.
왜 모두가 주식 투자에 눈이 가게 되었는지를 생각해 보게 되었는데,
 코로나의 영향이 커질 때의 소비자의 지출 및 소비 경향이 물가에 영향을 끼치기도하고
정부의 정책이 물가에 영향을 주기도 해서 이러한 특수한 경우라서
많은 사람들이 주식에 대해 과거와 다른 관점을 가지고 접근하게 되었다고 생각했다.
따라서 코로나의 확산 정도에 따라 물가가 어떻게 변하는지 살펴보고 싶었는데.
정부의 정책을 데이터셋으로 만들어서 물가의 동향을 예측하기는 쉽지 않다고 생각하여
 물가에 영향을 끼치는 요인 중 일부인 코로나 확진자 수를 통해 물가의 동향을 예측하고자 한다.



II. 데이터셋
- 일별 확진자 수
- 월별 확진자 수
- 물가 동향
- 가계 지출 및 소비 동향
- https://kosis.kr/covid/covid_index.do
- https://www.kiri.or.kr/report/downloadFile.do?docId=81889				
- https://www.google.com/search?q=%EC%BD%94%EB%A1%9C%EB%82%98+%EC%9D%BC%EC%9D%BC+%ED%99%95%EC%A7%84%EC%9E%90&rlz=1C1SQJL_enKR890KR890&sxsrf=AOaemvLeG04u5kj9F1YRQ8HCM6D0L1ccAg%3A1639760519962&ei=h8K8YcucOoiOhwPSvISYCw&ved=0ahUKEwiL_Lv6p-v0AhUIx2EKHVIeAbMQ4dUDCA4&uact=5&oq=%EC%BD%94%EB%A1%9C%EB%82%98+%EC%9D%BC%EC%9D%BC+%ED%99%95%EC%A7%84%EC%9E%90&gs_lcp=Cgdnd3Mtd2l6EAMyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEOggIABCABBCwAzoJCAAQsAMQBxAeOgQIIxAnOgQIABAeOgYIABAFEB46BwgjEOoCECc6CwgAEIAEELEDEIMBOgoIABCxAxCDARBDOgQIABBDSgQIQRgBSgQIRhgAUOYTWNgvYIwwaAZwAHgEgAGDAYgBrRaSAQQwLjI2mAEAoAEBsAEKyAECwAEB&sclient=gws-wiz


III. 방법
- 한 달 중에서 최대 일일 확진자 수를 통해 월별 확진자 수를 예측한다
월별 확진자 수와 가계 지출 및 소비 동향과 물가 동향을 비교 분석하여
일별 확진자 수가 갱신될 때 그 달의 물가 동향을 바로 예측하는 방식


일일 확진자 수 데이터를 이용하여 그 달의 평균, 최대값을 구한 뒤에 그 달의 총 확진자 수와 함께 데이터 프레임을 만든다.
![스크린샷(67)](https://user-images.githubusercontent.com/95401684/146572962-95e7b53e-a4cd-4267-9531-47ddcd6ec17b.png)



월별 확진자 데이터로는 물가의 동향을 알 수 있는 데이터들과 묶어 데이터 프레임을 만든다.
![스크린샷(68)](https://user-images.githubusercontent.com/95401684/146573202-02e1a4ec-badd-45a4-b4e2-31e7c2923c7a.png)


이 데이터 셋들을 KTAIDU 프로그램에 넣어 학습 시킨 뒤에 결과를 확인한다.


![스크린샷(74)](https://user-images.githubusercontent.com/95401684/146578608-35658ed7-226a-41cb-b53b-eab39b8fd62f.png)
한달동안의 일일 확진자 수의 최대값과 평균을 입력으로 하고, 월 확진자 수를 출력으로 선택하여 최대값과 평균으로 부터 월 확진자 수를 학습시킨다.


![스크린샷(75)](https://user-images.githubusercontent.com/95401684/146578774-76e3fba4-5a79-48a7-8223-74264678945f.png)
그에 따라 학습이 완료된 모델로 예측을 시켜보면

![스크린샷(76)](https://user-images.githubusercontent.com/95401684/146578885-5a0681a2-e138-4d9b-bd40-06fff65839e1.png)
위에서 봤던 실제 월 확진자 수와 유사하게 나타나는 것을 볼 수 있다.

그 다음엔 월 확진자 수를 입력으로, 나머지 물가 동향 수치들을 출력으로 두어 학습을 시킨다.
![스크린샷(77)](https://user-images.githubusercontent.com/95401684/146578974-9878726e-3fb7-49c4-a63a-642e4143246d.png)


![스크린샷(78)](https://user-images.githubusercontent.com/95401684/146579080-ab9f3bea-4216-4a86-a7b4-52a334770914.png)
학습시킨 후에 예측을 해봤는데, 실제 값과 많이 차이가 나는 것 같아 epoch를 더 늘려 한번 더 학습을 시켜보았다.



![스크린샷(80)](https://user-images.githubusercontent.com/95401684/146579616-c5f6d46b-7556-4ba1-b66d-0fc10a7b4637.png)
이제 실제 데이터 값과 유사하게 나타나게 되었는데, 단순히 epoch값만 늘려서 이렇게 크게 바뀐 것으로 보아 학습이 더 잘되었다기 보다는 이 모델에만 최적화되게 학습이 되었다는 생각이 든다.

IV. 그래프

![image](https://user-images.githubusercontent.com/95401684/146540867-6886c6a6-5415-4e68-bb97-3a9588cf1018.png)
월별 확진자 


![스크린샷(69)](https://user-images.githubusercontent.com/95401684/146573575-5c8111c3-09c3-4925-98fa-6bac55c5ecca.png)
월별 물가 동향



V. 결과
일일 확진자들의 데이터 값을 통해 월 확진자 수를 예측하는 것까지는 학습도 잘되고 예측도 잘 된 것 같지만, 확진자 수 만으로 물가의 동향을 모두 예측하는 것은 조금 어렵다는 생각이 들었다. 초기에 주제를 잡을 때에는 그래프로 보이는 것을 보고 확진자 수만으로도 예측을 할 수 있을 것이라고 생각했지만, 정부의 정책과 같은 다른 요인에 의해 변동되는 부분이 있어 확진자 수를 예측할 수 있다고 해서 물가의 동향까지 정확하게 예측하는 것은 어려운 것 같다. 원래는 외부 프로그램의 도움 없이 학습을 시키려고 했는데, 잘 되지 않아 이를 사용하게 되었다.
