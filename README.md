Petit projet Prometheus+Grafana (solutions opensource, free)

OS : Debian 12

Objectif : Dashboard affichant le trafic presque instantanéement (2 sec de délai) du réseau en direct.
Carte réseau de référence : carte physique de l'hôte, le trafic doit passer dessus pour qu'il puisse être interprété par prometheus puis affiché par graphana.

Arborescence à créer :

prometheus-stack/

├── docker-compose.yml

├── prometheus/

│   └── prometheus.yml
