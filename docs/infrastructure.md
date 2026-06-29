# Infrastructure OSIRIS — État actuel et architecture cible

## 1. Vue d'ensemble

Ce document décrit l'infrastructure technique sur laquelle repose le projet OSIRIS : l'accès au serveur d'hébergement, la virtualisation des composants du SIEM/XDR, et l'architecture réseau cible visant à centraliser la sécurité périmétrique via un pare-feu dédié.

L'infrastructure est découpée en trois couches :

1. **Accès distant sécurisé** — tunnel WireGuard
2. **Virtualisation** — hyperviseur Proxmox VE hébergeant l'ensemble des VM du projet
3. **Sécurité réseau** — segmentation et filtrage via une VM pfSense *(à venir)*

## 2. Accès distant — WireGuard

L'accès à l'infrastructure d'hébergement se fait exclusivement via un tunnel **WireGuard**, garantissant une connexion chiffrée de bout en bout entre le poste de travail et le serveur distant.

* Le serveur physique sur lequel repose Proxmox est mis à disposition dans le cadre du projet et n'est pas géré en propre sur le plan de l'hébergement.
* WireGuard sert de point d'entrée unique : une fois le tunnel établi, l'interface web de Proxmox ainsi que le réseau interne des VM deviennent accessibles.
* Cette approche évite d'exposer directement l'interface de gestion Proxmox (port 8006) ou les services internes sur Internet, réduisant la surface d'attaque.

**État actuel :** opérationnel.

## 3. Virtualisation — Proxmox VE

Proxmox VE constitue la couche d'hyperviseur sur laquelle l'ensemble des machines virtuelles du projet OSIRIS sont déployées et administrées.

* Toutes les VM (collecte de logs, Wazuh manager/indexer/dashboard, futurs composants Elastic/OpenSearch, outils annexes) sont hébergées sur ce même hôte Proxmox.
* L'administration se fait via l'interface web de Proxmox, accessible uniquement après établissement du tunnel WireGuard (cf. section 2).
* Cette mutualisation sur un hôte unique correspond aux exigences pédagogiques du Mastercamp, qui imposent une manipulation directe de Proxmox plutôt qu'un recours à des VM cloud indépendantes.

**État actuel :** opérationnel — VM du projet déployées et administrées sur cet hôte.

## 4. Sécurité réseau — pfSense (architecture cible)

> **Statut : à venir.** Cette section décrit l'objectif d'architecture réseau, pas encore mis en œuvre.

L'objectif est de faire transiter **l'intégralité du trafic réseau des VM** (inter-VM et sortant) par une VM **pfSense** dédiée, afin de centraliser le filtrage et la supervision réseau au niveau périmétrique.

Concrètement, la cible est la suivante :

* pfSense est déployée comme VM sur l'hôte Proxmox, au même titre que les autres composants.
* pfSense agit comme **passerelle par défaut** pour toutes les VM du projet : aucune VM ne communique directement avec le réseau externe sans passer par pfSense.
* Cela permet de mettre en place des règles de pare-feu centralisées, du filtrage par segment, et potentiellement du NAT/routing inter-VLAN selon la segmentation retenue.
* Cette étape s'inscrit dans la logique de défense en profondeur du projet OSIRIS, en complément de la détection assurée par Wazuh.

**Travaux restants :**

- [ ] Déploiement de la VM pfSense sur Proxmox
- [ ] Définition du plan d'adressage / segmentation réseau (VLAN ou réseaux virtuels Proxmox dédiés)
- [ ] Reconfiguration des interfaces réseau des VM existantes pour pointer vers pfSense comme gateway
- [ ] Définition des règles de pare-feu (politique par défaut, règles autorisées par flux)
- [ ] Tests de bascule et validation de la connectivité après mise en place

## 5. Schéma logique (état actuel → cible)

```
Poste de travail
      │
      │  (tunnel WireGuard chiffré)
      ▼
Serveur distant (hôte Proxmox VE)
      │
      ├── VM Wazuh (manager / indexer / dashboard)
      ├── VM(s) annexes du projet OSIRIS
      │
      └── [CIBLE] VM pfSense ─── passerelle par défaut pour toutes les VM
                                  └── filtrage / règles de pare-feu centralisées
```

## 6. Prochaines étapes

1. Finaliser le déploiement des VM applicatives restantes (Elastic Stack / OpenSearch, dashboards) sur Proxmox.
2. Déployer la VM pfSense et l'intégrer au réseau virtuel Proxmox.
3. Basculer la passerelle par défaut de chaque VM vers pfSense.
4. Documenter les règles de pare-feu appliquées (politique de filtrage par flux).
5. Mettre à jour ce document au fur et à mesure de l'avancement (statuts "à venir" → "opérationnel").
