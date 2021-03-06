# <a name="platform-supported-migration-of-iaas-resources-from-classic-to-azure-resource-manager"></a>클래식에서 Azure Resource Manager로 IaaS 리소스의 플랫폼 지원 마이그레이션
이 문서에서는 Microsoft가 어떻게 클래식에서 Resource Manager 배포 모델로 IaaS(Infrastructure as a Service) 리소스를 마이그레이션할 수 있도록 지원하는지 설명합니다. [Azure Resource Manager 기능 및 이점](../articles/azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아볼 수 있습니다. 가상 네트워크 사이트-사이트 게이트웨이를 사용하여 구독에서 공존하는 두 가지 배포 모델의 리소스를 연결하는 방법에 대해서도 설명합니다.

## <a name="goal-for-migration"></a>마이그레이션 목표
Resource Manager는 템플릿을 사용하여 복잡한 응용 프로그램을 배포할 수 있도록 지원하며 VM 확장을 사용하여 가상 컴퓨터를 구성하고 액세스 관리와 태깅을 통합합니다. Azure Resource Manager는 가용성 집합에 가상 컴퓨터에 대해 확장성 있는 병렬 배포를 포함합니다. 그뿐 아니라 새로운 배포 모델에서는 계산, 네트워크, 저장소의 수명 주기를 독립적으로 관리할 수 있습니다. 마지막으로 가상 네트워크에 가상 컴퓨터를 적용하여 보안 구현을 기본적으로 중요시합니다.

클래식 배포 모델의 거의 모든 기능이 Azure Resource Manager의 계산, 네트워크 및 저장소에 대해 지원됩니다. Azure Resource Manager의 새로운 기능을 제대로 활용하려는 경우 클래식 배포 모델에서 기존 배포를 마이그레이션할 수 있습니다.

## <a name="supported-resources-for-migration"></a>마이그레이션에 지원되는 리소스
이들 클래식 IaaS 리소스는 마이그레이션 시 지원됩니다.

* 가상 컴퓨터
* 가용성 집합
* 클라우드 서비스
* 저장소 계정
* 가상 네트워크
* VPN 게이트웨이
* Express 경로 게이트웨이_(가상 네트워크 전용으로 동일한 구독 내)_
* 네트워크 보안 그룹 
* 경로 테이블 
* 예약된 IP 

## <a name="supported-scopes-of-migration"></a>지원되는 마이그레이션 범위
계산, 네트워크 및 저장소 리소스의 마이그레이션을 완료하는 데는 4가지 방법이 있습니다. 다음과 같습니다. 

* 가상 컴퓨터 마이그레이션(가상 네트워크가 아님)
* 가상 컴퓨터 마이그레이션(가상 네트워크에서)
* 저장소 계정 마이그레이션
* 연결되지 않은 리소스(네트워크 보안 그룹, 경로 테이블 및 예약된 IP)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>가상 컴퓨터 마이그레이션(가상 네트워크가 아님)
Resource Manager 배포 모델에서는 기본적으로 응용 프로그램 보안이 적용되어 있습니다. 모든 VM은 Resource Manager 모델의 가상 네트워크에 있어야 합니다. Azure 플랫폼은 마이그레이션의 일부로 VM을 다시 시작합니다(`Stop`, `Deallocate` 및 `Start`). Virtual Machines이 마이그레이션될 가상 네트워크에 대해서는 두 가지 옵션이 있습니다.

* 플랫폼에서 새 가상 네트워크를 만들도록 요청하고 가상 컴퓨터를 새 가상 네트워크로 마이그레이션할 수 있습니다.
* 가상 컴퓨터를 Resource Manager의 기존 가상 네트워크로 마이그레이션할 수 있습니다.

> [!NOTE]
> 이 마이그레이션 범위에서는 마이그레이션 중 특정 시간 동안 관리 평면 작업 및 데이터 평면 작업이 허용되지 않을 수 있습니다.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>가상 컴퓨터 마이그레이션(가상 네트워크에서)
대부분의 VM 구성에서는 클래식과 Resource Manager 배포 모델 간에 메타데이터만 마이그레이션됩니다. 기본 VM은 동일한 네트워크의 동일한 하드웨어에서 동일한 저장소로 실행됩니다. 마이그레이션 중 특정 시간 동안 관리 평면 작업이 허용되지 않을 수 있습니다. 그러나 데이터 평면은 계속 작동합니다. 즉, 마이그레이션 중 VM(클래식) 상에서 실행되는 응용 프로그램에 가동 중지 시간이 발생하지 않습니다.

현재 지원되지 않는 구성은 다음과 같습니다. 향후 이에 대한 지원을 추가할 경우 이 구성의 일부 VM에서 가동 중지 시간(VM 작업 중지, 할당 취소, 다시 시작 진행)이 발생할 수 있습니다.

* 단일 클라우드 서비스에 둘 이상의 가용성 집합이 있습니다.
* 단일 클라우드 서비스에서 하나 이상의 가용성 집합과 가용성 집합에 없는 VM이 있습니다.

> [!NOTE]
> 이 마이그레이션 범위에서는 마이그레이션 중 특정 시간 동안 관리 평면이 허용되지 않을 수 있습니다. 앞서 설명한 특정 구성의 경우 데이터 평면 가동 중지 시간이 발생합니다.
>
>

### <a name="storage-accounts-migration"></a>저장소 계정 마이그레이션
원활한 마이그레이션을 위해 클래식 저장소 계정에 Resource Manager VM을 배포할 수 있습니다. 이 기능을 사용하면 계산 및 네트워크 리소스를 저장소 계정과 상관없이 마이그레이션할 수 있으며 이러한 방식이 바람직합니다. 가상 컴퓨터 및 가상 네트워크에 대해 마이그레이션한 후에는 저장소 계정에 대해 마이그레이션을 수행하여 마이그레이션 프로세스를 완료해야 합니다.

> [!NOTE]
> Resource Manager 배포 모델에는 기본 이미지 및 디스크 개념이 적용되지 않습니다. 저장소 계정이 마이그레이션되면 클래식 이미지와 디스크가 Resource Manager 스택에 표시되지 않지만 백업 VHD는 저장소 계정에 남아 있습니다.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>연결되지 않은 리소스(네트워크 보안 그룹, 경로 테이블 및 예약된 IP)
네트워크 보안 그룹, 모든 Virtual Machines 및 Virtual Networks에 연결되지 않은 경로 테이블 및 예약 IP는 따로 마이그레이션할 수 있습니다.

<br>

## <a name="unsupported-features-and-configurations"></a>지원되지 않는 기능 및 구성
현재는 일부 기능 및 구성 집합을 지원하지 않습니다. 다음 섹션에서는 이와 관련된 권장 지침에 대해 설명합니다.

### <a name="unsupported-features"></a>지원되지 않는 기능
현재 지원되지 않는 기능은 다음과 같습니다. 이러한 설정을 제거하고 VM을 마이그레이션한 다음 Resource Manager 배포 모델에서 설정을 다시 사용하도록 지정할 수 있습니다(선택 사항).

| 리소스 공급자 | 기능 | 권장 사항 |
| --- | --- | --- |
| Compute |연결되지 않은 가상 컴퓨터 디스크 | 이들 디스크 뒤에 있는 VHD Blob은 저장소 계정을 마이그레이션할 때 마이그레이션됩니다. |
| Compute |가상 컴퓨터 이미지 | 이들 디스크 뒤에 있는 VHD Blob은 저장소 계정을 마이그레이션할 때 마이그레이션됩니다. |
| 네트워크 |끝점 ACL. | 끝점 ACL을 제거하고 마이그레이션을 다시 시도합니다. |
| 네트워크 |ExpressRoute 게이트웨이와 VPN Gateway가 모두 있는 가상 네트워크  | 마이그레이션을 시작하기 전에 VPN Gateway를 제거한 후 마이그레이션이 완료되면 VPN Gateway를 다시 만듭니다. [ExpressRoute 마이그레이션](../articles/expressroute/expressroute-migration-classic-resource-manager.md)에 대해 자세히 알아봅니다.|
| 네트워크 |권한 부여 링크를 사용하는 ExpressRoute  | 마이그레이션을 시작하기 전에 가상 네트워크 연결에 대한 ExpressRoute 회로를 제거한 다음 마이그레이션이 완료되면 연결을 다시 만듭니다. [ExpressRoute 마이그레이션](../articles/expressroute/expressroute-migration-classic-resource-manager.md)에 대해 자세히 알아봅니다. |
| 네트워크 |응용 프로그램 게이트웨이 | 마이그레이션을 시작하기 전에 Application Gateway를 제거한 후 마이그레이션이 완료되면 Application Gateway를 다시 만듭니다. |
| 네트워크 |VNet 피어링을 사용하는 가상 네트워크 | Virtual Network를 리소스 관리자로 마이그레이션한 다음 피어를 마이그레이션합니다. [VNet 피어링](../articles/virtual-network/virtual-network-peering-overview.md)에 대해 자세히 알아보세요. | 

### <a name="unsupported-configurations"></a>지원되지 않는 구성
현재 지원되지 않는 구성은 다음과 같습니다.

| 부여 | 구성 | 권장 사항 |
| --- | --- | --- |
| 리소스 관리자 |클래식 리소스에 대한 RBAC(역할 기반 액세스 제어) |마이그레이션 후 리소스의 URI가 수정되므로 마이그레이션 후에 수행되어야 하는 RBAC 정책 업데이트를 계획하는 것이 좋습니다. |
| 계산 |VM과 연결된 여러 서브넷 |서브넷만 참조하도록 서브넷 구성을 업데이트합니다. |
| 계산 |가상 네트워크에 속하지만 명시적 서브넷이 할당되지 않은 가상 컴퓨터 |VM을 삭제할 수 있습니다(선택 사항). |
| 계산 |경고, 자동 크기 조정 정책이 있는 가상 컴퓨터 |마이그레이션이 진행되고 이러한 설정은 삭제됩니다. 따라서 마이그레이션 전에 환경을 평가하는 것이 좋습니다. 또는 마이그레이션이 완료된 다음 경고 설정을 다시 구성할 수 있습니다. |
| 계산 |XML VM 확장(BGInfo 1.*, Visual Studio 디버거, 웹 배포 및 원격 디버깅) |이 기능은 지원되지 않습니다. 마이그레이션을 계속하려면 가상 컴퓨터에서 이러한 확장을 제거하는 것이 좋습니다. 그러지 않으면 마이그레이션 프로세스 중에 자동으로 삭제됩니다. |
| 계산 |프리미엄 저장소를 사용한 부팅 진단 |마이그레이션을 계속하기 전에 VM에 대한 부팅 진단 기능을 비활성화합니다. 마이그레이션이 완료된 후에 Resource Manager 스택에서 부팅 진단을 재활성화할 수 있습니다. 또한 스크린샷 및 직렬 로그에 대해 사용되는 blob은 그러한 blob에 대해 요금이 부과되지 않도록 삭제해야 합니다. |
| 계산 |웹/작업자 역할이 포함된 클라우드 서비스 |현재는 지원되지 않습니다. |
| 네트워크 |가상 컴퓨터와 웹/작업자 역할이 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure 앱 서비스 |앱 서비스 환경이 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure HDInsight |HDInsight Services가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Microsoft Dynamics Lifecycle Services |Dynamics Lifecycle Services에서 관리하는 가상 컴퓨터가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure AD Domain Services |Azure AD Domain Services가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure RemoteApp |Azure RemoteApp 배포가 포함된 가상 네트워크 |현재는 지원되지 않습니다. |
| Azure API 관리 |Azure API Management 배포가 포함된 가상 네트워크 |현재는 지원되지 않습니다. IaaS VNET을 마이그레이션하려면 가동 중지 시간이 없는 API Management 배포의 VNET을 변경하세요. |
| Compute |온-프레미스 DNS 서버에서 전송 연결 중인 VPN Gateway 또는 ExpressRoute 게이트웨이가 있는 VNET을 포함하는 Azure Security Center 확장 |Azure Security Center는 보안을 모니터링하고 경고를 발생시키기 위한 확장을 가상 컴퓨터에 자동으로 설치합니다. 이러한 확장은 일반적으로 구독에서 Azure Security Center가 사용되도록 설정되면 자동으로 설치됩니다. ExpressRoute 게이트웨이 마이그레이션은 현재 지원되지 않고 전송 연결된 VPN Gateway는 온-프레미스 액세스를 상실합니다. ExpressRoute 게이트웨이를 삭제하거나 전송 연결된 VPN Gateway를 마이그레이션하면 마이그레이션을 커밋하도록 진행하는 경우 VM 저장소 계정에 대한 인터넷 액세스를 상실합니다. 게스트 에이전트 상태 blob을 채울 수 없어서 이 문제가 발생하는 경우에는 마이그레이션이 진행되지 않습니다. 마이그레이션을 계속하기 3시간 전에, 구독에서 Azure Security Center 정책을 사용하지 않도록 설정하는 것이 좋습니다. |

