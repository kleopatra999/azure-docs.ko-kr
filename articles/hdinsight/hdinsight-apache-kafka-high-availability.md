---
title: "Apache Kafka를 통한 고가용성 - Azure HDInsight | Microsoft Docs"
description: "Azure HDInsight의 Apache Kafka를 사용하여 고가용성을 보장하는 방법을 알아봅니다. HDInsight가 포함된 Azure 지역 내의 여러 장애 도메인에 있도록 Kafka에서 파티션 복제본의 균형을 다시 조정하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.translationtype: Human Translation
ms.sourcegitcommit: 138f04f8e9f0a9a4f71e43e73593b03386e7e5a9
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/29/2017

---
# HDInsight의 Apache Kafka(미리 보기)를 통한 데이터 고가용성
<a id="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight" class="xliff"></a>

기본 하드웨어 랙 구성을 활용하기 위해 Kafka 토픽에 대한 파티션 복제본을 구성하는 방법에 대해 알아봅니다. 이 구성은 HDInsight의 Apache Kafka에 저장된 데이터의 가용성을 보장합니다.

## Kafka를 사용하는 장애 및 업데이트 도메인
<a id="fault-and-update-domains-with-kafka" class="xliff"></a>

장애 도메인은 Azure 데이터 센터에 있는 기본 하드웨어의 논리적 그룹입니다. 장애 도메인마다 공통 전원과 네트워크 스위치를 공유합니다. HDInsight 클러스터 내의 노드를 구현하는 가상 컴퓨터와 관리 디스크는 이러한 장애 도메인에 분산되어 있습니다. 이 아키텍처에서는 실제 하드웨어 오류의 잠재적 영향을 제한합니다.

Azure 지역마다 특정 수의 장애 도메인이 있습니다. 도메인 목록과 해당 도메인에 포함된 장애 도메인의 수에 대한 내용은 [가용성 집합](../virtual-machines/linux/regions-and-availability.md#availability-sets) 설명서를 참조하세요.

> [!IMPORTANT]
> Kafka는 장애 도메인을 인식하지 않습니다. Kafka에서 토픽을 만들 때 모든 파티션 복제본을 동일한 장애 도메인에 저장할 수 있습니다. 이 문제를 해결하기 위해 [Kafka 파티션 리밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools)(영문)를 제공합니다.

## 파티션 복제본의 부하를 다시 조정해야 하는 경우
<a id="when-to-rebalance-partition-replicas" class="xliff"></a>

가장 높은 Kafka 데이터 가용성을 보장하려면 다음과 같은 경우에 토픽에 대한 파티션 복제본의 부하를 다시 조정해야 합니다.

* 새 토픽 또는 파티션을 만들 때

* 클러스터를 확장할 때

## 복제 계수
<a id="replication-factor" class="xliff"></a>

> [!IMPORTANT]
> 3개의 장애 도메인을 포함하는 Azure 지역을 사용하고 복제 계수로 3을 사용하는 것이 좋습니다.

2개의 장애 도메인만 포함하는 지역을 사용해야 하는 경우 복제 계수로 4를 사용하여 두 장애 도메인에 복제본을 동일하게 분산합니다.

토픽을 만들고 복제 계수를 설정하는 예제는 [HDInsight의 Kafka 시작](hdinsight-apache-kafka-get-started.md) 문서를 참조하세요.

## 파티션 복제본의 부하를 다시 조정하는 방법
<a id="how-to-rebalance-partition-replicas" class="xliff"></a>

[Kafka 파티션 리밸런스 도구](https://github.com/hdinsight/hdinsight-kafka-tools)를 사용하여 선택한 토픽의 부하를 다시 조정합니다. 이 도구는 SSH 세션에서 Kafka 클러스터의 헤드 노드로 실행되어야 합니다.

SSH를 사용하여 HDInsight에 연결하는 방법에 대한 자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서를 참조하세요.

## 다음 단계
<a id="next-steps" class="xliff"></a>

* [HDInsight의 Kafka 확장성](hdinsight-apache-kafka-scalability.md)
* [HDInsight의 Kafka 미러링](hdinsight-apache-kafka-mirroring.md)
