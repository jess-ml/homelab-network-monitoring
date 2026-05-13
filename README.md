# 🖥️ Homelab – Supervision Réseau (Prometheus + Grafana)

> Projet personnel – Monitoring & Observabilité réseau  
> Certification Expert Informatique SI – RNCP Niveau 7 | EPSI

---

## 📋 Description

Déploiement d'un environnement de supervision réseau complet via **Docker Compose** :
Prometheus pour la collecte de métriques, Grafana pour la visualisation, AlertManager
pour la gestion des alertes et Node Exporter pour la supervision des hôtes Linux.

Ce homelab simule un environnement de production avec plusieurs hôtes supervisés,
des tableaux de bord personnalisés et des alertes configurées par seuils.

---

## 🏗️ Architecture
```
┌─────────────────────────────────────────────┐
│              Docker Compose                  │
│                                             │
│  ┌──────────┐    ┌──────────┐              │
│  │Prometheus│───▶│ Grafana  │              │
│  │ :9090    │    │  :3000   │              │
│  └──────────┘    └──────────┘              │
│       │                                     │
│       ▼                                     │
│  ┌──────────┐    ┌──────────────┐          │
│  │  Alert   │    │ Node Exporter│          │
│  │ Manager  │    │    :9100     │          │
│  │  :9093   │    └──────────────┘          │
│  └──────────┘                               │
└─────────────────────────────────────────────┘
```
---

## 🛠️ Stack technique

| Outil | Rôle | Port |
|-------|------|------|
| **Prometheus** | Collecte et stockage des métriques | 9090 |
| **Grafana** | Visualisation et tableaux de bord | 3000 |
| **AlertManager** | Gestion et routage des alertes | 9093 |
| **Node Exporter** | Export des métriques système Linux | 9100 |
| **Docker Compose** | Orchestration des conteneurs | — |

---

## 📁 Structure du repo
```
homelab-network-monitoring/
├── README.md
├── docker-compose.yml
├── prometheus/
│   ├── prometheus.yml          # Config Prometheus
│   └── alerts.yml              # Règles d'alertes
├── alertmanager/
│   └── alertmanager.yml        # Config AlertManager
└── grafana/
└── provisioning/
├── datasources/
│   └── datasource.yml  # Source de données Prometheus
└── dashboards/
└── dashboard.yml   # Config des dashboards
```
---

## 🚀 Lancer le projet

### Prérequis
- Docker installé
- Docker Compose installé

### Démarrer la stack
```bash
git clone https://github.com/TON-PSEUDO/homelab-network-monitoring
cd homelab-network-monitoring
docker-compose up -d
```

### Accéder aux interfaces

| Interface | URL | Identifiants |
|-----------|-----|-------------|
| Grafana | http://localhost:3000 | admin / admin |
| Prometheus | http://localhost:9090 | — |
| AlertManager | http://localhost:9093 | — |
| Node Exporter | http://localhost:9100 | — |

### Arrêter la stack
```bash
docker-compose down
```

---

## 📊 Métriques supervisées

- Utilisation CPU (par cœur et globale)
- Utilisation RAM (disponible, utilisée, en cache)
- Espace disque (par partition)
- Trafic réseau (entrant/sortant par interface)
- Charge système (load average)
- Nombre de processus actifs
- Uptime des services

---

## 🔔 Alertes configurées

| Alerte | Seuil | Sévérité |
|--------|-------|----------|
| CPU élevé | > 80% pendant 2 min | Warning |
| CPU critique | > 95% pendant 5 min | Critical |
| RAM faible | < 10% disponible | Warning |
| Disque plein | > 85% utilisé | Warning |
| Disque critique | > 95% utilisé | Critical |
| Hôte inaccessible | Down > 1 min | Critical |

---

## 👤 Réalisé par

Projet personnel – Supervision et observabilité réseau  
**Expert Informatique et Système d'Information – RNCP Niveau 7**  
EPSI | Promotion 2024-2026
