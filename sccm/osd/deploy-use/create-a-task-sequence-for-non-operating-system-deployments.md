---
title: "Créer une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation"
titleSuffix: Configuration Manager
description: "Créez des séquences de tâches qui ne sont pas liées au déploiement de systèmes d’exploitation, telles que la distribution de logiciels, la mise à jour de pilotes, la modification des états utilisateur, etc."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: "6"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: e4a6e8e708a4c54be7dd84b0b3193cc00871ee88
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Créer une séquence de tâches pour des déploiements autres que des déploiements de systèmes d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les séquences de tâches permettent d’automatiser diverses tâches au sein de votre environnement. Ces tâches visent essentiellement à déployer des systèmes d’exploitation et sont testées à cet effet.  Configuration Manager offre bien d’autres fonctionnalités, des technologies essentielles à utiliser dans certains scénarios, comme l’[installation d’applications](../../apps/understand/introduction-to-application-management.md), l’[installation de mises à jour logicielles](../../sum/understand/software-updates-introduction.md), la [configuration de paramètres](../../compliance/understand/ensure-device-compliance.md) ou l’automatisation personnalisée. Vous devez aussi considérer d’autres technologies d’automatisation Microsoft System Center, notamment [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) et [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) .  

Le principal intérêt des séquences de tâches réside dans leur flexibilité et dans la façon dont vous pouvez les utiliser pour configurer les paramètres des clients, distribuer les logiciels, mettre à jour les pilotes, modifier les états utilisateur et effectuer d’autres tâches indépendantes du déploiement de systèmes d’exploitation. Vous pouvez créer une séquence de tâches personnalisée pour ajouter un nombre quelconque de tâches. L’utilisation de séquences de tâches personnalisées pour un déploiement autre que celui d’un système d’exploitation est prise en charge dans Configuration Manager. Toutefois, si une séquence de tâches entraîne des résultats incohérents ou indésirables, essayez de simplifier l’opération. Pour cela, vous pouvez suivre des étapes plus simples, en répartissant les actions entre plusieurs séquences de tâches, ou en adoptant une approche par étapes pour la création et le test de séquences de tâches.

 Les étapes suivantes peuvent être utilisées dans une séquence personnalisée de tâches de déploiement, autre qu’un déploiement de système d’exploitation :  

-   [Vérifier la préparation](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Se connecter à un dossier réseau](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Télécharger le contenu du package](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Installer l’application](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Installer le package](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Installer les mises à jour logicielles](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Redémarrer l’ordinateur](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [Exécuter la ligne de commande](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Exécuter le script PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Définir des variables dynamiques](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Définir la variable de séquence de tâches](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Étapes suivantes 
[Déployer la séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
