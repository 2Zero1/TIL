# Digital Transmission
데이터에 대한 신호들은 디지털와 아날로그 방식으로 나타낼 수 있다.
``` Digital to Digital Conversion``` 과 ```Analog to Digital Conversion```이 존재한다.

내용에 들어가기에 앞서 Signal element와 Data element에 대해서 알아보자.  
1. Data elements
    - 정보의 한 부분을 나타낼 수 있는 가장 작은 단위로 **bit**에 해당한다.
2. Signal elements
    - data elements를 옮기는 digital signal의 가장 짧은 unit(timewise)
    - 위의 설명을 보면 Signal elements 는 data elements를 옮기는 역할을 한다.
    - r : 각 signal elements에 옮겨지는 data elements의 개수의 비율 ***신호당 비트***
## Digital to Digital Conversion
먼저 디지털 데이터를 어떻게 디지털 신호로 사용하는지 살펴보자.  
**line coding**, block coding, scrambling 이란 3가지 방식이 존재한다.
세가지 방식중에 line coding을 가장 많이 사용한다.

- 1. line coding
    - digital data를 digital signals로 변환하는 프로세스이다.  
    - 우리가 사용하는 text, image,video는 컴퓨터에 연속된 bits들로 구성되어져 있는데, line coding은 이 bits들을 digital signal로 변환해 주는 역할을 한다.
     ![img1](./image/transmissionmedia/img1.png)
    - 위의 그림은 한 signal elements와 data elements를 나타내는 그림이다.
    - 각각 r에 대한 값을 구해보자.

    - 다음은 Data rate와 Signal rate에 대해서 알아볼 것이다.
        - Data rate(bit rate)
            - 1초 동안 보내지는 data elements의 수
            - bps로 표기한다.
        - Signal rate(pulse rate, modulation rate, baudrate)
            - 1동안 보내지는 signal elements의 수
            - baud로 표기
        - data communication의 목표는 data rate를 향상시키고, signal rate를 감소 시키는 것이다.
        - ```S = N/r ```
            - S : signal rate(baud)
            - data rate(bps)
            - r : 각 signal elements로 전송되는 data elements 수의 비율
        - ```S(average) = c * N * (1/r) = c *(N/r)```
            - 외우진 말고 알아두자.
            - S(average) : average value of baud rate
            - c : case factor
            - N : data rate(bps)
            - r : signal elements로 전송되는 data elements 수의 비율
            - 예제
                - ![img2](./image/transmissionmedia/img2.png)

        - 이전에는 bandwidth를 먼저 정했었지만, 밑의 식을 이용하여, 최소로 또는 최대호 필요한 bandwidth를 구할 수 있게 됬다. 
        - Minmum bandwidth : B(min) =c*N*(1/r)
        - Maximum bandwidth : N(max) =(1/c)*B*r
        - B : bandwidth of the channel

    - baseline Wandering
        - baseline : 수신된 신호 파워의 평균
        - 연속된 0이나 1의 비트값을 가진 데이터에 의해 기준선이 움직이는 현상으로, 전압이 오르락 내리락한다.

    - DC Components
        ![img3](./image/transmissionmedia/img3.png)
        - 전류에는 교류와 직류가 있다. Direct Current로 DC라고 한다. 디지털 신호로 논리적으로 1과 0으로 잡힌다.
        - 긴 케이블 통신을 할때 두개의 값의 평균은 양의 값을 갖는다. 이렇게 평균 값이 양의 값을 가지는 것을 직류 성분이 있다. DC Component가 있다 한다.

    - Self-Synchronization
        ![img4](./image/transmissionmedia/img4.png)
        - 받은 신호를 정확하게 해독하기 위해선 리시버의 비트 간격 sender의 bit 간격과 정확하게 일치해야한다.
        - 하지만 간격이 맞지 않을때가 있다. 그래서 self-synchronization은 시간 정보를 데이터에 포함하는 방법이다.

## Line coding schemes
line coding scheme는 5개의 broad categories로 나뉜다.
![img5](./image/transmissionmedia/img5.png)
- 위에서 언급했던 문제들 때문에 편하게 0과 1만으로는 통신을 할 수 없기 때문에 여러가지 방법으로 line coding을 이용한다.
- Unipolar
    ![img6](./image/transmissionmedia/img6.png)
    - positive voltage : 1, zero voltage : 0
    - 한개의 극성만 갖기 때문에 0이면 전압을 0으로, 1이면 전압을 1로 주는 방법이다.
    - 이를 위해 NRZ 방법을 사용한다.
    - 장점으로는 매우 간단하다.
    - 단점으로는 DC components 문제가 있고, synchronization이 힘들다.
    - 비용이 많이 들기 때문에 사용하지 않는다.
- polar
    ![img7](./image/transmissionmedia/img7.png)
    - 두개의 극성을 모두 사용한다.
    - positive voltage : 1, zero voltage : 0
    - NRZ-L : voltage의 level이 bit의 값을 결정
        - 0과 1이 적절히 섞여 있으면 평균이 0이 나오는 NRZ이다.
    - NRZ-I : voltage의 level에 change와 lack of change의 비트값을 결정.
    - 특정 값이 나타나면 교대로 왔다갔다함. 0이 지속되면 문제가 있지만, 1이 많으면 평균이 0이 나오게끔 설계가 되어서 이게 더 낫다.
    - 위의 두방식 다 baseline wandering을 해결하지 못하고, NRZ-L은 더 심하다.
    - Synchronization 또한 둘다 존재. NRZ-L에서 더 심각하다.
    - 둘다 DC component 문제를 갖는다.

    - RZ(Return to Zero)
        ![img8](./image/transmissionmedia/img8.png)
        - NRZ의 synchronization 문제를 해결한다.
        - +,-,0 총 3단계를 사용한다.
        - 신호가 비트 사이에서 변하는게 아니라, 한 비트 안에서 변한다.
        - 지금 사용안한다.
        - 장단점
            - 1bit를 해독하기 위해 2개의 signal change필요하므로, bandwidth가 더 필요하다.
            - 더 복잡하다
            - DC components 문제가 없다.

    - Manchester and Differential Manchester
        ![img10](./image/transmissionmedia/img10.png)
        - Manchester = RZ(transition at the middle of the bit) +  NRZ-L
            - 0dms high에서 low로 떨어지고, 1은 low 에서 high로 올라간다.
            - 항상 가운데서 transission이 발생한다.
            - 그렇기 때문에 신호 가운대에 줄을 그어야 한다.
        ![im11](./image/transmissionmedia/img11.png)
        - Differential Manchester = RZ(transition at the middle of the bit) + NRZ-I
            - 시작위치에서 transission이 있으면 0, 없으면 1.
    
        - 장단점
                - manchester는 NRZ-L를 극복한것.
                - Differential Manchester은 NRZ-I를 극복한것.
                - base line wandering없음
                - DC components 없음.
    - (Biopolar) AMI and Pseudoternary
        ![img9](./image/transmissionmedia/img9.png)
        - +,-,0 세개의 voltage level를 이용
        - AMI(Alternative Mark Inversion) : 처음 나오는 1은 high로 표시하고, 다음 나오는 1은 low, 이런 방식으로 변하고, 0이 나오면 0으로 표시한다.
        - Pseudoternary : AMI와 거꾸로다. 1이 아닌 0일때 신호를 바꿔주고, 1이면 0으로 둔다.
        - 장단점
            - signal rate은 NRZ와 같다.
            - DC components 문제가 없다.
            - long-distance communication에 사용된다.
                - 하지만 Synchronization 문제가 있지만, scrambling으로 해결한다.

        - B : binary data, n : the length of signal pattern, L : the number of levels in the signaling
        - B : L=2, T : L=3, Q : L=4
        
