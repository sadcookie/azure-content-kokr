<properties
	pageTitle="PowerApps 엔터프라이즈 및 논리 앱에 Twitter 커넥터 추가 | Microsoft Azure"
	description="REST API 매개 변수를 사용하는 Twitter 커넥터 개요"
	services=""
	documentationCenter="" 
	authors="MandiOhlinger"
	manager="erikre"
	editor=""
	tags="connectors"/>

<tags
   ms.service="multiple"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na" 
   ms.date="05/18/2016"
   ms.author="mandia"/>


# Twitter 커넥터 시작
Twitter에 연결하여 트윗 게시, 사용자의 타임라인 가져오기 등의 작업을 수행합니다. Twitter 커넥터는 다음에서 사용할 수 있습니다.

- 논리 앱 
- PowerApps

> [AZURE.SELECTOR]
- [논리 앱](../articles/connectors/connectors-create-api-twitter.md)
- [PowerApps 엔터프라이즈](../articles/power-apps/powerapps-create-api-twitter.md)

&nbsp;

>[AZURE.NOTE] 이 버전의 문서는 논리 앱 2015-08-01-preview 스키마 버전에 적용됩니다.

Twitter를 사용하면 다음과 같은 작업을 수행할 수 있습니다.

- Twitter에서 가져온 데이터를 기반으로 비즈니스 흐름을 빌드합니다. 
- 새로운 트윗이 있을 때 트리거를 사용합니다.
- 트윗 게시, 트윗 검색 등의 작업을 사용합니다. 이러한 작업을 사용하여 응답을 가져오고 출력을 다른 작업에 사용할 수 있도록 설정합니다. 예를 들어 새 트윗이 있으면 이 트윗을 Facebook에 게시할 수 있습니다.
- PowerApps 엔터프라이즈에 Twitter 커넥터를 추가합니다. 이렇게 하면 사용자가 앱 내에서 이 커넥터를 사용할 수 있습니다. 

PowerApps 엔터프라이즈에서 커넥터를 추가하는 방법을 보려면 [PowerApps에서 커넥터 등록](../power-apps/powerapps-register-from-available-apis.md)으로 이동하세요.

논리 앱에 작업을 추가하려면 [논리 앱 만들기](../app-service-logic/app-service-logic-create-a-logic-app.md)를 참조하세요.


## 트리거 및 작업
Twitter에는 다음 트리거 및 작업이 포함됩니다.

트리거 | 동작
--- | ---
<ul><li>새 트윗이 표시될 때</li></ul>| <ul><li>새 트윗 게시</li><li>새 트윗이 표시될 때</li><li>홈 타임라인 가져오기</li><li>사용자 가져오기</li><li>사용자 타임라인 가져오기</li><li>트윗 검색</li><li>팔로워 가져오기</li><li>내 팔로워 가져오기</li><li>팔로잉 가져오기</li><li>내 팔로잉 가져오기</li></ul>

모든 커넥터는 JSON 및 XML 형식의 데이터를 지원합니다.


## Twitter에 대한 연결 만들기

논리 앱에 이 커넥터를 추가할 때 Twitter 계정에 연결할 권한을 논리 앱에 부여해야 합니다.

1. Twitter 계정에 로그인합니다.
2. **권한 부여**를 선택하고 논리 앱에서 Twitter 계정에 연결하고 사용할 수 있도록 허용합니다. 

>[AZURE.INCLUDE [Twitter에 대한 연결을 만드는 단계](../../includes/connectors-create-api-twitter.md)]

>[AZURE.TIP] 다른 논리 앱에서 이와 동일한 Twitter 연결을 사용할 수 있습니다.


## Swagger REST API 참조
적용 버전: 1.0

### 새 트윗 게시 
트윗합니다. ```POST: /posttweet```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|tweetText|string|no|쿼리|없음|게시할 텍스트|
|body| string(binary) |no|body|없음|게시할 미디어|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 새 트윗이 표시될 때 
검색 쿼리와 일치하는 새 트윗이 게시될 때 워크플로를 트리거합니다. ```GET: /onnewtweet```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|searchQuery|string|yes|쿼리|없음|쿼리 텍스트(Twitter에서 지원되는 모든 쿼리 연산자를 사용할 수 있습니다. http://www.twitter.com/search)|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|202|수락됨|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 홈 타임라인 가져오기 
나와 내 팔로워가 게시한 최근 트윗 및 리트윗을 검색합니다. ```GET: /hometimeline```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|maxResults|정수|no|쿼리|20|검색할 최대 트윗 수|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 사용자 가져오기 
지정한 사용자에 대한 세부 정보(예: 사용자 이름, 설명, 팔로워 수 등)를 검색합니다. ```GET: /user```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|userName|string|yes|쿼리|없음|사용자의 Twitter 핸들|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 사용자 타임라인 가져오기 
지정한 사용자가 게시한 최근 트윗 모음을 검색합니다. ```GET: /usertimeline```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|userName|string|yes|쿼리|없음|Twitter 핸들|
|maxResults|정수|no|쿼리|20|검색할 최대 트윗 수|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 트윗 검색 
지정한 쿼리와 일치하는 관련 트윗 모음을 검색합니다. ```GET: /searchtweets```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|searchQuery|string|yes|쿼리|없음|쿼리 텍스트(Twitter에서 지원되는 모든 쿼리 연산자를 사용할 수 있습니다. http://www.twitter.com/search)|
|maxResults|정수|no|쿼리|20|검색할 최대 트윗 수|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 팔로워 가져오기 
지정된 사용자를 팔로잉하는 사용자를 검색합니다. ```GET: /followers```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|userName|string|yes|쿼리|없음|사용자의 Twitter 핸들|
|maxResults|정수|no|쿼리|20|검색할 최대 사용자 수|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 내 팔로워 가져오기 
나를 팔로잉하는 사용자를 검색합니다. ```GET: /myfollowers```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|maxResults|정수|no|쿼리|20|검색할 최대 사용자 수|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 팔로잉 가져오기 
지정된 사용자가 팔로잉하는 사용자를 검색합니다. ```GET: /friends```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|userName|string|yes|쿼리|없음|사용자의 Twitter 핸들|
|maxResults|정수|no|쿼리|20|검색할 최대 사용자 수|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


### 내 팔로잉 가져오기 
내가 팔로잉하는 사용자를 검색합니다. ```GET: /myfriends```

| 이름| 데이터 형식|필수|위치|기본값|설명|
| ---|---|---|---|---|---|
|maxResults|정수|no|쿼리|20|검색할 최대 사용자 수|

#### 응답
|이름|설명|
|---|---|
|200|확인|
|400|잘못된 요청|
|401|권한 없음|
|403|사용할 수 없음|
|404|찾을 수 없음|
|500|내부 서버 오류. 알 수 없는 오류 발생|
|기본값|작업이 실패했습니다.|


## 개체 정의

### TweetModel: 트윗 개체의 표현

| 속성 이름 | 데이터 형식 | 필수 |
|---|---| --- | 
|TweetText|string|yes|
|TweetId|string|no|
|CreatedAt|string|no|
|RetweetCount|정수|yes|
|TweetedBy|string|yes|
|MediaUrls|array|no|

### UserDetailsModel: Twitter 사용자의 세부 정보 표현

|속성 이름 | 데이터 형식 | 필수 |
|---|---|---|
|FullName|string|yes|
|위치|string|yes|
|Id|정수|no|
|사용자 이름|string|yes|
|FollowersCount|정수|no|
|설명|string|yes|
|StatusesCount|정수|no|
|FriendsCount|정수|no|

### TweetResponseModel: 게시된 트윗을 나타내는 모델

| 이름 | 데이터 형식 | 필수 |
|---|---|---|
|TweetId|string|yes|

### TriggerBatchResponse[TweetModel]

|속성 이름 | 데이터 형식 |필수 |
|---|---|---|
|value|array|no|


## 다음 단계

[논리 앱 만들기](../app-service-logic/app-service-logic-create-a-logic-app.md)

[API 목록](apis-list.md)으로 돌아갑니다.

<!--References-->

[6]: ./media/connectors-create-api-twitter/twitter-apps-page.png
[7]: ./media/connectors-create-api-twitter/twitter-app-create.png

<!---HONumber=AcomDC_0525_2016-->