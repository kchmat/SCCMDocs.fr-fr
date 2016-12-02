---
title: "Stratégie de hiérarchie source | System Center Configuration Manager"
description: "Configurez une hiérarchie source et collectez les données d’un site source avant de configurer une tâche de migration System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 11ab1dc90c3e26b159346693b8e85a182219daf4


---
# <a name="planning-a-source-hierarchy-strategy-in-system-center-configuration-manager"></a>Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de configurer une tâche de migration dans votre environnement System Center Configuration Manager, vous devez configurer une hiérarchie source et collecter des données depuis au moins un site source de cette hiérarchie. Servez-vous des sections suivantes pour planifier la configuration de hiérarchies sources et de sites sources, ainsi que pour déterminer la manière dont Configuration Manager collecte les informations depuis les sites sources de la hiérarchie source.  

-   [Hiérarchies sources](#BKMK_Source_Hierarchies)  

-   [Sites source](#BKMK_Source_Sites)  

-   [Collecte des données](#BKMK_Data_Gathering)  

##  <a name="a-namebkmksourcehierarchiesa-source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a> Hiérarchies sources  
Une hiérarchie source est une hiérarchie Configuration Manager qui contient les données à migrer. Lorsque vous configurez la migration et spécifiez une hiérarchie source, vous spécifiez le site de niveau supérieur de cette hiérarchie. Ce site est également appelé un site source. Les sites supplémentaires à partir desquels vous pouvez migrer des données dans la hiérarchie source sont également appelés des sites sources :  

-   Quand vous configurez une tâche de migration pour migrer des données depuis une hiérarchie source Configuration Manager 2007, vous la configurez pour migrer les données d’un ou de plusieurs sites sources spécifiques de la hiérarchie source.  

-   Quand vous configurez une tâche de migration pour migrer les données d’une hiérarchie source qui exécute System Center 2012 Configuration Manager ou une version ultérieure, vous devez uniquement spécifier le site de niveau supérieur.  

Vous pouvez configurer une seule hiérarchie source à la fois :  

-   Si vous configurez une nouvelle hiérarchie source, cette hiérarchie devient automatiquement la hiérarchie source actuelle et elle remplace la hiérarchie source précédente.  

-   Quand vous configurez une hiérarchie source, vous devez spécifier le site de niveau supérieur de celle-ci, ainsi que les informations d’identification nécessaires à Configuration Manager pour se connecter au fournisseur SMS et à la base de données de site du site source.  

-   Configuration Manager utilise ces informations d’identification pour collecter des données et récupérer des informations sur les objets et les points de distribution à partir du site source.  

-   Dans le cadre du processus de collecte des données, les sites enfants de la hiérarchie source sont identifiés.  

-   Si la hiérarchie source est une hiérarchie Configuration Manager 2007, vous pouvez ensuite configurer ces sites supplémentaires en tant que sites sources, avec des informations d’identification distinctes pour chaque site source.  

Même si vous pouvez configurer plusieurs hiérarchies sources successivement, la migration est active pour une seule hiérarchie source à la fois :  

-   Si vous configurez une hiérarchie source supplémentaire avant d’effectuer la migration à partir de la hiérarchie source actuelle, Configuration Manager annule les tâches de migration en cours et reporte les tâches de migration planifiées pour la hiérarchie source actuelle.  

-   La nouvelle hiérarchie source configurée devient alors la hiérarchie source actuelle, et la hiérarchie source d’origine est maintenant inactive.  

-   Vous pouvez ensuite configurer les informations d'identification de connexion, les sites sources supplémentaires et les tâches de migration pour la nouvelle hiérarchie source.  

Si vous restaurez une hiérarchie source inactive et que vous n'avez pas exécuté l'action **Nettoyer les données de migration** précédemment, vous pouvez voir les tâches de migration configurées pour cette hiérarchie source. Cependant, avant de pouvoir continuer la migration à partir de cette hiérarchie, vous devez reconfigurer les informations d'identification pour vous connecter à chaque site source applicable et replanifier les tâches de migration qui n'ont pas été terminées.  

> [!CAUTION]  
>  Si vous migrez des données à partir de plusieurs hiérarchies source, chaque hiérarchie source supplémentaire doit contenir un ensemble unique de codes de site.  

Pour plus d’informations sur la configuration d’une hiérarchie source, consultez [Configuration des hiérarchies sources et des sites sources pour la migration vers System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="a-namebkmksourcesitesa-source-sites"></a><a name="BKMK_Source_Sites"></a> Sites sources  
 Les sites source sont des sites dans la hiérarchie source qui contiennent des données à migrer. Le site de niveau supérieur de la hiérarchie source est toujours le premier site source. Lorsque la migration collecte des données à partir du premier site source d'une nouvelle hiérarchie source, elle découvre des informations à propos des sites supplémentaires dans cette hiérarchie.  

 À la fin de la collecte de données du site source initial, les actions suivantes que vous effectuez dépendent de la version du produit de la hiérarchie source.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Sites sources exécutant Configuration Manager 2007 SP2  
 Une fois les données collectées à partir du site source initial de la hiérarchie Configuration Manager 2007 SP2, vous n’avez pas à configurer de sites sources supplémentaires pour créer des tâches de migration. Toutefois, pour pouvoir migrer les données à partir de sites supplémentaires, vous devez configurer les sites supplémentaires en tant que sites sources, et System Center Configuration Manager doit collecter correctement les données depuis ces sites.  

 Pour collecter des données depuis des sites supplémentaires, vous devez configurer individuellement chaque site comme site source. Vous devez définir les informations d’identification pour la connexion de System Center Configuration Manager au fournisseur SMS et à la base de données de site de chaque site source. Après avoir configuré les informations d'identification d'un site source, le processus de collecte de données commence pour ce site.  

 Quand vous configurez des sites sources supplémentaires dans une hiérarchie source Configuration Manager 2007 SP2, vous devez configurer les sites sources du haut vers le bas, ce qui signifie que vous configurez les sites de niveau inférieur en dernier. Vous pouvez configurer des sites source ans une branche de la hiérarchie à tout moment, mais vous devez configurer un site comme site source pour pouvoir configurer ses sites enfant comme sites source.  

> [!NOTE]  
>  Seuls les sites principaux d’une hiérarchie Configuration Manager 2007 SP2 sont pris en charge pour la migration.  

### <a name="source-sites-that-run-system-center-2012-configuration-or-later"></a>Sites sources exécutant System Center 2012 Configuration Manager ou version ultérieure  
 Une fois les données collectées à partir du site source initial de la hiérarchie System Center 2012 Configuration Manager ou une version ultérieure, vous n’avez pas à configurer de sites sources supplémentaires dans cette hiérarchie source. En effet, contrairement à Configuration Manager 2007, ces versions de Configuration Manager utilisent une base de données partagée qui vous permet d’identifier, puis de migrer tous les objets disponibles à partir du site source initial.  

 Toutefois, lorsque vous configurez les comptes d'accès pour collecter des données, il peut être nécessaire d'accorder l'accès **Compte fournisseur SMS du site source** à plusieurs ordinateurs de la hiérarchie source. Cela peut être nécessaire lorsque le site source prend en charge plusieurs instances du fournisseur SMS, chacune sur un ordinateur différent. Lorsque la collecte des données commence, le site de niveau supérieur de la hiérarchie de destination contacte le site de niveau supérieur de la hiérarchie source pour identifier les emplacements du fournisseur SMS de ce site. Seule la première instance du fournisseur SMS est identifiée. Si le processus de collecte des données ne peut pas accéder au fournisseur SMS à l'emplacement identifié, le processus échoue et ne tente pas de se connecter à d'autres ordinateurs qui exécutent une instance du fournisseur SMS pour le site.  

##  <a name="a-namebkmkdatagatheringa-data-gathering"></a><a name="BKMK_Data_Gathering"></a> Collecte des données  
 Dès que vous avez spécifié une hiérarchie source, configuré les informations d’identification de chaque site source supplémentaire dans une hiérarchie source ou partagé les points de distribution d’un site source, Configuration Manager commence à collecter des données depuis le site source.  

 La collecte de données se répète ensuite selon une planification simple pour maintenir la synchronisation avec les modifications apportées aux données dans le site source. Par défaut, le processus se répète toutes les quatre heures. Vous pouvez modifier la planification du cycle en modifiant les **propriétés** du site source. Le processus de collecte de données initial doit vérifier tous les objets de la base de données Configuration Manager, ce qui peut prendre beaucoup de temps. Les processus de collecte de données suivants identifient uniquement les modifications apportées aux données et ils s'exécutent plus rapidement.  

 Pour collecter des données, le site de niveau supérieur dans la hiérarchie de destination se connecte au fournisseur SMS et à la base de données du site source pour récupérer une liste d'objets et les points de distribution. Ces connexions utilisent les comptes d'accès de site source. Pour plus d’informations sur les configurations nécessaires pour la collecte des données, consultez [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 Vous pouvez démarrer et arrêter la collecte des données à l’aide des actions **Collecter les données maintenant** et **Arrêter la collecte de données** dans la console Configuration Manager.  

 Après avoir utilisé l'option **Arrêter la collecte de données** pour un site source pour une raison quelconque, vous devez reconfigurer les informations d'identification du site pour pouvoir collecter de nouveau les données de ce site. Configuration Manager ne peut pas identifier les nouveaux objets ni les modifications apportées aux objets migrés tant que vous ne reconfigurez pas le site source.  

> [!NOTE]  
>  Avant de développer un site principal autonome dans une hiérarchie avec un site d'administration centrale, vous devez arrêter toutes les collectes des données. Vous pouvez reconfigurer la collecte des données lorsque le développement du site est terminé.  

### <a name="gather-data-now"></a>Collecter les données maintenant  
 Après l'exécution du processus initial de collecte des données d'un site, le processus se répète pour identifier les objets mis à jour depuis le dernier cycle de collecte des données. Vous pouvez également utiliser l’action **Collecter les données maintenant** dans la console Configuration Manager pour démarrer immédiatement le processus et réinitialiser l’heure de début du cycle suivant.  

 Lorsqu'un processus de collecte de données aboutit pour un site source, vous pouvez partager les points de distribution à partir du site source et configurer des tâches de migration pour migrer les données depuis le site. La collecte des données est un processus répétitif pour la migration et il se poursuit jusqu'à ce que vous changiez la hiérarchie source ou exécutiez l'action **Arrêter la collecte de données** pour mettre fin au processus de collecte des données du site.  

### <a name="stop-gathering-data"></a>Arrêter la collecte de données  
 Vous pouvez exécuter l’action **Arrêter la collecte de données** pour mettre fin à la collecte des données d’un site source quand vous ne souhaitez plus que Configuration Manager identifie les objets nouveaux et modifiés du site. Cette action empêche également Configuration Manager de proposer aux clients de la hiérarchie de destination des points de distribution partagés de la source en tant qu’emplacements pour le contenu que vous avez migré.  

 Pour arrêter la collecte des données de chaque site source, vous devez exécuter l'action **Arrêter la collecte de données** sur les sites source de niveau inférieur, puis répéter le processus sur chaque site parent. Le site de niveau supérieur de la hiérarchie source doit être le dernier site sur lequel vous arrêtez la collecte des données. Vous devez arrêter la collecte des données sur chaque site enfant avant d'effectuer cette action sur un site parent. En règle générale, vous arrêtez la collecte de données uniquement lorsque vous êtes prêt à exécuter le processus de migration.  

 Lorsque vous arrêtez la collecte des données d'un site source, les informations collectées précédemment sur l'objet et les collections du site peuvent toujours être utilisées lorsque vous configurez de nouvelles tâches de migration. Toutefois, vous ne voyez pas les nouveaux objets ou regroupements ou vous voyez les modifications apportées aux objets existants. Si vous reconfigurez le site source et recommencez à collecter les données, vous voyez les informations et l'état des objets précédemment migrés.  



<!--HONumber=Nov16_HO1-->

