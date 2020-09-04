# K3s-mac
Für die Verwendung von K3s auf Linux siehe [hier](https://github.com/kweronek/k3s-linux).

## Beschreibung
Eine Reihe von Shell-Skripten, um auf dem Mac ein K3s-Cluster zur erzeugen, zu betreiben und zu löschen. K3s ist eine leichtgewichtige aber vollständige und zertifizierte Kubernetes-Distribution. Näheres siehe unter [`K3s`](https://github.com/rancher/k3s).

### Anwendungsfall
K3s-Cluster ermöglichen u.a. die schnelle und ressourcenschonende Implementeriung eines voll funktionsfähigen Kubernetes-Clusters auf einen MAC. Dadurch können einen Vielzahl von Kubernetes-Anwendungen auf dem MAC getestet werden.

### Funktionsweise
Die parametrisierten Scripte arbeiten mit Cononical [`multipass`](https://multipass/run). Dabei werden mindestens zwei virtuelle Maschinen (VMs) mit Ubuntu erzeugt, upgedated und die erforderlichen Pakete installiert. Darüber hinaus werden Verzeichnisse der VMs in lokale Verzeichnisse gemountet. Dabei wird immer die aktuelle [`Ubuntu-LTS-Version`](https://wiki.ubuntu.com/Releases) verwendet und die letzte aktuelle [`stabile Version von K3s`](https://github.com/rancher/k3s/releases). Für K3s wird aktuelle [`containerD`](https://containerd.io) als Runtime verwendet.

### Voraussetzungen and technische Anforderungen
Benötigt werden:
* Hardware: 
  * Mac mit mindestens MacOS 10.X, zwei Cores, 
  * mindestens 4GB RAM, 10 GB freier Plattenspeicher,
* Software: 
  * Canonical [`multipass`](https://multipass/run)
  * Kubernetes: [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* Internetverbindung

Anmerkung: Bei zusätzlichen Worker-Knoten sind entsprechend mehr Hardware (ca. 1G RAM, 3G Platte, 1 CPU je Knoten) bereitzustellen.

## Skripte und Anwendung

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
`getKubeconfig` holt die Kubeconfig-Datei `<Master-Node-Name>/etc/rancher/k3s/k3s.yaml` vom Master, kopiert diese nach $HOME/.kube/config (Default für Kubeconfig-Dateien). Danach wird die Master-IP-Adresse von 127.0.0.1 auf die aktuelle IP-Adresse des Master-Knoten `k3s-<Cluster-Name>-master-0` gesetzt. Dies ermöglicht den unmittelbaren Zugriff von `kubectl` auf den Cluster. 
```
getKubeconfig <Cluster-Name>
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
`kubectl cluster-info`  
`multipass info <Knoten-Name>`  
`multipass info --all`

## Beispiel
```
addCluster myCluster 3 1
multipass list
getKubeconfig myCluster
kubectl cluster-info
kubectl get nodes
kubectl get pods --all-namespaces
stopCluster myCluster
multipass list
```
