Petit projet Prometheus+Grafana (solutions opensource, free)

OS : Debian 12

Objectif : Dashboard affichant le trafic presque instantanéement (2 sec de délai) du réseau en direct.
Carte réseau de référence : carte physique de l'hôte, le trafic doit passer dessus pour qu'il puisse être interprété par prometheus puis affiché par graphana.

Arborescence à créer :

prometheus-stack/

├── docker-compose.yml

├── prometheus/

│   └── prometheus.yml

🌐 Accès aux interfaces :
Prometheus : http://localhost:9090

Grafana : http://localhost:3000

Login : admin

Password : admin (à changer à la première connexion)

🧭 Étapes suivantes :
Ajouter la source Prometheus dans Grafana (elle sera à http://prometheus:9090)

Importer un dashboard de type Node Exporter Full depuis Grafana.com

4. Configurer Prometheus comme datasource dans Grafana :
Menu latéral → ⚙️ Configuration → Data Sources

➕ Add data source → Choisir Prometheus

URL : http://prometheus:9090

Enregistre

5. Importer un Dashboard Node Exporter (optionnel mais recommandé) :
Menu latéral → 📊 Dashboards → Import

ID : 1860 → Node Exporter Full

Sélectionne ta datasource Prometheus → Importer

🟢 Tu devrais maintenant avoir un dashboard complet avec :

CPU, RAM, charge, disques, réseau

Graphiques temps réel avec historique

