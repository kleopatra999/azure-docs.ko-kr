---
title: "Azure에서 정적 HTML 웹앱 만들기 | Microsoft Docs"
description: "정적 HTML 샘플 앱을 배포하여 Azure App Service에서 웹앱을 실행하는 방법을 알아봅니다."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.translationtype: Human Translation
ms.sourcegitcommit: 4f68f90c3aea337d7b61b43e637bcfda3c98f3ea
ms.openlocfilehash: bfa54a90af057f3c799fd8265b3cd5e053f21e69
ms.contentlocale: ko-kr
ms.lasthandoff: 06/20/2017

---
# <a name="create-a-static-html-web-app-in-azure"></a>Azure에서 정적 HTML 웹앱 만들기

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.  이 빠른 시작에서는 기본적인 HTML+CSS 사이트를 Azure Web Apps에 배포하는 방법을 보여 줍니다. [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)를 사용하여 웹앱을 만들고 Git을 사용하여 웹앱에 샘플 HTML 콘텐츠를 배포합니다.

![샘플 앱의 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Mac, Windows 또는 Linux 컴퓨터를 사용하여 아래 단계를 따르면 됩니다. 필수 구성 요소가 설치된 후 단계를 완료하는 데는 약 5분 정도 걸립니다.

## <a name="prerequisites"></a>필수 조건

이 빠른 시작을 완료하려면 다음이 필요합니다.

- [Git 설치](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다. `az --version`을 실행하여 버전을 찾습니다. 설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요. 

## <a name="download-the-sample"></a>샘플 다운로드

터미널 창에서 다음 명령을 실행하여 로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

이 터미널 창을 사용하여 이 빠른 시작의 모든 명령을 실행합니다.

## <a name="view-the-html"></a>HTML 보기

샘플 HTML을 포함하는 디렉터리로 이동합니다. 브라우저에서 *index.html* 파일을 엽니다.

![샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![빈 웹앱 페이지](media/app-service-web-get-started-html/app-service-web-service-created.png)

Azure에서 비어 있는 새 웹앱을 만들었습니다.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a>앱으로 이동

브라우저에서 Azure 웹앱 URL로 이동합니다.

```
http://<app_name>.azurewebsites.net
```

이 페이지는 Azure App Service 웹앱으로 실행됩니다.

![샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**축하합니다.** App Service에 첫 번째 HTML 앱을 배포했습니다.

## <a name="update-and-redeploy-the-app"></a>앱 업데이트 및 다시 배포

텍스트 편집기에서 *index.html* 파일을 열고 태그를 변경합니다. 예를 들어 "Azure App Service - 샘플 정적 HTML 사이트"에서 H1 제목을 "Azure App Service'로 변경합니다.

Git에서 변경 내용을 커밋한 다음 Azure에 코드 변경 내용을 푸시합니다.

```bash
git commit -am "updated HTML"
git push azure master
```

배포가 완료되면 브라우저를 새로 고쳐 변경 내용을 확인합니다.

![업데이트된 샘플 앱 홈 페이지](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>새로운 Azure 웹앱 관리

만든 웹앱을 관리하려면 <a href="https://portal.azure.com" target="_blank">Azure Portal</a>로 이동합니다.

왼쪽 메뉴에서 **App Services**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.

![Azure 웹앱에 대한 포털 탐색](./media/app-service-web-get-started-html/portal1.png)

웹앱의 개요 페이지가 표시됩니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다. 

![Azure Portal의 App Service 블레이드](./media/app-service-web-get-started-html/portal2.png)

왼쪽 메뉴는 앱 구성을 위한 서로 다른 페이지를 제공합니다. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [사용자 지정 도메인 매핑](app-service-web-tutorial-custom-domain.md)

