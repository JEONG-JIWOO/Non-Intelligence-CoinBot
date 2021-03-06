# Non-Intelligence-CoinBot

무지성  / 지성 코인봇 거래 프로젝트 



## A. Why : 이 프로젝트를 왜 하는가?

##### 나도 돈버는 기계를 만들어 보자 

은행이자이상만이라도, 내 자산이 꾸준히 늘어나는 ,
마법의 기계를 만들어 봅시다. 

```
자산투자 관련알고리즘은 오랜 연구가 된 매우 전문적 분야입니다. 
저같은 (투자분야) 비 전문가가 투자 알고리즘을 만들어서 
수익을 보기란 매우 어렵고 오래걸릴겁니다. 

정석적인 방법으로 투자알고리즘을 만든다면.. 말이죠
그러면,  비 정석적인 루트로 시도를 해 봐야겠지요. 
무지성 - 코인봇을 시도해봅시다. 
```


## B. Why,  왜 코인 단타시장인가.

##### 1. 기반지식없이도, 가능성이 있는 시장

뉴비에게도 기회가 있을지도 모르는곳
```
주식의 경우, 이미 수백년간 연구되어왔고, 
수많은 투자 알고리즘회사들이 있는것을 볼때 그에따른 많은 기반 지식없이는 진입이 힘든 시장입니다. 
반면 코인은 생긴지 얼마 안되었을 뿐더러, 
내재 가치조차 의견이 분분한 시장이기때문에 매우 변동성이 크고, 예측이 힘든 시장입니다.  
그래서, 뉴비에게도 기회가 있을지도 모르는곳입니다.
```


##### 2.  인간보다 기계에 유리한시장 

24시간 단타하는 알고리즘 vs 인간?

```
코인시장을 사람이 투자하는것의 problem은 다음과 같습니다. 
1. 24시간 쉬지않는 시장. 
2. 극한의 변동성 
이중 1번은 알고리즘 특성상 바로 극복이 되는문제입니다.  
그러면 2번 변동성이 문제인데. 이를 오히려 역이용해서, 단타로 작은 이득을 여러번 보는 알고리즘을 만든다면, 
어떨까요?
```


## C. What 무엇을 할건가 : 투자 형태 결정

##### 1.  칼같은 손절과 이득선 

손절과 이득선 원칙을 지키는 단타 투자

```
종종 다양한 투자강의에서 제시되는 이야기기도 한데, 
사람이 한다면주관적인 생각이 개입되서 하기 어려운 부분입니다. 
```

##### 2. 게임규칙 


```

1. 1시간 이내 단타를 진행합니다.

2. Long포지션이나  Short 포지션, 혹은 hold로 포지션 진입을 안하는것 셋중 하나를 알고리즘이 선택합니다. 

3. rate 라는 하나의 변수를 두고, 

4. rate% 이득이면 무조건 익절을 

5. rate% 하락이면 무조건 손절을 진행합니다. 

6. 익절한 경우 > 손절한 경우 , 즉 승패가 50%이상일 경우(수수료를 감안하면 좀더 높아야하겠지만)
   이득을 보게 됩니다.

```

##### 3. 알고리즘이 판단할것

현재 차트및 시장상황을 보고 Short, Long , Hold  포지션중 어떤 포지션에 진입할건지 판단합니다.



## D. What : 어떤 알고리즘을 쓸것인가.

##### 1. 무지성 랜덤단타. 

코인 단타 시장은 완전한 랜덤시장으로 

진입한 1시간동안, **가격이 오를가능성 = 가격이 내릴가능성** 이라는 가정에서 시작합니다. 

```bash
1. 상승장 long 포지션 → rate 상승이후 이득실현 : rate*seed 이득 
2. 상승장 short 포지션 → 0.6rate 상승이후 , 손절 :  0.6*rate*seed  손해 
3. 하락장  long 포지션 → 0.6rate 하락이후 , 손절 :  0.6*rate*seed  손해 
4. 하락장  short 포지션→ rate 하락이후 이득실현 : rate*seed  이득
```

만약 P(1) ~= P(2) ~= P(3) ~= P(4)  라면, **기대 수익률은 0.4rate %**가 됩니다.

##### 2. 지성 - 지도학습 

코인 단타 시장이 패턴이 있는 시장 이라는 가능성에서 시작합니다.

즉 다음 1시간동안 코인이 오르고 내릴지 여부가 이전 차트와 관련이 있다는 추정입니다.

```
x_data     : 이전 m분의 시장데이터
y_predict :  포지션 (LSH, 3개 라벨)
y_true : 이후 60분간의 데이터를 통해서 계산한 이득을 보는 포지션 (LSH, 3개 라벨)
```

##### 3. 강화학습 

사실 이런류의 투자는 강화학습으로 접근한 논문이나 케이스가 가장 많지만,. 

강화학습자체가 row데이터로 처음부터하기에는 어려움으로, 이번 프로젝트에서는 배제했습니다.
