# Prometheus+Grafana, affichage du flux en temps presque réel
## Présentation
_OS de test : Debian 12_

**Objectif :** 
Créer un dashboard type "Jauge" (comme speedtest) affichant le flux DOWN/UP (RX/TX ; réception/envoie) de manière presque instantannée.
Carte réseau de référence : carte physique de l'hôte, le trafic doit passer dessus pour qu'il puisse être interprété par prometheus puis affiché par graphana.
>[!NOTE]
>Graphana interpête les informations reçues par Prometheus.
>Graphana utilise un "scape" c'est à dire, un temps d'actualise à interval régulier. Celui-ci est réglé à 1 seconde dans cette configuration.
>C'est à cause de ce "scape" qu'on ne parle pas de temps réel; car il y a un délai applicatif avant émission/réception des informations. 

**Résultat :**
IMG

### 1. Configuration Environnement
**Arborescence à créer :**
```
prometheus-stack/
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
```
**Commande :**
```
mkdir -p /prometheus-stack/prometheus/
```
>[!TIP]
>🌐 Accès aux interfaces :<br>
>Prometheus : http://IP_MACHINE:9090<br>
>Grafana : http://IP_MACHINE:3000<br>
>Login : admin<br>
>Password : admin (à changer à la première connexion)<br>

>[!IMPORTANT]
>Remplacer IP_MACHINE par l'adresse IPv4 de la machine (hôte généralement)

## 🧭 Étapes suivantes :
Ajouter la source Prometheus dans Grafana (elle sera à http://IP_MACHINE:9090)


>[!CAUTION]
> Cette partie du readme n'est pas encore approuvé à 100%, les menus ont légèrement changé avec la dernière mise à jour.

### 2. Configurer Prometheus comme datasource dans Grafana :
```
-> Menu latéral → ⚙️ Configuration → Data Sources
-> ➕ Add data source → Choisir Prometheus
-> URL : http://IP_MACHINE:9090
-> Enregistre
```
### 3. Importer le fichier .json :
```
Menu latéral → 📊 Dashboards → Import
ID : 1860 → Node Exporter Full
Sélectionne ta datasource Prometheus → Importer
```


### 4. Importer un Dashboard Node Exporter (optionnel pour test) :
```
Menu latéral → 📊 Dashboards → Import
ID : 1860 → Node Exporter Full
Sélectionne ta datasource Prometheus → Importer
```

>[!NOTE]
> 🟢 Tu devrais maintenant avoir un dashboard complet avec :
> CPU, RAM, charge, disques, réseau
> Graphiques temps réel avec historique

