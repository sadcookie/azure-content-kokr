<properties
    pageTitle="Azure 모바일 앱(Xamarin.Android)에 대해 오프라인 동기화 사용"
    description="앱 서비스 모바일 앱을 사용하여 Xamarin 안드로이드 응용 프로그램에서 오프라인 데이터를 캐시 및 동기화하는 방법을 알아봅니다."
    documentationCenter="xamarin"
    authors="wesmc7777"
    manager="dwrede"
    editor=""
    services="app-service\mobile"/>

<tags
    ms.service="app-service-mobile"
    ms.workload="mobile"
    ms.tgt_pltfrm="mobile-xamarin-android"
    ms.devlang="dotnet"
    ms.topic="article"
	ms.date="05/05/2016"
    ms.author="wesmc"/>

# Xamarin.Android 모바일 앱에 대해 오프라인 동기화 사용

[AZURE.INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## 개요

이 자습서에서는 Xamarin.Android용 Azure 모바일 앱의 오프라인 동기화 기능을 소개합니다. 오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱과 데이터 보기, 추가 또는 수정과 같은 상호 작용을 수행할 수 있습니다. 변경 내용은 로컬 데이터베이스에 저장됩니다. 장치가 다시 온라인 상태가 되면 이러한 변경 내용이 원격 서비스와 동기화됩니다.

이 자습서에서는 자습서 [Xamarin Android 앱 만들기]에서 클라이언트 프로젝트를 업데이트하여 Azure 모바일 앱의 오프라인 기능을 지원합니다. 다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 데이터 액세스 확장 패키지를 추가해야 합니다. 서버 확장 패키지에 대한 자세한 내용은 [Azure 모바일 앱용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.

오프라인 동기화 기능에 대한 자세한 내용은 [Azure 모바일 앱에서 오프라인 데이터 동기화] 항목을 참조하세요.

## 클라이언트 동기화 코드 검토

자습서 [Xamarin Android 앱 만들기]를 완료한 경우 다운로드한 Xamarin 클라이언트 프로젝트는 로컬 SQLite 데이터베이스를 사용하여 오프라인 동기화를 지원하는 코드를 포함합니다. 이미 자습서 코드에 포함된 내용에 대한 간략한 개요입니다. 기능의 개념적 개요는 [Azure 모바일 앱에서 오프라인 데이터 동기화]를 참조하세요.

* 모든 테이블 작업을 수행하려면 먼저 로컬 저장소를 초기화해야 합니다. `ToDoActivity.OnCreate()`가 `ToDoActivity.InitLocalStoreAsync()`를 실행하는 경우 로컬 저장소 데이터베이스를 초기화합니다. Azure 모바일 앱 클라이언트 SDK에서 제공하는 `MobileServiceSQLiteStore` 클래스를 사용하여 새 로컬 SQLite 데이터베이스를 만듭니다. 
 
	`DefineTable` 메서드는 제공된 형식(이 경우 `ToDoItem`)의 필드와 일치하는 테이블을 로컬 저장소에 만듭니다. 이 형식은 원격 데이터베이스에 있는 열을 모두 포함하지 않아도 됩니다. 열의 하위 집합 저장은 불가능합니다.

		// ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code to initialize the SQLite store
            string path = Path.Combine(System.Environment
				.GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses the default conflict handler, which fails on conflict
            // To use a different conflict handler, pass a parameter to InitializeAsync. 
			// For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }


* `ToDoActivity`의 `toDoTable` 멤버는 `IMobileServiceTable` 대신 `IMobileServiceSyncTable` 형식입니다. 모든 만들기, 읽기, 업데이트 및 삭제(CRUD) 테이블 작업을 로컬 저장소 데이터베이스로 보냅니다.
 
	클라이언트 연결에 대한 동기화 컨텍스트를 사용하는 `IMobileServiceSyncContext.PushAsync()`를 호출하여 Azure 모바일 앱 백 엔드에 해당 변경 내용을 푸시합니다. 동기화 컨텍스트를 사용하면 모든 테이블의 변경 내용을 추적하고 밀어넣어서 테이블 관계를 보존할 수 있습니다. `PushAsync`를 호출하는 경우 클라이언트 앱을 수정합니다.

	제공되는 코드는 `ToDoActivity.SyncAsync()`를 호출하여 todoitem목록이 새로 고쳐지거나 todoitem이 더해지거나 완료될 때마다 동기화합니다. 따라서 동기화 컨텍스트를 푸시하고 동기화 테이블을 끌어오는 모든 로컬 변경 후에 동기화합니다. 그러나 끌어오기가 컨텍스트에 의해 추적되는 로컬 업데이트를 보류 중인 테이블에 대해 실행되는 경우 끌어오기 작업은 먼저 자동으로 컨텍스트 푸시를 트리거한다는 사실을 알아야 합니다. 이러한 경우(새로 고침, 추가 및 항목 완료) 명시적 `PushAsync` 호출을 생략할 수 있습니다. 중복됩니다.

    제공된 코드에서 원격 `TodoItem` 테이블에 있는 모든 레코드를 쿼리하지만 쿼리 ID 및 쿼리를 `PushAsync`로 전달하여 레코드를 필터링할 수도 있습니다. 자세한 내용은 [Azure 모바일 앱에서 오프라인 데이터 동기화]에서 섹션 *증분 동기화*를 참조하세요.

	<!-- Need updated conflict handling info : `InitializeAsync` uses the default conflict handler, which fails whenever there is a conflict. To provide a custom conflict handler, see the tutorial [Handling conflicts with offline support for Mobile Services].
 	-->


		// ToDoActivity.cs
        private async Task SyncAsync()
        {
			try {
	            await client.SyncContext.PushAsync();
	            await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
			} catch (Java.Net.MalformedURLException) {
				CreateAndShowDialog (new Exception ("There was an error creating the Mobile Service. Verify the URL"), "Error");
			} catch (Exception e) {
				CreateAndShowDialog (e, "Error");
			}
        }


## 클라이언트 앱을 실행합니다.

클라이언트 응용 프로그램을 적어도 한 번 실행하여 로컬 저장소 데이터베이스를 채웁니다. 다음 섹션에서 앱이 오프라인인 동안 오프라인 시나리오를 시뮬레이션하고 로컬 저장소에 있는 데이터를 수정합니다.

## 클라이언트 앱의 동기화 동작 업데이트

이 섹션에서 백엔드에 잘못된 응용 프로그램 URL을 사용하여 오프라인 시나리오를 시뮬레이션하도록 클라이언트 앱을 수정합니다. 데이터 항목을 추가하거나 변경하는 경우 이러한 변경 내용은 로컬 저장소에 보관되지만 연결이 다시 설정될 때까지 백 엔드 데이터 저장소에 동기화되지 않습니다.

1. `ToDoActivity.cs`의 맨 위에서 잘못된 URL을 가리키도록 `applicationURL`의 초기화를 변경합니다.

        const string applicationURL = @"https://your-service.azurewebsites.fail/"; 

	응용 프로그램이 인증 또한 사용하는 경우 로그인에 실패할 수 있습니다. 장치에서 wifi 및 celluar 네트워크를 사용하지 않도록 설정하여 오프라인 동작을 시연하거나 비행기 모드를 사용할 수 있습니다.

2. `ToDoActivity.SyncAsync`를 업데이트하므로 오프라인 상태를 가정하여 `MobileServicePushFailedException`이 발생하고 무시됩니다.

        private async Task SyncAsync()
        {
			try {
	            await client.SyncContext.PushAsync();
	            await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
			} catch (Java.Net.MalformedURLException) {
				CreateAndShowDialog (new Exception ("There was an error creating the Mobile Service. Verify the URL"), "Error");
			} catch (MobileServicePushFailedException)
            {
                // Not reporting this exception. Assuming the app is offline for now
            }
            catch (Exception e) {
				CreateAndShowDialog (e, "Error");
			}
        }


3. 앱을 빌드 및 실행합니다. 이름 확인예외를 보고하는 대화 상자를 받으면 닫습니다. 새 할 일 항목을 추가하면 `MobileServicePushFailedException`이 대화 상자를 표시하지 않고 처리되기 때문에 앱이 연결된 것처럼 동작합니다.

4. 추가한 새 항목은 모바일 백 엔드에 푸시할 수 있을 때까지 로컬 저장소에만 있습니다. 앱을 닫았다가 다시 시작하여 만든 새 항목이 로컬 저장소에 유지되는지 확인합니다.

5. (선택 사항) Azure SQL 데이터베이스 테이블을 보는 Visual Studio를 사용하여 백 엔드 데이터베이스에서 데이터가 변경되지 않았음을 확인합니다.

   	Visual Studio에서 **서버 탐색기**를 엽니다. **Azure**->**SQL 데이터베이스**에 있는 데이터베이스로 이동합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다. 이제 SQL 데이터베이스 테이블 및 콘텐츠를 찾아볼 수 있습니다.

6. (선택 사항) Fiddle 또는 Postman과 같은 REST 도구를 사용하여 모바일 백 엔드를 쿼리하는데에 `https://your-mobile-app-backend-name.azurewebsites.net/tables/TodoItem` 양식의 GET 쿼리를 사용합니다.


## 모바일 백 엔드를 다시 연결하도록 클라이언트 앱 업데이트

이 섹션에서는 앱을 모바일 백 엔드에 다시 연결하여 다시 온라인 상태로 전환되는 앱을 시뮬레이트합니다. 새로 고침 제스처를 수행하면 데이터가 모바일 백 엔드에 동기화됩니다.

1. `ToDoActivity.cs`을(를) 엽니다. 올바른 URL을 가리키도록 `applicationURL`를 수정합니다.

2. 앱을 다시 빌드하고 실행합니다. 앱을 시작한 후에 Azure 모바일 앱 백 엔드와 동기화하려고 합니다. 예외 대화 상자를 만들지 않았는지를 확인합니다.

3. (선택 사항) SQL Server 개체 탐색기 또는 Fiddler와 같은 REST 도구를 사용하여 업데이트된 데이터를 봅니다. Azure 모바일 앱 백 엔드 데이터베이스와 로컬 저장소 간에 데이터는 동기화되었습니다.

    데이터베이스와 로컬 저장소 간에 데이터가 동기화되었으며 오프라인 상황에서 추가한 항목을 포함합니다.

## 추가 리소스

* [Azure 모바일 앱에서 오프라인 데이터 동기화]

* [Cloud Cover: Azure 모바일 서비스에서 오프라인 동기화](참고: 비디오는 모바일 서비스에 있지만 Azure 모바일 앱에서 비슷한 방식으로 오프라인 동기화가 작동합니다.)

<!-- ##Summary

[AZURE.INCLUDE [mobile-services-offline-summary-csharp](../../includes/mobile-services-offline-summary-csharp.md)]

## Next steps

* [Handling conflicts with offline support for Mobile Services]

* [How to use the Xamarin Component client for Azure Mobile Services]
 -->

<!-- Images -->

<!-- URLs. -->
[Xamarin Android 앱 만들기]: ../app-service-mobile-xamarin-android-get-started.md
[Azure 모바일 앱에서 오프라인 데이터 동기화]: ../app-service-mobile-offline-data-sync.md

[How to use the Xamarin Component client for Azure Mobile Services]: ../partner-xamarin-mobile-services-how-to-use-client-library.md

[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio

[Cloud Cover: Azure 모바일 서비스에서 오프라인 동기화]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri

<!---HONumber=AcomDC_0511_2016-->