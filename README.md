# k3s-mac

## Beschreibung
Eine Reihe von Shell-Skripten, um auf dem Mac ein K3s-Cluster zur erzeugen, zu betreiben und zu löschen. K3s ist eine leichtgewichtige aber vollständige und zertifizierte Kubernetes-Distribution. Näheres siehe unter [`K3s`](https://github.com/rancher/k3s).

### Anwendungsfall
K3s-Cluster ermöglichen die schnelle und Ressourcenschonen Implementeriung eines voll funktionsfähigen Kubernetes-Clusters auf einen MAC. Dadurch können einen Vielzahl von Kubernetes-Anwendungen auf dem MAC getestet werden.

### Funktionsweise
Die parametrisierten Script arbeiten mit Cononical [multipass](https://multipass/run). Dabei werden mindestens zwei virtuelle Maschinen (VMs) mit Ubuntu erzeugt, upgedated und die erforderlichen Pakete installiert. Darüber hinaus werden Verzeichnisse der VMs in lokale Verzeichnisse gemountet. Dabei wird immer die aktuelle [`Ubuntu-LTS-Version`](https://wiki.ubuntu.com/Releases) verwendet und die letzte aktuelle [`stabile Version von K3s`](https://github.com/rancher/k3s/releases). Für K3s wird aktuelle containerD als Runtime verwendet.

### Voraussetzungen and technische Anforderungen
Benötigt werden:
* Hardware: 
  * Mac mit mindestens MacOS 10.X, zwei Cores, 
  * mindestens 4GB RAM, 10 GB freie Plattenspeicher,
* Software: 
  * Canonical [`multipass`](https://multipass/run)
  * Kubernetes: [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* Internetverbindung zum Laden der Ubuntu- und K3s-Software.  
Anmerkung: Bei einer größeren Anzahl von Worker-Knoten sind entsprechend mehr Hardware (ca. 1G RAM, 3G Platte, 1 CPU je Knoten) bereitzustellen.

## Skripte und Anwendung:

### addCluster
`addCluster` erstellt k3s-Master- und -Worker-Nodes und erzeugt somit einen neuen Kubernetes-Cluster.  
```  
addCluster <Cluster-Name> <Zahl der Worker-Nodes> <Zahl der Master-Nodes>  
```
Als Cluster-Name wird dann `k3s-<Cluster-Name>` verwendet. Die Knotenbezeichnungen sind dann:  
* `k3s-<Cluster-Name>-master-0`
* `k3s-<Cluster-Name>-worker-<i>` mit `<i>=0 ... <Zahl der Worker-Nodes>`  
Hinweis: in der aktuellen Version ist nur ein Master-Node möglich (Einsatz von SQ-Lite)

### getKubeconfig
`getKubeconfig` holt die Kubeconfig-Datei `<Master-Node-Name>/etc/rancher/k3s/k3s.yaml` vom Master und  
kopiert diese mit dem Namen `.kubeconfig` in das lokale Verzeichnis.
```
getKubeconfig <Cluster-Name>
```
Anmerkung: Nach der Ausführung muss der Befehl `export KUBECONFIG=./.kubeconfig`ausgeführt werden.

### setKubeconfig
`setKubeconfig`  
```
setKubeconfig <Cluster-Name>
```

### stopCluster
`stopCluster` stoppt alle Master- und Worker-Knoten eines Clusters.
```
stopCluster <Cluster-Name>
```
### startCluster
`startCluster` startet alle Master- und Worker-Knoten eines Clusters.
```
startCluster <Cluster-Name>
```
### purgeCluster
`purgeCluster` stoppt alle Master- und Worker-Knoten eines Clusters und löscht nicht wiederherstellbar.
```
purgeCluster <Cluster-Name>
```
## Hilfreiche Befehle
`multipass list`  
`multipass info <Knoten-Name>`  
`kubectl cluster-info`  
`kubectl get nodes`  
`kubectl get pods --all-namespaces`
