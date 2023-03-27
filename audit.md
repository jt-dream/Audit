## 공통적인 부분 

### 설명 
수수료 계산 부분에서 totalsupply * 999 / 1000 으로 (totalsupply<1000)인 결과가 0이 되는 경우 

### 파급력 : Low


### 해결방안

적당히 큰 값으로 다시 곱하고 나눠주거나 하는 방식으로 숫자를 조작하여 정수 비교를 할 수 있도록 한다. 

### 설명 
유동성 풀 내 유동성 비율에 대한 검증이 없다. 

### 파급력 : Medium
풀의 비율을 무너뜨려 토큰 가격을 악의적으로 조절할 수 있음. 


### 해결방안

토큰의 비율을 확인하는 조건문 추가해야한다. 




## DEX/kimhanki

### 설명
kimhanki/Dex.sol require 156,
단순 오타로 require(rx>= minimumTokenYamount); 로 removeLiquidity 에서 minimumTokenAmount 를 검증하는 부분에 오류.

### 파급력 : Low
ry 가 rx 로 잘못기재되어 있긴하나 위 require(rx > = minimumTokenXAmount); 구문이 있어 큰 피해는 없을 것이라 판단됨. 
만약 위에가 설정이 안 되어 있었다면 minimumtokenyamount 를 0으로 하고 minimumkotenxamount 를 최대로하여 교환 비율 붕괴 공격 가능


### 해결방안
오타 수정

### 설명
kimhanki/Dex.sol removeliquidity 138
removeliquidity 에서 x,y 토큰을 되돌려 주는 함수가 없다. 

### 파급력 : Critical
유동성을 제공하고나서 x,y 토큰을 다시 되돌려 받을 수 없는 문제점이 있다. 

### 해결방안
x,y 를 다시 되돌려주는 로직을 구현해야한다. 



## Dex/Kimziwoo

### 설명
Kimziwoo/Dex.sol require 87

### 파급력 : informational

수수료 계산(0.001) 로 인해 소수점 자리가 제거되면서 outpu_amount와 tokenMinimumoutputAmount 를 파고드는 취약점이 생길 수도 있다. 

### 해결방안
양 변에 1000을 곱하여 정수계산을 수행하도록 하면 개선된다. 






### -
Lending 은 발표 전까지 추가로 진행할 수 있도록 하겠습니다. 
