---
title: "Afficher l’inventaire logiciel avec l’Explorateur de ressources"
titleSuffix: Configuration Manager
description: "Utilisez l’Explorateur de ressources pour afficher l’inventaire logiciel dans System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 242bd336fcb13172097e26187a48c924dbd9acb6
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Comment utiliser l’Explorateur de ressources pour afficher l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’Explorateur de ressources de System Center Configuration Manager pour afficher des informations sur l’inventaire logiciel collecté auprès des ordinateurs de votre hiérarchie.  

> [!NOTE]  
>  L’Explorateur de ressources n’affiche pas de données d’inventaire tant qu’un cycle d’inventaire logiciel n’a pas été exécuté sur le client.  

 L’Explorateur de ressources fournit les informations d’inventaire matériel et logiciel suivantes :  

-   **Logiciels** :  

    -   **Fichiers collectés** : fichiers collectés lors de l’inventaire logiciel.  

    -   **Détails du fichier** : fichiers qui ont été inventoriés pendant l’inventaire logiciel, et qui ne sont pas associés à un produit ou un fabricant spécifique.  

    -   **Dernière analyse logicielle** : date et heure de la dernière collecte d’inventaire logiciel et de fichiers pour l’ordinateur client.  

    -   **Détails du produit** : produits logiciels qui ont été inventoriés par l’inventaire logiciel, regroupés par fabricant.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Pour exécuter l'Explorateur de ressources à partir de la console Configuration Manager  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité**.

2.  Dans l’espace de travail **Ressources et Conformité**, cliquez sur **Appareils** ou ouvrez un regroupement qui affiche des appareils.  

3.  Choisissez l’ordinateur contenant l’inventaire que vous voulez afficher puis, sous l’onglet **Accueil**, dans le groupe **Appareils**, choisissez **Démarrer** > **Explorateur de ressources**.

4.  Vous pouvez cliquer avec le bouton droit sur un élément dans le volet droit de la fenêtre Explorateur de ressources, puis choisir **Propriétés** pour visualiser les informations d’inventaire collectées dans un format plus lisible.  
 
