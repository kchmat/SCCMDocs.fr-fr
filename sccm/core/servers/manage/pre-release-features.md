---
title: "Fonctionnalités de préversion"
titleSuffix: Configuration Manager
description: "Fonctionnalités en préversion dans System Center Configuration Manager"
ms.custom: na
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: "36"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 2ef961732431bd4314229e3da6a65df58592342f
ms.sourcegitcommit: 6c2aa79924c0e7fc64ef5e9003498fc00c349db9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/21/2017
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Fonctionnalités en préversion dans System Center Configuration Manager
*S’applique à : System Center Configuration Manager (Current Branch)*

Les fonctionnalités de préversion sont des fonctions incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production. Ces fonctionnalités sont entièrement prises en charge mais sont toujours en cours de développement. Elles peuvent donc être modifiées jusqu'à ce qu’elles passent en préversion.

 Pour pouvoir sélectionner et utiliser ces fonctions, vous devez d’abord donner votre consentement via la console Configuration Manager.  

Le consentement est une action à effectuer une seule fois par hiérarchie ; elle ne peut pas être annulée. Tant que vous n’avez pas accepté de les utiliser, vous ne pouvez pas activer les fonctions en préversion incluses avec les mises à jour. Après avoir activé une fonctionnalité en préversion, vous ne pouvez pas la désactiver.

Pour donner votre consentement, accédez à la console, sélectionnez **Administration** > **Configuration du site** > **Sites**, puis choisissez **Paramètres de hiérarchie**. Sous l’onglet **Général**, choisissez **Accepter d’utiliser les fonctionnalités en préversion**.

Lorsque vous installez une mise à jour qui comprend des fonctionnalités de préversion, ces dernières sont affichées dans l’Assistant Maintenance et mises à jour, avec les fonctionnalités standard incluses dans la mise à jour :
  - **Si vous avez donné votre consentement :** vous pouvez activer les fonctionnalités à partir de l’Assistant Maintenance et mises à jour quand vous installez la mise à jour. Pour ce faire, sélectionnez les fonctionnalités de préversion, comme vous le feriez pour toute autre fonctionnalité.     

    Si vous le souhaitez, vous pouvez attendre pour activer une fonctionnalité en préversion par la suite à partir du nœud **Administration** > **Mises à jour et maintenance** > **Fonctionnalités** de la console. Dans le nœud **Fonctionnalités**, sélectionnez la fonctionnalité, puis choisissez **Activer**. Cette option est grisée jusqu’à ce que vous donniez votre consentement. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.)
  -   **Si vous n’avez pas donné votre consentement :** lorsque vous installez une mise à jour, les fonctionnalités en préversion sont visibles dans l’Assistant Mises à jour et maintenance, mais elles sont grisées et ne peuvent pas être activées. Une fois la mise à jour installée, vous pouvez afficher ces fonctionnalités dans le nœud **Fonctionnalités**. Mais vous ne pouvez pas les activer tant que vous n’avez pas donné votre consentement dans **Paramètres de hiérarchie**.

Si vous avez donné votre consentement sur un site principal autonome, et si vous développez ensuite la hiérarchie en installant un nouveau site d’administration centrale, vous devez redonner votre consentement sur ce dernier.

 Quand vous activez une fonctionnalité en préversion, le Gestionnaire de hiérarchie de Configuration Manager (HMAN) doit traiter le changement avant que cette fonctionnalité ne soit disponible. Le traitement du changement est souvent immédiat, mais il peut prendre jusqu’à 30 minutes en fonction du cycle de traitement HMAN. Une fois le changement traité, vous devez redémarrer la console pour voir la nouvelle interface utilisateur associée à cette fonctionnalité.

**Les fonctionnalités en préversion disponibles sont les suivantes** :

 |Fonctionnalité          |Ajoutée en préversion | Ajoutée en version complète|  
|------------------|---------------------|---------------------|
| Exécuter l’étape de la séquence de tâches <!-- 1261338 --> |  [Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Version 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Évaluation de l’attestation de l’intégrité des appareils pour les stratégies de conformité pour l’accès conditionnel <!-- 1235616 --> |  [Version 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager <!-- 1236459 --> |  [Version 1706](/sccm/apps/deploy-use/create-deploy-scripts)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gérer les mises à jour du pilote Microsoft Surface <!-- 1098490 --> |  [Version 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Version 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Gestion Device Guard avec Configuration Manager <!-- 1319346 --> |  [Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Mise en cache préalable du contenu de la séquence de tâches <!-- 1021244 --> |  [Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Version 1706](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application <!-- 1284624 --> |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Version 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Point de service de l’entrepôt de données <!-- 1277922 --> |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |[Version 1706](/sccm/core/servers/manage/data-warehouse)|
| Cache d’homologue pour la distribution de contenu aux clients <!-- 1101436 --> |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Version 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Passerelle de gestion cloud <!-- 1101764 --> |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Connecteur Microsoft Operations Management Suite <!-- 1236739 --> | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Maintenance d’un regroupement prenant en charge les clusters (maintenance d’un groupe de serveurs) <!-- 1081776 --> | [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Accès conditionnel pour les PC gérés par System Center Configuration Manager <!--  --> | [Version 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
