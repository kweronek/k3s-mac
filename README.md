# k3s-mac

## Beschreibung k3s-mac
Eine Reihe von Shell-Skripten, um auf dem Mac ein k3s-Cluster zur erzeugen, zu betreiben und zu löschen.

### Anwendungsfall
k3s-Cluster ermöglichen die schnelle und Ressourcenschonen Implementeriung eines voll funktionsfähigen Kubernetes-Clusters auf einen MAC. Dadurch können einen Vielzahl von Kubernetes-Anwendungen auf dem MAC getestet werden.

### Funktionsweise


### Voraussetzungen and technische Anforderungen
Benötigt wird:
* Hardware: Mac mit mindestens MacOS 10.X, zwei Cores, minimal  4GB RAM, minimal 10 GB Plattenspeicher,
* Software: Canonical multipass,
* Internetverbindung zum Laden der Ubuntu und k3s Software.

## Skripte und Anwendung:

### addCluster
`addCluster` erstellt Master- und Worker-Nodes und erzeugt einen neuen k3s Cluster.  
```  
addCluster `*<Cluster-Name>*` <Zahl der Worker-Nodes> <Zahl der Master-Nodes>  
```
Als Cluster-Name wird dann `k3s-<Cluster-Name>` verwendet. Die Knotenbezeichnungen sind dann:  
```
k3s-<Cluster-Name>-master-0
k3s-<Cluster-Name>-worker-<i>` mit `<i>=0 ... <Zahl der Worker-Nodes>
```
Hinweis: in der aktuellen Version ist nur ein Master-Node möglich (Einsatz von SQ-Lite)
### getKubeconfig
`getKubeconfig` holt die Kubeconfig-Datei `<Master-Node-Name>/etc/rancher/k3s/k3s.yaml` vom Master und  
kopiert diese mit dem Namen `.kubeconfig` in das lokale Verzeichnis  

### stopCluster
`stopCluster` stoppt alle Master- und Worker-Knoten eines Clusters.
```
stopCluster <Cluster-Name>
```
### startCluster
`startCluster` startet alle Master- und Worker-Knoten eines Clusters.
```
stopCluster <Cluster-Name>
```
### purgeCluster
`purgeCluster` stoppt alle Master- und Worker-Knoten eines Clusters und löscht nicht wiederherstellbar.
```
stopCluster <Cluster-Name>
```
## Hilfreiche Befehle
`multipass get notes`  
`mulitpass get info <Knoten-Name>`  
