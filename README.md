# DataMining Team Project 
서울과학기술대학교 산업정보시스템전공 데이터마이닝 팀 프로젝트

### Members
- 이혜린
- 이태경
- 오민석
- 박현길

### Language
Python 

### Project
스니커즈 리셀 시장 판매자들을 위한 투자 상품/전략 추천

### Purpose 
MZ 세대 새로운 재테크로 떠오르고 있는 리셀테크

리셀 시장에 발을 들이고 싶어하는 소비자들을 위한 투자 상품 및 투자 전략 정보 제공

### Data
````
kream_data.csv
````
Kream 사이트 내 상품 정보 크롤링

|Feature Name|Type|Description|
|:---:|:---:|:---|
|상품명|string|상품 이름|
|모델번호|string|모델 번호|
|브랜드|string|브랜드 이름|
|색상|string|해당 상품의 색상|
|거래량|float|해당 상품의 거래량|
|관심 수|float|해당 상품의 관심 수|
|스타일 수|float|해당 상품의 스타일 수|
|발매일|datetime|해당 상품의 발매일|
|발매가|float|해당 상품의 발매가|
|최근 거래가|float|해당 상품의 최근 거래가|
|최고 거래가|float|해당 상품의 최고 거래가|
|최고 거래 체결일|datetime|해당 상품이 최고 거래가로 체결된 날짜|
|최저 거래가|float|해당 상품의 최저 거래가|
|최저 거래 체결일|datetime|해당 상품이 최저 거래가로 체결된 날짜|

### Data Preprocessing

````
Preprocessing.ipynb
````

#### 1. 파생 변수 추가
|Feature Name|Type|Description|
|:---:|:---:|:---|
|발매일부터 현재까지 일|float|해당 상품이 출시된 후부터의 기간|
|수익률|float|(최고 거래가 - 출시 가격) / (출시 가격)|
|가격 변동성|float|(최고 거래가 - 최저 거래가) / (최고 거래가)|

#### 2. 원 핫 인코딩
상위 10가지 브랜드 원 핫 인코딩

#### 3. 야콥슨 변환
한 쪽으로 치우쳐진 데이터들 정규 분포로 변환

#### 4. 이상치 제거
Z-score를 이용한 이상치 제거

#### 5. 스케일링
StandardScaler

### Experiments

````
Var_kmeans.ipynb
````


#### 1. 군집 분석 (Clustering Analysis)
제품별 특성을 파악하기 위한 군집 분석

***수익률/변동성/거래량***
  
#### K-means Clustering
elbow method를 이용하여 최적의 K 값 찾기

"K-Means Inertia"
"Silhouette Score"
"시각화 이미지"


---
###### 이하 변수들로도 클러스터링 진행하기 위해 위의 과정으로 전처리했고 모델링 진행했으나 의미 있는 결과가 나오지 않았다고 판단하여 아래 목록들은 결과에서 제외함 
###### (해당 분석을 위한 전처리(원 핫 인코딩, 야콥슨 변환), 모델링 코드는 존재)

- ###### 수익률/출시 날짜(duration)/콜라보 여부
  
- ###### 수익률/브랜드/관심 수
  
- ###### 수익률/거래량/출시 날짜(duration)
---

#### 2. 군집 해석
|Cluster Name|Description|
|:---:|:---:|
|투자 초수 (군집 0)|낮은 수익률, 낮은 거래량, 안정적 변동성 - 보수적 투자|
|투자 중수 (군집 1)|중간 수익률, 중간 거래량, 다소 높은 변동성 - 일반적 투자|
|투자 고수 (군집 2)|높은 수익률, 높은 거래량, 높은 변동성 - 고위험 투자|
|하이 리스크 하이 리턴 (군집 3)|매우 높은 수익률, 중간 거래량, 높은 변동성 - 고위험, 고수익 투자|
|통장이 궁해 (군집 4)|매우 높은 수익률, 매우 높은 거래량, 높은 변동성 - 매우 고위험, 매우 고수익 투자|

#### 3. 투자 상품 및 전략 추천 

리셀 시장 초기 진입자 추천 리스트
|상품명|발매가|상품 URL|
|:---:|:---:|:---:|
|(W) 나이키 에어포스 1 '07 미드 화이트|139,000원|/products/76895|
|(W) 나이키 에어포스 1 '07 LX 아워포스 1|139,000원|/products/59832|
|나이키 에어 줌 GT 점프 블랙|$150 (약 204,800원)|/products/51688|

군집 1번 추천 리스트
|상품명|발매가|상품 URL|
|:---:|:---:|:---:|
|(W) 나이키 에어포스 1 '07 SE 40주년 조인 포스 세일 말라카이트|139,000원|/products/79366|
|(W) 나이키 덩크 로우 트리플 화이트|129,000원|/products/36465|
|(W) 나이키 덩크 로우 하베스트 문|129,000원|/products/47867|

군집 2번 추천 리스트
|상품명|발매가|상품 URL|
|:---:|:---:|:---:|
|나이키 x 클랏 x 프라그먼트 덩크 로우 블랙 앤 화이트|179,000원|/products/127236|
|나이키 x 루오한 왕 에어포스 1 로우 플라이레더|119,000원|/products/25745|
|나이키 에어포스 1 '07 LV8 화이트 블랙 울프 그레이|12,100円 (약 105,400원)|/products/44282|

군집 3번 추천 리스트
|상품명|발매가|상품 URL|
|:---:|:---:|:---:|
|나이키 줌 보메로 5 벨벳 브라운 미디엄 애쉬|219,000원|/products/192423|
|(W) 나이키 에어맥스 스콜피온 플라이니트 블랙 앤 페르시안 바이올렛|299,000원|/products/77892|
|나이키 에어맥스 97 스타디움 그레이 앤트러사이트|$170 (약 232,100원)|/products/53039|

군집 4번 추천 리스트
|상품명|발매가|상품 URL|
|:---:|:---:|:---:|
|나이키 에어포스 1 '07 LV8 애슬레틱 클럽 러쉬 오렌지 워시드 틸|179,000원|/products/49015|
|(W) 나이키 덩크 로우 디스럽트 2 블랙 화이트|139,000원|/products/68097|
|(W) 나이키 덩크 로우 애트모스피어 핑크|129,000원|/products/57679|
