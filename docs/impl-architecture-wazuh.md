# 🛡️ Architecture SIEM basée sur Wazuh – Projet universitaire

## 1. Objectif du projet

L’objectif de ce projet est de mettre en place une infrastructure SIEM (Security Information and Event Management) basée sur Wazuh afin de centraliser, analyser et corréler les événements de sécurité provenant de plusieurs systèmes hétérogènes (Linux, Windows et machines vulnérables).

Cette infrastructure permet de simuler un environnement réaliste de supervision de sécurité (SOC) incluant une machine d’attaque et plusieurs machines cibles.

---

## 2. Architecture générale retenue

L’architecture repose sur une séparation claire entre les machines de production, les machines de test et l’infrastructure SIEM.

### 🧱 Composants principaux :

- 1 VM dédiée au SIEM (Wazuh Server)
- 3 à 4 machines clientes avec agents Wazuh
- 1 machine de test/pentest (Kali Linux)

---

## 3. Répartition des machines virtuelles

### 🖥️ VM 1 — Infrastructure SIEM (isolée)

Cette machine est dédiée exclusivement au système Wazuh.

Elle héberge :
- Wazuh Manager (serveur d’analyse et de corrélation)
- Wazuh Indexer (stockage et recherche des logs)
- Wazuh Dashboard (interface de visualisation)

👉 Cette VM constitue le cœur du SIEM et est totalement isolée des activités offensives.

---

### 🐧 VM 2 — Ubuntu (agent)

- Système Linux standard
- Installation de l’agent Wazuh
- Génération de logs système (auth, processus, réseau)

---

### 🪟 VM 3 — Windows (agent)

- Système Windows
- Agent Wazuh installé
- Surveillance :
  - événements système
  - authentification
  - activité utilisateur

---

### 💀 VM 4 — Metasploitable (agent optionnel)

- Machine volontairement vulnérable
- Sert de cible d’attaque
- Permet de générer des logs exploitables (bruteforce, services vulnérables, scans)

---

### 🐉 VM 5 — Kali Linux (machine d’attaque)

- Machine utilisée pour les tests d’intrusion (Red Team)
- Outils de pentest (scan réseau, exploitation, brute force)
- Peut contenir un agent Wazuh pour remonter certaines activités
- Accès au dashboard Wazuh pour analyse des résultats (optionnel)

---

## 4. Schéma logique de l’architecture

```text
                ┌─────────────────────────────┐
                │     VM SIEM (isolée)        │
                │  Wazuh Manager + Indexer    │
                │  + Dashboard                │
                └─────────────┬───────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
 ┌──────────────┐   ┌────────────────┐   ┌──────────────────┐
 │ Ubuntu VM    │   │ Windows VM     │   │ Metasploitable   │
 │ Wazuh Agent  │   │ Wazuh Agent    │   │ Wazuh Agent      │
 └──────────────┘   └────────────────┘   └──────────────────┘
                              │
                      ┌────────────────┐
                      │ Kali Linux     │
                      │ Pentest + opt. │
                      │ Wazuh Agent    │
                      └────────────────┘
```
