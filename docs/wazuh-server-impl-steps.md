# 🛡️ Projet SIEM Wazuh – Étapes de réalisation

Ce document présente les principales étapes du projet de mise en place d’une infrastructure SIEM basée sur Wazuh, dans un contexte de laboratoire de cybersécurité.

---

## 1. Prise de connaissance de Wazuh

La première étape du projet consiste à comprendre le fonctionnement global de Wazuh et son rôle dans une architecture SIEM.

Cette phase inclut :

- Compréhension des composants principaux :
  - Wazuh Manager (analyse et corrélation des événements)
  - Wazuh Indexer (stockage et recherche des logs)
  - Wazuh Dashboard (interface de visualisation)
  - Agents Wazuh (collecte des logs sur les machines cibles)

- Analyse du flux de données :
  - Les agents envoient les logs au manager
  - Le manager applique des règles de détection et génère des alertes
  - Les données sont stockées dans l’indexer
  - Le dashboard permet la visualisation des événements de sécurité

---

## 2. Installation de la VM Amazon Linux sur VMware

Dans cette étape, une machine virtuelle fournie par Wazuh est utilisée comme base du SIEM.

- Import de l’image OVA officielle Wazuh dans VMware Workstation
- Démarrage de la VM basée sur Amazon Linux 2023
- Vérification du bon fonctionnement des services Wazuh préinstallés
- Accès au dashboard via navigateur web

Cette étape permet une prise en main rapide de l’environnement SIEM sans installation manuelle.

---

## 3. Découverte de Wazuh Server

Une fois la VM opérationnelle, l’environnement Wazuh est exploré en détail.

Activités réalisées :

- Accès au Wazuh Dashboard
- Analyse des tableaux de bord de sécurité
- Exploration des règles de détection
- Compréhension du rôle du Wazuh Manager dans la centralisation des logs
- Observation des indices dans l’Indexer

Cette étape permet de comprendre le fonctionnement interne d’un SIEM opérationnel.

---

## 4. Implémentation d’un premier agent Wazuh et liaison avec le serveur

Un premier agent est installé sur une machine cliente afin de valider la communication avec le serveur Wazuh.

Étapes réalisées :

- Installation de l’agent Wazuh sur une machine Linux ou Windows
- Configuration de l’adresse du Wazuh Manager
- Enregistrement de l’agent auprès du serveur
- Vérification de la communication entre agent et serveur
- Observation des logs remontés dans le dashboard

Cette étape valide le fonctionnement du flux de données entre une machine cliente et le SIEM.

---

## 5. Décision : utilisation cloud AWS ou infrastructure locale

Une phase de décision est ensuite réalisée afin de choisir l’architecture finale du projet.

### Option 1 — Infrastructure locale (recommandée)
- Déploiement sur VMware
- VM Wazuh locale
- Agents sur réseau privé virtuel
- Contrôle total de l’environnement

### Option 2 — Infrastructure cloud AWS
- Déploiement sur instance Amazon Linux
- Scalabilité cloud
- Moins de contrôle sur l’environnement local
- Dépendance à AWS

### Décision attendue
Le choix final dépendra des contraintes du projet (pédagogie, reproductibilité, complexité et objectifs de démonstration).

---

## Conclusion

Ces étapes permettent de structurer la mise en place progressive d’un SIEM fonctionnel basé sur Wazuh, depuis la découverte de l’outil jusqu’à la décision d’architecture finale.
