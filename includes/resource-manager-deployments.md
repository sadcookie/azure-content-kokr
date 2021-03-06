템플릿은 로컬 파일이거나 URI를 통해 사용 가능한 외부 파일일 수 있습니다. 템플릿이 저장소 계정에 상주하는 경우, 템플릿에 대한 액세스를 제한하고 배포 중에 공유 액세스 서명(SAS) 토큰을 제공할 수 있습니다.

## 증분 및 전체 배포

기본적으로 리소스 관리자는 리소스 그룹에 대한 증분 업데이트로 배포를 처리합니다. 증분 배포를 통해 리소스 관리자는 다음을 수행합니다.

- 리소스 그룹에 존재하지만 템플릿에 지정되지 않는 리소스를 **변경되지 않은 상태로 유지**
- 템플릿에 지정되어 있지만 리소스 그룹에 없는 리소스를 **추가** 
- 템플릿에 정의된 동일한 조건으로 리소스 그룹에 존재하는 리소스를 **다시 프로비전하지 않음**

전체 배포를 통해 리소스 관리자는 다음을 수행합니다.

- 리소스 그룹에 존재하지만 템플릿에 지정되지 않는 리소스를 **삭제**
- 템플릿에 지정되어 있지만 리소스 그룹에 없는 리소스를 **추가** 
- 템플릿에 정의된 동일한 조건으로 리소스 그룹에 존재하는 리소스를 **다시 프로비전하지 않음**
 
**Mode** 속성을 통해 배포 유형을 지정합니다.

<!---HONumber=AcomDC_0615_2016-->