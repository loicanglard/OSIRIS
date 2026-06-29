# OSIRIS

## Open-source SIEM for Incident Response and Infrastructure Security

### Présentation

OSIRIS est une plateforme SIEM/XDR open source destinée à centraliser la supervision de la sécurité des systèmes d'information, la collecte des journaux et la détection des menaces au sein d'infrastructures hétérogènes.

Face à l'augmentation constante des cyberattaques, des violations de données et des exigences réglementaires, les organisations doivent disposer d'une solution capable d'assurer une visibilité globale de leur environnement informatique. OSIRIS répond à ce besoin en offrant une plateforme centralisée permettant de collecter, analyser et corréler les événements de sécurité provenant de multiples sources.

### Objectifs

L'objectif principal du projet est de concevoir et déployer une solution open source de supervision de sécurité capable d'améliorer la détection des incidents, de faciliter les investigations et de renforcer la visibilité sur l'ensemble de l'infrastructure.

La plateforme doit permettre la collecte centralisée des journaux, la surveillance en temps réel des événements de sécurité, l'analyse des activités suspectes et la production de tableaux de bord facilitant la prise de décision et le suivi opérationnel.

### Fonctionnalités

OSIRIS intègre un ensemble de fonctionnalités essentielles à la supervision de la sécurité :

* Collecte centralisée et gestion des journaux.
* Corrélation et analyse des événements de sécurité.
* Détection des menaces et génération d'alertes en temps réel.
* Surveillance de l'intégrité des fichiers (File Integrity Monitoring).
* Recherche, filtrage et analyse des événements.
* Tableaux de bord et outils de reporting.
* Gestion des accès basée sur les rôles (RBAC).
* Journalisation des activités utilisateurs et traçabilité des actions.
* Gestion sécurisée du stockage et de la rétention des journaux.
* Support des investigations et de la réponse aux incidents.

### Sources de données

La solution est conçue pour intégrer différentes sources de données afin d'assurer une couverture complète de l'infrastructure :

* Postes de travail Windows.
* Serveurs Linux.
* Serveurs Web.
* Pare-feu.
* Équipements réseau.
* Applications et services compatibles Syslog ou API REST.

La collecte peut être réalisée à l'aide d'agents ou via des mécanismes sans agent selon les contraintes techniques des équipements supervisés.

### Architecture technique

OSIRIS repose exclusivement sur des technologies open source reconnues dans le domaine de la cybersécurité et de l'observabilité.

L'architecture s'appuie notamment sur Wazuh comme moteur principal de supervision et de détection, associé à Elastic Stack ou OpenSearch pour l'indexation, la recherche et l'analyse des données. Les interfaces de visualisation peuvent être fournies par Kibana, OpenSearch Dashboards ou Grafana selon les besoins du projet.

Le déploiement est réalisé dans un environnement Linux et peut être exécuté sur des machines virtuelles ou des conteneurs Docker afin de faciliter son intégration et son évolution.

Les développements et automatisations associés reposent principalement sur Python, Bash ainsi que sur des fichiers de configuration YAML et JSON.

### Infrastructure

L'infrastructure du projet repose sur un hyperviseur **Proxmox VE** hébergeant l'ensemble des machines virtuelles, accessible via un tunnel **WireGuard** chiffré. L'objectif cible est de centraliser la sécurité réseau via une VM **pfSense** agissant comme passerelle unique pour l'ensemble des VM.

Le détail de cette architecture (état actuel, schéma logique, travaux restants) est documenté dans [`docs/infrastructure.md`](docs/infrastructure.md).

### Sécurité

La sécurité de la plateforme est assurée par l'utilisation de mécanismes d'authentification sécurisés, de contrôles d'accès granulaires et du chiffrement des communications via TLS/SSL.

OSIRIS garantit la confidentialité, l'intégrité et la disponibilité des données collectées grâce à des politiques de stockage sécurisées, à la journalisation des activités administratives et à la surveillance continue de l'environnement supervisé.

### Conformité

Le projet a été conçu pour faciliter le respect des principales exigences réglementaires et normatives en matière de sécurité de l'information. Les mécanismes de collecte, d'audit, de traçabilité et de contrôle des accès contribuent à la mise en conformité avec des référentiels tels que le RGPD, l'ISO/IEC 27001 et le PCI DSS.

### Bénéfices attendus

La mise en œuvre d'OSIRIS doit permettre d'améliorer significativement la visibilité sur l'infrastructure informatique, de réduire le temps de détection des incidents et d'accélérer les investigations de sécurité.

En s'appuyant sur une architecture centralisée et open source, le projet contribue également à la réduction des coûts d'exploitation tout en favorisant la transparence, l'interopérabilité et le partage des connaissances au sein de la communauté cybersécurité.
