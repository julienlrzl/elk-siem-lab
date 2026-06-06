# Suricata IDS – Détection d’intrusions et supervision réseau
![Suricata](https://img.shields.io/badge/Suricata-EF4444?style=for-the-badge&logoColor=white)
![Elastic](https://img.shields.io/badge/Elastic_Stack-005571?style=for-the-badge&logo=elastic&logoColor=white)
![Kibana](https://img.shields.io/badge/Kibana-005571?style=for-the-badge&logo=kibana&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![syslog-ng](https://img.shields.io/badge/syslog--ng-000000?style=for-the-badge&logoColor=white)

## Présentation

Ce projet met en œuvre un système complet de détection d’intrusions (IDS) et de supervision réseau, reposant sur la pile logicielle Suricata — syslog-ng — Elasticsearch — Kibana.  
L’objectif est de détecter, centraliser et visualiser en temps réel différents types d’activités suspectes au sein d’un réseau local.

Le travail a été réalisé sur une machine virtuelle Ubuntu configurée comme un IDS complet ; la documentation et les captures sont fournies dans le rapport PDF.

---

## Contenu du dépôt

📁 ./  
├── Enonce_Projet.pdf -->Sujet et consignes officielles du projet  
├── Rapport_Projet.pdf --> Rapport final (installation, tests, analyses, captures)  
├── Rapport_Latex/ --> Sources LaTeX du rapport (chapitres, figures, etc.)  
└── README.md --> Présentation du projet (ce fichier)

> Remarque : les fichiers de configuration système (`/etc/suricata/suricata.yaml`, `local.rules`, `syslog-ng.conf`, etc.) et les journaux (`/var/log/suricata/eve.json`, `fast.log`, etc.) **ne sont pas inclus** dans ce dépôt car ils résident dans la VM. Leur contenu est décrit et illustré dans `Rapport_Projet.pdf`.

---

## Description du projet

Le projet intègre et configure les composants suivants :

- **Suricata** : capture et analyse du trafic réseau, génération d’alertes selon des règles personnalisées ;
- **syslog-ng** : collecte et centralisation des logs (lecture du fichier `eve.json` et redirection vers stockage local / rotation) ;
- **Elasticsearch** : indexation et stockage des événements pour recherche et agrégation ;
- **Kibana** : visualisation, filtres et tableaux de bord pour l’analyse interactive.

Cinq scénarios d’intrusion ont été conçus et testés :

1. ICMP (ping)
2. Scan Nmap (reconnaissance)
3. Tentatives SSH (détection de connexions répétées / brute-force)
4. Fuzzing web (volume élevé de requêtes HTTP)
5. Accès FTP anonyme (exemple d’accès service)

Tous les tests, commandes exactes et captures d’écran sont fournis dans `Rapport_Projet.pdf`.

---

## Guide d’utilisation rapide (pour l’évaluateur)

Si vous souhaitez reproduire l’environnement, les étapes générales sont :

1. Démarrer la VM Ubuntu fournie (ou restaurer les configurations depuis le rapport).
2. Lancer Suricata avec la configuration décrite dans le rapport
3. Démarrer syslog-ng / vérifier que `eve.json` est lu (voir `lsof /var/log/suricata/eve.json`).
4. Démarrer Elasticsearch et Kibana, ouvrir Kibana et charger l’index pattern `suricata-*`.
5. Reproduire les scénarios en suivant les commandes du rapport ; vérifier `fast.log` et `eve.json` puis la visualisation dans Kibana Discover / Dashboard.

Les commandes précises et captures sont détaillées dans le rapport.

---

## A propos des artefacts fournis

- Le rapport PDF contient : installation pas-à-pas, fichiers de configuration essentiels (extraits), commandes de test, captures `fast.log` / `eve.json`, et screenshots Kibana.
- Si l’évaluateur souhaite reproduire l’environnement exact, le fichier VM (`.ova`) peut être fourni sur demande (téléchargement externe / clé USB) — indiquer la méthode souhaitée dans une issue du dépôt.

---

## Auteur

Julien Larzul - Tom Humeau - Ian Bertrand - Alexis Georges  
Sécurité Informatique

---
