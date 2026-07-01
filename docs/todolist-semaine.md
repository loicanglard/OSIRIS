# Todolist semaine du 29 juin au 5 juillet 2026

Suivi des tâches pour le déploiement des agents Wazuh et la mise en place de pfSense sur l'infrastructure OSIRIS.

> pfSense étant l'étape la plus sensible (bascule réseau de toutes les VM + tests d'attaque), elle est étalée sur 3 jours plutôt que 2 pour limiter les risques et le stress associés.

## Lundi 29 juin — Agents, bases

- [x] Installer l'agent Wazuh sur Mint
- [x] Installer l'agent Wazuh sur Kali
- [x] Vérifier l'enrollment des deux agents dans le manager

## Mardi 30 juin — Agents, suite

- [x] Installer l'agent Wazuh sur Windows 10
- [x] Installer l'agent Wazuh sur Metasploitable (ou agentless si incompatible)
- [x] Vérifier réception des logs des 4 sources dans le dashboard

## Mercredi 1 juillet — Règles & détection

- [ ] Configurer des règles de détection adaptées à Metasploitable (vulnérabilités connues)
- [ ] Activer le File Integrity Monitoring sur Ubuntu et Windows 10
- [ ] Générer un événement de test par source et vérifier l'alerte

## Jeudi 2 juillet — pfSense, étape 1/3 : création

- [x] Créer la VM pfSense dans Proxmox
- [ ] Définir le plan d'adressage réseau (segments / VLAN)
- [ ] Configurer les interfaces réseau de pfSense (WAN/LAN)

## Vendredi 3 juillet — pfSense, étape 2/3 : bascule

- [ ] Basculer la gateway des VM (Wazuh, Mint, Kali, Windows 10) vers pfSense
- [ ] Définir les règles de pare-feu de base (politique par défaut)
- [ ] Tester la connectivité de chaque VM après bascule

## Samedi 4 juillet — pfSense, étape 3/3 : validation

- [ ] Vérifier que le trafic inter-VM passe bien par pfSense (logs pare-feu)
- [ ] Ajuster les règles de pare-feu si des flux légitimes sont bloqués
- [ ] Point de stabilisation avant les tests d'attaque

## Dimanche 5 juillet — Simulation & documentation

- [ ] Simuler une attaque simple depuis Kali vers Metasploitable
- [ ] Vérifier la détection et la corrélation dans Wazuh
- [ ] Mettre à jour `docs/infrastructure.md` (statuts pfSense → opérationnel)
- [ ] Documenter les règles de pare-feu appliquées
- [ ] Bilan de la semaine (acquis + reste à faire)

---

**Progression actuelle : 2 / 23 tâches**
