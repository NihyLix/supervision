# Prometheus+Grafana, affichage du flux en temps presque réel

### Présentation
_OS de test : Debian 12 avec VMware Workstation sous Windows 11 24H2_
Grafana v12.0.0
Prometheus :
```
Build information
version	3.3.1
branch	HEAD
buildDate	20250502-15:03:21
goVersion	go1.24.2
```

**Objectif :** 
Créer un dashboard type "Jauge" (comme speedtest) affichant le flux DOWN/UP (RX/TX ; réception/envoie) de manière presque instantanée.

>[!NOTE]
> Grafana interprète les informations reçues par Prometheus.
> Prometheus utilise un "scrape" c'est-à-dire, un temps d'actualisation à intervalles régulier. Celui-ci est réglé à 1 seconde dans cette configuration.
> C'est à cause de ce "scrape" qu'on ne parle pas de temps réel ; car il y a un délai applicatif avant émission/réception des informations. 

**Résultat :**
![Résultats](https://github.com/NihyLix/supervision/blob/b218aec84d98769cebd037ddd224a581f5361950/image.png)
![Résultats](https://github.com/NihyLix/supervision/blob/main/preview.png)

>[!IMPORTANT]
>Cette configuration a été effectuée pour écouter sur la carte réseau physique de l'hôte.
>Le flux réseau doit en conséquent passer par la carte physique pour être vu par prométheus puis interprété par grafana.
>
### 1. Configuration Environnement
**Arborescence à créer :**
```
prometheus-stack/
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
```
**Commandes :**
```
mkdir -p /prometheus-stack/prometheus/
```
=> On ajoute les 2 fichiers .yml à l'endroit indiqué par l'arborescence ci-dessus. 

```
cd /prometheus-stack/
docker-compose up -d
```

>[!IMPORTANT]
>Remplacer IP_MACHINE par l'adresse IPv4 de la machine (hôte généralement)

>[!TIP]
>🌐 Accès aux interfaces :<br>
>Prometheus : http://IP_MACHINE:9090<br>
>Grafana : http://IP_MACHINE:3000<br>
>Login : admin<br>
>Password : admin (à changer à la première connexion)<br>

## 🧭 Étapes suivantes :

### 2. Ajouter la source Prometheus dans Grafana :


```
-> Menu latéral (haut à gauche) → ⚙️ Connection → Data Sources
-> ➕ Add data source → Choisir Prometheus
-> URL : http://IP_MACHINE:9090
-> Enregistre
```
### 3. Importer le fichier .json :
```
-> Menu latéral (haut à gauche) → 📊 Dashboards
-> New (haut à droite) → Import
-> Upload dashboard JSON file 
-> Import
```
>[!NOTE]
> 🟢 Il devrait maintenant avoir un dashboard avec 2 jauges UP/DOWN avec 2 graphiques pour le suivi historique.


