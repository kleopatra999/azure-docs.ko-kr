---
title: "Azure CLI 2.0을 사용하여 Linux에서 웹앱 관리 | Microsoft Docs"
description: "Azure CLI를 사용하여 Linux에서 웹앱 관리"
keywords: "azure app service, 웹앱, cli, linux, oss"
services: app-service
documentationCenter: 
authors: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.translationtype: HT
ms.sourcegitcommit: cf381b43b174a104e5709ff7ce27d248a0dfdbea
ms.openlocfilehash: e0c913ef50db3572940928d9f739e26994c96981
ms.contentlocale: ko-kr
ms.lasthandoff: 08/23/2017

---

# <a name="manage-web-app-on-linux-using-azure-cli"></a>Azure CLI를 사용하여 Linux에서 웹앱 관리

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

이 문서의 명령을 사용하면 Azure CLI 2.0을 사용하여 Linux에서 웹앱을 만들고 관리할 수 있습니다.
다음 두 가지 방법으로 새 버전의 CLI를 사용하기 시작할 수 있습니다.

* 컴퓨터에 [Azure CLI 2.0 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell(미리 보기)](../cloud-shell/overview.md) 사용


## <a name="create-a-linux-app-service-plan"></a>Linux App Service 계획 만들기

Linux App Service 계획을 만들려면 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>사용자 지정 Docker 컨테이너 웹앱 만들기

웹앱을 만들고 사용자 지정 Docker 컨테이너를 실행하도록 구성하려면 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Linux 앱에서 기존 웹앱에 대한 사용자 지정 Docker 컨테이너 변경

이전에 만든 앱을 현재 Docker 이미지에서 새 이미지로 변경하려면 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>개인 레지스트리의 Docker 이미지 사용

개인 레지스트리의 이미지를 사용하도록 앱을 구성할 수 있습니다. 레지스트리, 사용자 이름 및 암호에 대한 URL을 제공해야 합니다. 이 작업은 다음 명령을 사용하여 수행할 수 있습니다.

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>사용자 지정 Docker 이미지에 대한 연속 배포 사용

다음 명령을 사용하여 CD 기능을 사용하도록 설정하고 웹후크 URL을 가져올 수 있습니다. 이 URL은 DockerHub 또는 Azure Container Registry 리포지토리를 구성하는 데 사용할 수 있습니다.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>기본 제공된 런타임 프레임워크 중 하나를 사용하여 Linux 앱에서 웹앱 만들기

Linux 앱에서 PHP 5.6 웹앱을 만들려면 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Linux 앱에서 기존 웹앱에 대한 프레임워크 버전 변경

이전에 만든 앱을 현재 프레임워크 버전에서 Node.js 6.11로 변경하려면 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>웹앱에 대한 Git 배포 설정

앱에 대한 Git 배포를 설정하려면 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>다음 단계
* [Linux에서 Azure Web App이란?](app-service-linux-intro.md)
* [Azure CLI 2.0 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell(미리 보기)](../cloud-shell/overview.md)
* [Linux의 Azure Web App에서 웹앱 만들기](app-service-linux-how-to-create-web-app.md)
* [Azure App Service에서 스테이징 환경 설정](./web-sites-staged-publishing.md)
* [Linux에서 Azure 웹앱을 사용한 연속 배포](./app-service-linux-ci-cd.md)

