<properties
	pageTitle="Azure 기계 학습 FAQ | Microsoft Azure"
	description="Azure 기계 학습 소개: 간소화된 예측 모델링에 대한 클라우드 서비스의 요금 청구, 기능 및 제한 사항을 다루는 FAQ."
	keywords="기계 학습 소개, 예측 모델링, 기계 학습이란 무엇인가요"
	services="machine-learning"
	documentationCenter=""
	authors="garyericson"
	manager="paulettm"
	editor="cgronlun"/>

<tags
	ms.service="machine-learning"
	ms.workload="data-services"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="get-started-article"
	ms.date="06/13/2016"
	ms.author="garye"/>

# Azure 기계 학습 질문과 대답(FAQ): 대금 청구, 기능, 제한 사항 및 지원

이 FAQ에서는 Azure 기계 학습, 예측 모델 개발을 위한 클라우드 서비스 및 웹 서비스를 통한 운용성 솔루션에 대한 질문에 답변합니다. 이 FAQ는 요금 청구 모델, 기능, 제한 및 지원을 포함한 서비스 사용에 대한 질문을 다룹니다.

## 일반적인 질문

**Azure 기계 학습이란 무엇인가요?**

Azure 기계 학습은 완벽하게 관리되는 서비스로, 이 서비스를 통해 클라우드에 예측 분석 솔루션을 만들고, 테스트하고, 운영하고, 관리할 수 있습니다. 브라우저만 있으면 로그인하고 데이터를 업로드하고 즉시 기계 학습 실험을 시작할 수 있습니다. 끌어서 놓기 예측 모델링, 모듈의 대형 팔레트 및 시작 템플릿의 라이브러리를 활용하면 일반적인 기계 학습 작업을 간단히, 빠르게 수행할 수 있습니다. 자세한 내용은 [Azure 기계 학습 서비스 개요](https://azure.microsoft.com/services/machine-learning/)를 참조하세요. 주요 용어 및 개념을 다루는 기계 학습 소개는 [Azure 기계 학습 소개](machine-learning-what-is-machine-learning.md)를 참조하세요.


[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**기계 학습 스튜디오란 무엇인가요?**

기계 학습 스튜디오는 웹 브라우저를 통해 액세스하는 워크벤치 환경입니다. 기계 학습 스튜디오는 실험 형태의 전체 데이터 과학 워크플로를 구성할 수 있는 시각적 컴퍼지션 인터페이스와 함께 모듈 팔레트를 호스트합니다.

기계 학습 스튜디오에 대한 자세한 내용은 [기계 학습 스튜디오란 무엇인가요?](machine-learning-what-is-ml-studio.md)를 참조하세요.

**Azure 기계 학습 API 서비스란 무엇인가요?**

기계 학습 API 서비스를 통해 기계 학습 스튜디오에 기본 제공되는 것과 같은 예측 모델을 확장 가능한 내결함성 웹 서비스로 배포할 수 있습니다. 기계 학습 API 서비스를 통해 만든 웹 서비스는, 외부 응용 프로그램과 예측 분석 모델 간의 통신용 인터페이스를 제공하는 REST API입니다.

자세한 내용은 [기계 학습 웹 서비스에 연결](machine-learning-connect-to-azure-machine-learning-web-service.md)을 참조하세요.


## 대금 청구 관련 질문

**기계 학습 결제는 어떤 방식으로 이루어지나요?**

대금 청구 및 가격 정보는 [기계 학습 가격](https://azure.microsoft.com/pricing/details/machine-learning/)을 참조하세요.

**Azure 기계 학습의 무료 평가판이 있나요?**

 Azure 기계 학습에는 무료 구독 옵션이 있고(자세한 내용은 [기계 학습 가격 책정](https://azure.microsoft.com/pricing/details/machine-learning/) 참조), 기계 학습 스튜디오에서는 8시간 빠른 평가 평가판을 사용할 수 있습니다(이 평가판은 [기계 학습 스튜디오](https://studio.azureml.net/?selectAccess=true&o=2)에 로그인).
 
 또한 Azure 무료 평가판에 등록하면 한 달 동안 모든 Azure 서비스를 사용해볼 수 있습니다. Azure 무료 평가판에 대한 자세한 내용을 보려면 [Azure 무료 평가판 FAQ](/pricing/free-trial-faq/)를 방문하세요.

## 기계 학습 스튜디오 질문

### 실험 만들기

**실험 그래프에 대한 버전 제어 또는 Git 통합이 있나요?**

아니오, 하지만 기계 학습 스튜디오에 실험에 대한 각 반복이 유지되며, 이것은 다른 사용자가 수정할 수 없습니다. 자세한 내용은 [기계 학습 스튜디오에서 반복 실험 관리](machine-learning-manage-experiment-iterations.md)를 참조하세요.

### 기계 학습 데이터 가져오기 및 내보내기

**기계 학습에서 지원하는 데이터 원본은 무엇인가요?**

데이터는 로컬 파일을 데이터 집합으로 업로드하거나, 클라우드 데이터 서비스에서 데이터를 가져오는 모듈을 사용하거나, 다른 실험에서 저장된 데이터 집합을 가져오는 세 가지 방법 중 하나를 사용하여 기계 학습 스튜디오 실험에 로드될 수 있습니다. 지원된 파일 형식에 대한 자세한 내용은 [기계 학습 스튜디오로 학습 데이터 가져오기](machine-learning-data-science-import-data.md)를 참조하세요.


#### <a id="ModuleLimit"></a>모듈에 대해 설정할 수 있는 데이터 집합의 크기는 어느 정도인가요?

기계 학습 스튜디오의 모듈은 일반적인 사용 사례의 경우 최대 10GB 숫자 데이터의 데이터 집합을 지원합니다. 모듈에서 둘 이상의 입력을 사용하는 경우에는 모든 입력 크기의 합계가 10GB입니다. Hive 또는 Azure SQL 데이터베이스 쿼리를 사용하거나 Learning by Counts 전처리를 통해 수집하기 전에 더 큰 데이터 집합을 샘플링할 수 있습니다.

다음 데이터 형식은 기능 정규화 중에 확장할 수 있으며 10GB 미만으로 제한됩니다.

- 스파스
- 범주
- 문자열
- 이진 데이터

다음 모듈은 10GB 미만의 데이터 집합으로 제한됩니다.

- Recommender 모듈
- SMOTE 모듈
- Scripting 모듈: R, Python, SQL
- 출력 데이터 크기가 입력 데이터 크기보다 클 수 있는 모듈(예: Join 또는 Feature Hashing)
- Cross-validation, Tune Model Hyperparameters, Ordinal Regression 및 One-vs-All Multiclass(반복 횟수가 매우 많은 경우).

몇 GB보다 큰 데이터 집합의 경우 로컬 파일에서 직접 업로드하지 않고 Azure 저장소 또는 Azure SQL 데이터베이스에 데이터를 업로드하거나 HDInsight를 사용해야 합니다.


####<a id="UploadLimit"></a>데이터 업로드에 대한 제한 사항은 무엇인가요?
몇 GB보다 큰 데이터 집합의 경우 로컬 파일에서 직접 업로드하지 않고 Azure 저장소 또는 Azure SQL 데이터베이스에 데이터를 업로드하거나 HDInsight를 사용합니다.

**Amazon S3에서 데이터를 읽을 수 있나요?**

소량의 데이터를 http URL을 통해 노출하려는 경우 [Import Data][import-data] 모듈을 사용할 수 있습니다. Azure 저장소로 전송할 데이터가 많은 경우에는 먼저 [Import Data][import-data] 모듈을 사용하여 실험으로 가져옵니다.
<!--
<SEE CLOUD DS PROCESS>
-->

**기본 제공 이미지 입력 기능이 있나요?**

이미지 입력 기능은 [이미지 가져오기][image-reader] 참조에서 확인할 수 있습니다.

### 모듈

**원하는 알고리즘, 데이터 원본, 데이터 형식, 데이터 변환 작업이 Azure 기계 학습 스튜디오에 없습니다. 어떻게 해야 하나요?**

[사용자 피드백 포럼](http://go.microsoft.com/fwlink/?LinkId=404231)을 방문하면 Microsoft에서 추적 중인 기능 요청을 확인할 수 있습니다. 원하는 기능이 이미 요청된 경우 해당 요청에 투표할 수 있습니다. 원하는 기능이 없는 경우 새로운 요청을 만드세요. 이 포럼에서 요청의 상태를 확인할 수도 있습니다. Microsoft는 이 목록을 긴밀하게 추적하여 기능의 사용 가능성 상태를 자주 업데이트합니다. R 및 Python에 대한 기본적인 지원 외에 필요에 따라 사용자 지정 변환을 만들 수 있습니다.


**기존 코드를 기계 학습 스튜디오로 가져올 수 있나요?**

예, 기계 학습 스튜디오로 기존 R 또는 Python 코드를 가져와서, Azure 기계 학습 학습자와 동일한 실험에서 실행하고 Azure 기계 학습을 통해 솔루션을 웹 서비스로 배포할 수 있습니다. 자세한 내용은 [R을 사용하여 실험 확장](machine-learning-extend-your-experiment-with-r.md) 및 [Azure 기계 학습 스튜디오에서 Python 기계 학습 스크립트 실행](machine-learning-execute-python-scripts.md)을 참조하세요.

**[PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language)과 유사한 것을 사용하여 모델을 정의할 수 있나요?**

아니요, 이 기능은 지원되지 않습니다. 그러나 사용자 지정 R 및 Python 코드를 사용하여 모듈을 정의할 수 있습니다.

**실험에서 병렬로 실행할 수 있는 모듈은 몇 개인가요?**

실험에서 동시에 최대 4개의 모듈을 실행할 수 있습니다.


### 데이터 처리

**실험 내에서 대화형으로 데이터를 시각화하는 기능(R 시각화 외)이 있나요?**

모듈의 출력을 클릭하면 데이터를 시각화하고 통계를 가져올 수 있습니다.

**브라우저에서 결과 또는 데이터를 미리 볼 때 행 및 열 수가 제한되는 이유는 무엇인가요?**

데이터가 브라우저로 전송되고 클 수 있기 때문에 기계 학습 스튜디오의 성능 저하를 방지하기 위해 데이터 크기가 제한됩니다. 모든 데이터/결과를 시각화하려면, 데이터를 다운로드하고 Excel 또는 다른 도구를 사용하는 것이 좋습니다.

### 알고리즘

**기계 학습 스튜디오에서 지원되는 기존 기계 학습 알고리즘은 무엇인가요?**

기계 학습 스튜디오는 Microsoft Research에서 개발된 확장 가능한 고급 의사 결정 트리, Bayesian 권장 시스템, 심층적인 신경망, 의사 결정 정글 등 최신 기계 학습 알고리즘을 제공합니다. Vowpal Wabbit과 같은 확장 가능한 오픈 소스 기계 학습 패키지도 포함되어 있습니다. 기계 학습 스튜디오는 여러 클래스의 이진 분류, 회귀 및 클러스터링을 위한 기계 학습 알고리즘을 지원합니다. 전체 목록은 [기계 학습 모듈][machine-learning-modules]을 참조하세요.

**데이터에 사용할 올바른 기계 학습 알고리즘이 자동으로 제안되나요?**

아니요. 그러나 기계 학습 스튜디오에서 각 알고리즘의 결과를 비교하여 문제에 적합한 알고리즘을 확인할 수 있는 몇 가지 방법이 있습니다.

**제공된 알고리즘에서 적합한 알고리즘 하나를 선택하는 데 대한 지침이 있나요?** [알고리즘을 선택하는 방법](machine-learning-algorithm-choice.md)을 참조하세요.

**제공되는 알고리즘은 R 또는 Python으로 작성되었나요?**

아니요, 이러한 알고리즘은 더 높은 성능을 제공하기 위해 주로 컴파일된 언어로 작성됩니다.

**제공되는 알고리즘에 대한 세부 정보가 있나요?**

설명서에는 알고리즘에 대한 일부 정보가 나와 있으며, 용도에 맞게 알고리즘을 최적화할 수 있도록 조정을 위해 제공되는 매개 변수에 대한 설명이 있습니다.

**온라인 학습을 지원하나요?**

아니요, 현재는 프로그래밍 방식의 재학습만 지원됩니다.

**기본 제공 모듈을 사용하여 신경망 모델의 계층을 시각화할 수 있나요?**

번호

**C# 또는 일부 다른 언어로 모듈을 만들 수 있나요?**

현재 새 사용자 지정 모듈은 R로만 만들 수 있습니다.

### R 모듈

**기계 학습 스튜디오에서 사용 가능한 R 패키지는 무엇인가요?**

기계 학습 스튜디오는 현재 400개 이상의 CRAN R 패키지를 지원하며 다음은 모든 포함된 패키지의 [현재 목록](http://az754797.vo.msecnd.net/docs/RPackages.xlsx)입니다. 이 목록을 직접 검색하는 방법에 대해 알아보려면 [R을 사용하여 실험 확장](machine-learning-extend-your-experiment-with-r.md)을 참조하세요. 원하는 패키지가 이 목록에 없는 경우 [사용자 피드백 포럼](http://go.microsoft.com/fwlink/?LinkId=404231)에서 패키지 이름을 제공해 주세요.

**사용자 지정 R 모듈을 빌드할 수 있나요?**

예, 자세한 내용은 [Azure 기계 학습에서 사용자 지정 R 모듈 작성](machine-learning-custom-r-modules.md)을 참조하세요.

**R에 대한 REPL 환경이 있나요?**

아니요, R에 대한 REPL 환경은 스튜디오에 없습니다.

### Python 모듈

**사용자 지정 Python 모듈을 빌드할 수 있나요?**

현재는 안되지만, 하나 이상의 [Python 스크립트 실행][python] 모듈을 사용하여 동일한 결과를 낼 수 있습니다.

**Python에 대한 REPL 환경이 있나요?**

기계 학습 스튜디오에서 Jupyter 노트북을 사용할 수 있습니다. 자세한 내용은 [Azure 기계 학습 스튜디오에 Jupyter 노트북 도입](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)을 참조하세요.

## 웹 서비스

###프로그래밍 방식으로 모델 재학습

**Azure 기계 학습 모델 프로그래밍 방식을 다시 학습하려면 어떻게 하나요?**

재학습 API를 사용합니다. 자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요. [Microsoft Azure 기계 학습 재학습 데모](https://azuremlretrain.codeplex.com/)(영문)에 샘플 코드도 제공됩니다.

### 생성

**모델을 로컬로 배포하거나 인터넷에 연결하지 않고 응용 프로그램에서 배포할 수 있나요?**

번호


**모든 웹 서비스에 예상되는 기준 대기 시간이 있나요?**

[Azure 구독 제한](../azure-subscription-service-limits.md)을 참조하세요.

### 사용

**어떤 경우에 내 예측 모델을 일괄 처리 실행 서비스로 실행하고 어떤 경우에 요청-응답 웹 서비스를 실행하나요?**

RRS(요청-응답 서비스)는 대기 시간이 짧고, 확장성이 높은 웹 서비스로, 실험 환경에서 생성하여 배포하는 상태 비저장 모델에 대한 인터페이스를 제공하는 데 사용됩니다. BES(일괄 처리 실행 서비스)는 데이터 레코드의 배치에 대한 점수를 비동기적으로 계산하는 서비스입니다. BES의 입력은 RRS에 사용되는 데이터 입력과 유사합니다. 가장 중요한 차이는 BES에서는 Azure의 Blob 서비스 및 테이블 서비스, Azure SQL 데이터베이스, HDInsight(Hive 쿼리), HTTP 소스 등의 다양한 소스에서 레코드 블록을 읽는다는 점입니다. 자세한 내용은 [기계 학습 웹 서비스 사용 방법](machine-learning-consume-web-services.md)을 참조하세요.

**배포된 웹 서비스의 모델을 업데이트하려면 어떻게 해야 하나요?**

이미 배포된 서비스의 예측 모델을 업데이트하는 작업은 학습된 모델을 빌드하여 저장하는 데 사용된 실험을 수정하고 다시 실행하는 작업만큼 간단합니다. 새 버전의 학습된 모델이 확보되면, 기계 학습 스튜디오에서 웹 서비스를 업데이트할지 여부를 묻습니다. 배포된 웹 서비스를 업데이트하는 방법에 대한 자세한 내용은 [기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

다시 학습 API도 사용할 수 있습니다. 자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요. [Microsoft Azure 기계 학습 재학습 데모](https://azuremlretrain.codeplex.com/)(영문)에 샘플 코드도 제공됩니다.

**프로덕션에 배포된 웹 서비스를 모니터링하려면 어떻게 해야 하나요?**

예측 모델을 배포한 후에는 Azure 클래식 포털에서 모니터링할 수 있습니다. 배포된 각 서비스에는 고유한 대시보드가 있어, 이 대시보드에서 해당 서비스에 대한 모니터링 정보를 볼 수 있습니다. 배포된 웹 서비스를 관리하는 방법에 대한 자세한 내용은 [Azure 기계 학습 작업 영역 관리](machine-learning-manage-workspace.md)를 참조하세요.

**RRS/BES의 출력을 볼 수 있는 곳이 있나요?**

RRS의 경우 웹 서비스 응답은 일반적으로 결과를 보는 위치입니다. Azure Blob 저장소에 기록도 가능합니다. BES의 경우 기본적으로 출력은 Blob에 기록됩니다. [데이터 내보내기][export-data] 모듈을 사용하여 출력을 데이터베이스 또는 테이블에 기록할 수도 있습니다.

**기계 학습 스튜디오에서 만든 모델에서만 웹 서비스를 만들 수 있나요?**

아니요. Jupyter 노트북 및 RStudio에서 직접 웹 서비스를 만들 수도 있습니다.

**오류 코드에 대한 정보를 어디서 찾을 수 있습니까?**

오류 코드 목록 및 설명은 [기계 학습 모듈 오류 코드](https://msdn.microsoft.com/library/azure/dn905910.aspx)를 참조하세요.

## 확장성

**웹 서비스의 확장성이란 무엇인가요?**

현재 기본 끝점은 끝점당 20개의 동시 RRS 요청으로 프로비전됩니다. [API 끝점 크기 조정](machine-learning-scaling-endpoints.md)에 설명된 것처럼 끝점당 동시 요청 수를 200개까지 확장할 수 있으며 웹 서비스당 10,000개 끝점으로 각 웹 서비스를 확장할 수 있습니다. BES의 경우 각 끝점은 한 번에 40개의 요청을 처리할 수 있으며 40개를 초과하는 추가 요청은 큐에 대기됩니다. 이러한 큐에 대기 중인 요청은 큐에서 나옴과 동시에 자동으로 실행됩니다.


**R 작업은 노드 간에 분산되나요?**

번호


**학습에 사용할 수 있는 데이터의 양은 얼마인가요?**

기계 학습 스튜디오의 모듈은 일반적인 사용 사례의 경우 최대 10GB 숫자 데이터의 데이터 집합을 지원합니다. 모듈에서 둘 이상의 입력을 사용하는 경우에는 모든 입력에 대한 총 크기의 합계가 10GB입니다. Hive 또는 Azure SQL 데이터베이스 쿼리를 통하거나 수집 전에 [개수로 알아보기][counts] 모듈로 전처리하여 더 큰 데이터 집합을 샘플링할 수도 있습니다.

다음 데이터 형식은 기능 정규화 중에 확장할 수 있으며 10GB 미만으로 제한됩니다.

- 스파스
- 범주
- 문자열
- 이진 데이터

다음 모듈은 10GB 미만의 데이터 집합으로 제한됩니다.

- Recommender 모듈
- SMOTE 모듈
- Scripting 모듈: R, Python, SQL
- 출력 데이터 크기가 입력 데이터 크기보다 클 수 있는 모듈(예: Join 또는 Feature Hashing)
- Cross-Validate, Tune Model Hyperparameters, Ordinal Regression 및 One-vs-All Multiclass(반복 횟수가 매우 많은 경우)

몇 GB보다 큰 데이터 집합의 경우 로컬 파일에서 직접 업로드하지 않고 Azure 저장소 또는 Azure SQL 데이터베이스에 데이터를 업로드하거나 HDInsight를 사용해야 합니다.


**벡터 크기 제한이 있나요?**

행 및 열은 각각 .NET 제한인 Max Int: 2,147,483,647로 제한됩니다.

**웹 서비스를 실행하기 위해 사용 중인 가상 컴퓨터의 크기를 조정할 수 있나요?**

번호

## 보안 및 사용 가능성

**웹 서비스에 대한 http 끝점에 기본적으로 액세스 권한을 갖는 사람은 누구인가요? 끝점에 대한 액세스는 어떻게 제한하나요?**

웹 서비스가 배포된 후 해당 서비스에 대한 기본 끝점이 만들어집니다. 기본 끝점은 API 키를 사용하여 호출할 수 있습니다. Azure 클래식 포털에서 또는 웹 서비스 관리 API를 사용하여 프로그래밍 방식으로 해당 고유 키로 끝점을 더 추가할 수 있습니다. 액세스 키는 웹 서비스를 호출하는 데 필요합니다. 자세한 내용은 [기계 학습 웹 서비스에 연결](machine-learning-connect-to-azure-machine-learning-web-service.md)을 참조하세요.


**내 Azure 저장소 계정을 찾을 수 없는 경우 어떻게 되나요?**

기계 학습 스튜디오는 워크플로를 실행할 때 사용자가 제공한 Azure 저장소 계정을 기반으로 중간 데이터를 저장합니다. 이 저장소 계정은 작업 영역을 만들 때 기계 학습 스튜디오에 제공됩니다. 작업 영역을 만든 후 저장소 계정이 삭제되고 더 이상 찾을 수 없는 경우에는 해당 작업 영역의 작동이 중지되고 작업 영역의 모든 실험이 실패합니다.

저장소 계정을 실수로 삭제한 경우 이를 복구하는 유일한 방법은 삭제한 저장소 계정과 같은 지역과 같은 이름으로 저장소 계정을 다시 만드는 것 입니다. 그 후 액세스 키를 다시 동기화하세요.


**저장소 계정 액세스 키가 동기화되지 않은 경우 어떻게 되나요?**

기계 학습 스튜디오는 워크플로를 실행할 때 사용자가 제공한 Azure 저장소 계정을 기반으로 중간 데이터를 저장합니다. 이 저장소 계정은 작업 영역을 만들고 해당 작업 영역과 액세스 키를 연결할 때 기계 학습 스튜디오에 제공됩니다. 작업 영역을 만든 후 액세스 키가 변경되고 해당 작업 영역에서 저장소 계정에 더 이상 액세스할 수 없는 경우에는 해당 작업 영역의 작동이 중지되고 작업 영역의 모든 실험이 실패합니다.

저장소 계정 액세스 키를 변경한 경우에는, Azure 클래식 포털을 사용하여 작업 영역에서 액세스 키를 다시 동기화합니다.


## Azure 마켓플레이스

[기계 학습 마켓플레이스에서 앱 게시 및 사용에 대한 FAQ](machine-learning-marketplace-faq.md)를 참조하세요.

## 지원 및 교육

**Azure 기계 학습에 대한 교육은 어디에서 받을 수 있나요?**

[Azure 기계 학습 설명서 센터](https://azure.microsoft.com/services/machine-learning/)에서 비디오 자습서와 방법 가이드를 호스트합니다. 이러한 단계별 가이드에서는 서비스를 소개하고, 데이터 가져오기, 데이터 정리, 예측 모델 구성, Azure 기계 학습에서 프로덕션으로 전환의 데이터 과학 수명 주기 전체를 안내해 줍니다.

Microsoft는 기계 학습 센터에 새로운 자료를 계속 추가할 예정입니다. [사용자 피드백 포럼](https://windowsazure.uservoice.com/forums/257792-machine-learning)에서 기계 학습 센터의 추가 학습 자료에 대한 요청을 제출할 수 있습니다.

[Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning)에서 교육을 찾을 수도 있습니다.

**Azure 기계 학습에 대한 지원을 받으려면 어떻게 해야 하나요?**

Azure 기계 학습에 대한 기술 지원을 받으려면 [Azure 지원](/support/options/)으로 이동하여 **기계 학습**을 선택합니다.

또한 Azure 기계 학습은 MSDN에 커뮤니티 포럼을 갖고 있으며, 여기에서 Azure 기계 학습 관련 질문을 할 수 있습니다. 이 포럼은 Azure 기계 학습 팀에서 모니터링합니다. [Azure 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)을 방문해보세요.


<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx

<!---HONumber=AcomDC_0615_2016-->