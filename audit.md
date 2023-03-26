## 공통적인 부분 

### 설명 
수수료 계산 부분에서 totalsupply * 999 / 1000 으로 인해 소수점이 날라가는경우 

### 파급력 
low 
토큰의 값이 클 경우 손실이 커진다. 

### 해결방안

적당히 큰 값으로 다시 곱하고 나눠주거나 하는 방식으로 숫자를 조작하여 정수 비교를 할 수 있도록 한다. 



## DEX/kimhanki

### 설명
swap kimhanki/Dex.sol require 156,
단순 오타로 require(rx>= minimumTokenYamount); 로 removeLiquidity 에서 minimumTokenAmount 를 검증하는 부분에 오류.

### 파급력
low
ry 가 rx 로 잘못기재되어 있긴하나 위 require(rx > = minimumTokenXAmount); 구문이 있어 큰 피해는 없을 것이라 판단됨. 
만약 위에가 설정이 안 되어 있었다면 minimumtokenyamount 를 0으로 하고 minimumkotenxamount 를 최대로하여 교환 비율 붕괴 공격 가능


### 해결방안
오타 수정



## Dex/Kimziwoo

### 설명
Kimziwoo/Dex.sol require 87

### 파급력
imformational 
수수료 계산(0.001) 로 인해 소수점 자리가 제거되면서 outpu_amount와 tokenMinimumoutputAmount 를 파고드는 취약점이 생길 수도 있다. 

### 해결방안
양 변에 1000을 곱하여 정수계산을 수행하도록 하면 개선된다. 


## Dex/kwonjoonwoo


### 설명 
Kwonjoonwoo Dex.sol swap 20

### 파급력
High
swap 함수 require 구문 두줄을 보면 token x 와 y 가 동시에 0일 때의 구분을 두지 않았다. ( || 로 묶여 있음) 
따라서 이는 토큰풀의 비율을 망가뜨릴 수 있는 flash loan 공격의 대상이 될 수 있다. 
