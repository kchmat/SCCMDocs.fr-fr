---
title: "Gérer Windows Device Guard"
titleSuffix: Configuration Manager
description: "Découvrez comment gérer Windows Device Guard avec System Center Configuration Manager."
ms.custom: na
ms.date: 10/20/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 8d84d0d65db7668baa7be9bbf0ad1df869b37919
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Gestion de Device Guard avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>Introduction
Device Guard est un groupe de fonctionnalités Windows 10 qui sont conçues pour protéger les ordinateurs contre les logiciels malveillants et d’autres logiciels non autorisés. Il empêche le code malveillant de s’exécuter en s’assurant que seul le code approuvé, que vous connaissez, peut être exécuté.

Device Guard englobe les fonctionnalités de sécurité basées aussi bien sur des logiciels que sur du matériel. L’intégrité du code configurable est une couche de sécurité logicielle qui applique une liste explicite de logiciels autorisés à s’exécuter sur un PC. Seule, l’intégrité du code configurable n’a pas de prérequis matériels ou logiciels. Les stratégies Windows Defender Application Control déployées avec Configuration Manager activent une stratégie d’intégrité du code configurable sur les PC de regroupements ciblés qui répondent aux exigences décrites dans cet article (version minimale de Windows et référence SKU). Si vous le souhaitez, vous pouvez activer la protection basée sur un hyperviseur des stratégies d’intégrité du code déployées par le biais de Configuration Manager au moyen de la stratégie de groupe sur le matériel compatible.

Pour en savoir plus sur Device Guard, consultez le [Guide de déploiement de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## <a name="using-device-guard-with-configuration-manager"></a>Utilisation de Device Guard avec Configuration Manager

Vous pouvez utiliser Configuration Manager pour déployer une stratégie Device Guard qui vous permet de configurer le mode dans lequel Windows Defender Application Control s’exécute sur les PC d’un regroupement. 

Vous pouvez configurer l’un des modes suivants :

1.  **Mise en conformité activée** : seuls les exécutables approuvés sont autorisés à s’exécuter.
2.  **Audit uniquement** : autorisez tous les exécutables à s’exécuter, mais journalisez les exécutables non fiables qui s’exécutent dans le journal local des événements du client.

>[!TIP]
>Dans cette version de Configuration Manager, Device Guard est une fonctionnalité en préversion. Pour l’activer, consultez [Fonctionnalités en version préliminaire dans System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Quels composants peuvent s’exécuter quand vous déployez une stratégie Windows Defender Application Control ?

Windows Device Guard vous permet de contrôler précisément les composants qui peuvent s’exécuter sur les ordinateurs que vous gérez. Cette fonctionnalité peut être utile pour les PC des services de haute sécurité, où il est vital que les logiciels indésirables ne puissent pas s’exécuter.

Quand vous déployez une stratégie, les exécutables suivants peuvent généralement s’exécuter :

- Composants du système d’exploitation Windows
- Pilotes du Centre de développement matériel (qui ont des signatures Windows Hardware Quality Labs)
- Applications du Windows Store
- Client Configuration Manager 
- Tous les logiciels déployés par le biais de Configuration Manager que les PC installent après le traitement de la stratégie Windows Defender Application Control. 
- Mises à jour des composants Windows à partir de :
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Ces éléments n’incluent pas les logiciels qui *ne sont pas* intégrés à Windows et qui se mettent à jour automatiquement à partir d’Internet ou de mises à jour logicielles tierces en cas d’installation par le biais d’un des mécanismes de mise à jour mentionnés précédemment, ou à partir d’Internet. Seuls les changements logiciels déployés au moyen du client Configuration Manager peuvent s’exécuter.

## <a name="before-you-start"></a>Avant de commencer

Avant de configurer ou de déployer des stratégies Windows Defender Application Control, lisez les informations suivantes :

- La gestion Device Guard est une fonctionnalité en préversion pour Configuration Manager. Elle est susceptible de changer.
- Pour utiliser Device Guard avec Configuration Manager, les PC que vous gérez doivent exécuter Windows 10 Entreprise version 1703 ou ultérieure.
- Une fois qu’une stratégie est traitée sur un PC client, Configuration Manager est configuré comme un programme d’installation managé sur ce client et les logiciels déployés par le biais de SCCM après le traitement de la stratégie sont automatiquement approuvés. Les logiciels installés par Configuration Manager avant le traitement de la stratégie Windows Defender Application Control ne sont pas approuvés automatiquement.
- Les PC clients doivent être connectés à leur contrôleur de domaine pour que la stratégie Windows Defender Application Control soit traitée correctement.
- L’évaluation de la conformité par défaut pour les stratégies Windows Defender Application Control, configurable pendant le déploiement, s’effectue quotidiennement. Si des problèmes de traitement de la stratégie sont observés, il peut être avantageux de configurer une planification plus fréquente de l’évaluation de la conformité, par exemple toutes les heures. Cette planification détermine la fréquence à laquelle les clients réessayent de traiter une stratégie Windows Defender Application Control en cas d’échec.
- Quel que soit le mode de mise en conformité que vous sélectionnez quand vous déployez une stratégie Windows Defender Application Control, les PC clients ne peuvent pas exécuter des applications HTML avec l’extension .hta.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Comment créer une stratégie Windows Defender Application Control
1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2.  Dans l’espace de travail **Ressources et Conformité**, développez **Endpoint Protection**, puis cliquez sur **Stratégies Windows Defender Application Control**.
3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une stratégie Windows Defender Application Control**.
4.  Dans la page **Général** de l’**Assistant Création d’une stratégie Windows Defender Application Control**, spécifiez les paramètres suivants :
    - **Nom** : entrez un nom unique pour cette stratégie Windows Defender Application Control. 
    - **Description** : si vous le souhaitez, entrez une description pour faciliter l’identification de la stratégie dans la console Configuration Manager.
    - **Mode de mise en conformité** : choisissez une des méthodes de mise en conformité suivantes pour Device Guard sur le PC client.
        - **Mise en conformité activée** : seuls les exécutables approuvés sont autorisés à s’exécuter.
        - **Audit uniquement** : autorisez tous les exécutables à s’exécuter, mais journalisez les exécutables non fiables qui s’exécutent dans le journal local des événements du client.
5.  Sous l’onglet **Inclusions** de l’**Assistant Création d’une stratégie Windows Defender Application Control**, cliquez sur **Ajouter** si vous souhaitez ajouter une approbation pour des fichiers ou des dossiers spécifiques sur les PC. 
6.  Dans la boîte de dialogue **Ajouter fichier ou dossier approuvé**, spécifiez les informations sur le fichier ou dossier que vous souhaitez approuver. Vous pouvez spécifier un chemin de dossier ou de fichier local, ou vous connecter à un appareil distant auquel vous êtes autorisé à vous connecter et spécifier un chemin de fichier ou de dossier sur cet appareil.
Quand vous ajoutez une approbation pour des fichiers ou des dossiers spécifiques dans une stratégie Windows Defender Application Control, vous pouvez :
    - Résoudre les problèmes avec les comportements des programmes d’installation gérés
    - Approuver les applications métier qui ne peuvent pas être déployées avec Configuration Manager
    - Approuver des applications qui sont incluses dans une image de déploiement de système d’exploitation. 
7.  Cliquez sur **Suivant**, puis fermez l’Assistant.

>[!IMPORTANT]
>L’inclusion de fichiers ou de dossiers approuvés n’est prise en charge que sur les PC clients équipés de la version 1706 ou d’une version ultérieure du client Gestionnaire de configuration. Si toutes les règles d’inclusion sont comprises dans une stratégie Windows Defender Application Control et que celle-ci est ensuite déployée sur un PC client équipé d’une version antérieure du client Gestionnaire de configuration, elle ne sera pas appliquée. Pour résoudre ce problème, il suffit de mettre à niveau ces anciennes versions de clients. Les stratégies qui ne comprennent aucune règle d’inclusion peuvent toujours être appliquées sur des versions antérieures du client Gestionnaire de configuration.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Comment déployer une stratégie Windows Defender Application Control
1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2.  Dans l’espace de travail **Ressources et Conformité**, développez **Endpoint Protection**, puis cliquez sur **Stratégies Windows Defender Application Control**.
3.  Dans la liste des stratégies, sélectionnez la stratégie que vous souhaitez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Déployer**.
4.  Dans la boîte de dialogue **Déployer la stratégie Windows Defender Application Control**, sélectionnez le regroupement sur lequel vous souhaitez déployer la stratégie. Ensuite, configurez une planification pour définir à quel moment les clients évaluent la stratégie. Enfin, indiquez si le client peut évaluer la stratégie en dehors des fenêtres de maintenance configurées.
5.  Lorsque vous avez terminé, cliquez sur **OK** pour déployer la stratégie. 

### <a name="restarting-the-device-after-deploying-the-policy"></a>Redémarrage de l’appareil après le déploiement de la stratégie

Une fois que la stratégie est traitée sur un PC client, un redémarrage est planifié sur ce client selon les **paramètres clients** relatifs au **redémarrage de l’ordinateur**. Le redémarrage n’est pas nécessaire pour appliquer des stratégies, mais il s’agit de la valeur par défaut. Si vous souhaitez désactiver les redémarrages, procédez comme suit :

1. Ouvrez l’Assistant **Création d’une stratégie Windows Defender Application**.
2. Sur la page**Général**, décochez la case **Forcer le redémarrage des appareils pour appliquer cette stratégie à tous les processus**.
3. Cliquez sur **Suivant** jusqu'à ce que l'Assistant ait terminé.



## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Comment surveiller une stratégie Windows Defender Application Control

Utilisez les informations de l’article [Surveiller les paramètres de conformité](/sccm/compliance/deploy-use/monitor-compliance-settings) pour vérifier que la stratégie a été correctement déployée sur tous les PC.

Pour surveiller le traitement d’une stratégie Windows Defender Application Control, utilisez le fichier journal suivant sur les PC clients :

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Pour vérifier le logiciel bloqué ou audité, consultez les journaux d’événements suivants du client local :

1.  Pour le blocage et l’audit des fichiers exécutables, utilisez **Journaux des applications et des services** > **Microsoft** > **Windows** > **Intégrité du code** > **Opérationnel**.
2.  Pour le blocage et l’audit du programme d’installation Windows et des fichiers de script, utilisez **Journaux des applications et des services** > **Microsoft** > **Windows** > **AppLocker** > **MSI et Script**.

## <a name="automatically-let-software-run-if-it-is-trusted-by-intelligent-security-graph"></a>Laisser s’exécuter automatiquement les logiciels s’ils sont approuvés par Intelligent Security Graph

Vous pouvez autoriser les appareils verrouillés à exécuter des logiciels jouissant d’une bonne réputation, tel que déterminé par Microsoft Intelligent Security Graph (ISG). ISG inclut [Windows Defender SmartScreen](https://docs.microsoft.com/windows/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) et d’autres services Microsoft. Les appareils doivent exécuter Windows Defender SmartScreen pour que les logiciels soient approuvés.

1. Ouvrez l’Assistant **Création d’une stratégie Windows Defender Application**.
2. Sur la page **Inclusions**, cochez la case **Autoriser les logiciels approuvés par Intelligent Security Graph**.
3. Dans la zone Fichiers ou dossiers approuvés, ajoutez les fichiers et dossiers à approuver.
4. Cliquez sur **Suivant** jusqu'à ce que l'Assistant ait terminé.



## <a name="security-and-privacy-information-for-device-guard"></a>Informations sur la sécurité et la confidentialité pour Device Guard

- Dans cette préversion, ne déployez pas de stratégies Windows Defender Application Control avec le mode de mise en conformité **Audit uniquement** dans un environnement de production. Ce mode est conçu pour vous aider à tester la capacité dans un environnement de laboratoire uniquement.
- Les appareils qui ont une stratégie déployée en mode **Audit uniquement** ou **Mise en conformité activée** et qui n’ont pas encore été redémarrés pour appliquer la stratégie sont vulnérables aux logiciels non autorisés dont l’installation est en cours.
Dans ce cas, le logiciel peut continuer à être autorisé à s’exécuter même en cas de redémarrage de l’appareil ou il reçoit une stratégie en mode **Mise en conformité activée**.
- Pour vérifier que la stratégie Windows Defender Application Control est appliquée, préparez l’appareil dans un environnement lab. Ensuite, déployez la stratégie **Mise en conformité activée**. Pour terminer, redémarrez l’appareil avant de donner l’appareil à un utilisateur final.
- Ne déployez pas une stratégie **Mise en conformité activée** puis plus tard une stratégie **Audit uniquement** sur le même appareil. Il se peut que des logiciels non autorisés soient autorisés à s’exécuter à cause de cette configuration.
- Quand vous utilisez Configuration Manager pour activer l’intégrité du code configurable sur les PC clients avec des stratégies Windows Defender Application Control, la stratégie n’empêche pas les utilisateurs disposant de droits d’administrateur local de contourner la stratégie Windows Defender Application Control ou d’exécuter des logiciels non autorisés. 
- La seule façon d’empêcher les utilisateurs dotés de droits d’administrateur local de désactiver l’intégrité du code configurable consiste à déployer une stratégie binaire signée. Ce déploiement est possible par le biais de la stratégie de groupe, mais il n’est pas pris en charge dans Configuration Manager pour le moment.
- Le paramétrage de Configuration Manager en tant que programme d’installation managé sur les PC clients utilise la stratégie AppLocker. AppLocker est utilisé uniquement pour identifier les programmes d’installation managés et la mise en conformité se produit avec l’intégrité du code configurable. 




