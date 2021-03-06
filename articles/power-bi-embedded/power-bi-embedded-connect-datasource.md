<properties
   pageTitle="Microsoft Power BI Embedded - 데이터 원본에 연결"
   description="Power BI Embedded, 데이터 원본에 연결"
   services="power-bi-embedded"
   documentationCenter=""
   authors="minewiskan"
   manager="NA"
   editor=""
   tags=""/>
<tags
   ms.service="power-bi-embedded"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="powerbi"
   ms.date="06/28/2016"
   ms.author="owend"/>

# 데이터 원본에 연결

**Power BI Embedded**를 사용하여 사용자 고유의 앱에 보고서를 포함할 수 있습니다. Power BI 보고서를 앱에 포함하면 데이터의 복사본을 **가져오거나** **DirectQuery**를 통해 데이터 원본에 **직접 연결**하여 기본 데이터에 보고서에 연결됩니다.

**가져오기** 및 **DirectQuery** 사용 간의 차이점은 다음과 같습니다.

|가져오기 | DirectQuery
|---|---
|테이블, 열 *및 데이터*를 보고서의 데이터 집합으로 가져오거나 복사합니다. 기본 데이터에서 발생한 변경 내용을 보려면 현재 데이터 집합을 다시 새로 고치거나 가져오거나 완료해야 합니다.|*테이블 및 열*만 보고서의 데이터 집합으로 가져오거나 복사합니다. 항상 최신 데이터가 표시됩니다.

다음 섹션에서는 **DirectQuery**를 사용할 경우의 이점 및 제한 사항을 설명합니다.

## DirectQuery 사용할 경우의 이점

**DirectQuery**를 사용할 경우 다음 두 가지 주요 이점이 있습니다.

   -	**DirectQuery**를 사용하면 대규모 데이터 집합에서 시각화를 빌드할 수 있습니다. 그렇지 않으면 먼저 모든 데이터를 가져올 수 없습니다.
   -	기본 데이터 변경에는 데이터 새로 고침이 필요할 수 있으며, 일부 보고서의 경우 현재 데이터를 표시하려면 대용량 데이터 전송이 필요할 수 있습니다. 이 경우 데이터를 다시 가져올 수 없습니다. 반면, **DirectQuery** 보고서는 항상 현재 데이터를 사용합니다.

## DirectQuery의 제한 사항

   **DirectQuery** 사용에 대한 몇 가지 제한 사항이 있습니다.

   -	모든 테이블을 단일 데이터베이스에서 가져와야 합니다.
   -	쿼리가 지나치게 복잡한 경우 오류가 발생합니다. 이 오류를 해결하려면 복잡하지 않도록 쿼리를 리팩터링해야 합니다. 쿼리가 복잡한 경우 **DirectQuery**를 사용하는 대신 데이터를 가져와야 합니다.
   -	관계 필터링은 양방향이 아니라 단방향으로 제한됩니다.
   -	열의 데이터 형식을 변경할 수 없습니다.
   -	기본적으로 제한은 측정값에 허용되는 DAX 식에 적용됩니다. [DirectQuery 및 측정값](#measures)을 참조하세요.

<a name="measures"/>
## DirectQuery 및 측정값

기본 데이터 원본으로 전송되는 쿼리가 허용되는 성능을 유지하도록 하기 위해 측정값에 대한 제한 사항이 적용됩니다. **Power BI Desktop**을 사용할 때 고급 사용자는 **파일 > 옵션 및 설정 > 옵션**을 선택하여 이 제한 사항을 무시하도록 선택할 수 있습니다. **옵션** 대화 상자에서 **DirectQuery**를 선택한 다음 **DirectQuery 모드에서 무제한 측정값 허용** 옵션을 선택합니다. 이 옵션을 선택하면 측정값에 유효한 모든 DAX 식을 사용할 수 있습니다. 그러나 데이터를 가져올 때 성능이 뛰어난 일부 식이 **DirectQuery** 모드에서는 백 엔드 원본에 대한 쿼리 속도가 매우 느려질 수 있습니다. **Power BI Desktop**을 사용하는 방법에 대해 알아보려면 [Power BI Desktop 시작](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)을 참조하세요.

## 참고 항목
- [Microsoft Power BI Embedded 미리 보기 시작](power-bi-embedded-get-started.md)
- [Power BI 데스크톱](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)
- [Power BI Desktop 시작](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)

<!---HONumber=AcomDC_0629_2016-->