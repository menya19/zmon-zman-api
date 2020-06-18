# zmon-zman-api
zmon-zman-api

# 1.인증
모든 API 호출시 헤더에 전달 받은 인증 Token및 Content-type을 다음과 같이 입력해야 한다.
```
Authorization: Bearer <Token>
Content-Type: application/json
```
# 2.API 설명
## 2.1 ORG
### 2.1.1 ORG 등록
```
POST /api/v1/tenant
```
- 입력 데이터 (Body) 
```
{ 
  orgId :  ORG 식별자 문자열
  name :  ORG 이름
  description :  ORG에 대한 설명
}
```
- 응답 : 성공시 `200` 리턴
### 2.1.2 ORG 수정
```
POST /api/v1/tenant/{orgId}
```
등록된 ORG의  `ORG 이름`과 `ORG에 대한 설명`을 수정한다.
- 입력 데이터 (Path)
>- OrgId : ORG 식별자 문자열
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  ORG 이름
  description :  ORG에 대한 설명
}
```
- 응답 : 성공시 `200` 리턴
## 2.2 Account
### 2.2.1 AWS Account
#### 2.2.1.1 AWS Account 등록
```
POST /api/v1/account/aws
```
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  AWS Account 이름
  accessKey : accessKey
  secretKey : secretKey
}
```
- 응답 : 성공시 `200`. 등록 실패시 오류 내용 리턴.
#### 2.2.1.2 AWS Account 수정
```
/api/v1/account/aws/{orgId}/{name}
```
기 등록된 AWS Account의 accessKey, secretKey를 변경한다.
- 입력 데이터 (Path)
>- orgId : ORG 식별자 문자열
>- name : AWS Account 이름
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  AWS Account 이름
  accessKey : accessKey
  secretKey : secretKey
}
- 응답 : 성공시 `200`. 등록 실패시 오류 내용 리턴.
```
### 2.2.2 Azure Account
#### 2.2.2.1 Azure Account 등록
```
POST /api/v1/account/azure
```
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  Azure Account 이름
  tenantId : Tenant ID
  appId : App ID
  secretKey : App SecretKey
}
```
- 응답 : 성공시 `200`. 실패시 오류 내용 리턴.
#### 2.2.2.2 Azure Account 수정
```
/api/v1/account/azure/{orgId}/{name}
```
기 등록된 Azure Account의 tenantId, appId, secretKey를 변경한다.
- 입력 데이터 (Path)
>- orgId : ORG 식별자 문자열
>- name : Azure Account 이름
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  Azure Account 이름
  tenantId : Tenant ID
  appId : App ID
  secretKey : App SecretKey
}
```
- 응답 : 성공시 `200`. 실패시 오류 내용 리턴.
### 2.2.3 Account 삭제
```
POST /api/v1/account/{orgId}/{name}/delete
```
- 입력 데이터 (Path)
>- orgId : ORG 식별자 문자열
>- name : Account 이름 
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  Azure Account 이름
  type : Account 유형 ( 'AWS' | 'AZURE' )
}
```
- 응답 : 성공시 `200`. 실패시 오류 내용 리턴.
## 2.3 리소스 추가 알림
### 2.3.1 AWS 리소스 추가 알림
```
POST /api/v1/resource/aws/{orgId}/{name}
```
- 입력 데이터 (Path)
>- orgId : ORG 식별자 문자열
>- name : AWS Account 이름 
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  Azure Account 이름
  region :  region (ex: ap-northeast-2)
  service :  service (ex: AWS/S3)
  metrics : 수집할 메트릭, 복수일 경우 ','로 분리 (ex: cpu,mem)
}
```
- 응답 : 성공시 `200`. 실패시 오류 내용 리턴.
### 2.3.2 Azure 리소스 추가 알림
```
POST /api/v1/resource/azure/{orgId}/{name}
```
- 입력 데이터 (Path)
>- orgId : ORG 식별자 문자열
>- name : AWS Account 이름 
- 입력 데이터 (Body)
```
{ 
  orgId :  ORG 식별자 문자열
  name :  Azure Account 이름
  subscriptionId : 구독 ID
  resourceType :  리소스 유형 ( ex: Microsoft.Compute/virtualMachines )
  resourceId :  리소스 ID
  metrics : 수집할 메트릭, 복수일 경우 ','로 분리 (ex: cpu,mem)
}
```
- 응답 : 성공시 `200`. 실패시 오류 내용 리턴.
