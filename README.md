# metricbeat-filebeat

Premiers réflexes vérifier le statut des pods sur le cluster concerné (et le nombre de restarts)

$ kubectl get po -n elastic-beats --watch

Situation attendue :

Les pods sont tous en statut running
Leur âge est approchant.
Un pod dont l'âge serait sensiblement plus faible que les autres pourrait avoir redémarré suite à un incident.
Le nombre de restarts est faible en regard de l'âge du pod.
ATTENTION : Un pod avec zero restart n'est pas forcément en bonne santé.
Il peut avoir pris le relai d'un autre pod qui serait tombé suite à un incident.
n pods peuvent se succéder à intervalle rapide, passer brièvement en statut "running" avant de tomber, en affichant chacun 0 restart.
=> Effectuez plusieurs fois la requête avec quelques secondes d'intervalle pour vérifier que les statuts sont stables, ou appliquez le paramètre --watch pour suivre l'évolution en temps réel.
Controler les logs du filebeat du worker où est schedulé les pods de l'application dont les logs ne remontent pas
Situation attendue : pas de logs indiquants des erreurs.
