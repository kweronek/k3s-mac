# k3s-mac

## Beschreibung
Eine Reihe von Shell-Skripten, um auf dem Mac ein k3s-Cluster zur erzeugen, zu betreiben und zu löschen. k3s ist eine leichtgewichtige aber vollständige und zertifizierte Kubernetes-Distribution. Näheres siehe unter `[k3s](https://github.com/rancher/k3s)

### Anwendungsfall
k3s-Cluster ermöglichen die schnelle und Ressourcenschonen Implementeriung eines voll funktionsfähigen Kubernetes-Clusters auf einen MAC. Dadurch können einen Vielzahl von Kubernetes-Anwendungen auf dem MAC getestet werden.

### Funktionsweise
Die parametrisierten Script arbeiten mit Cononical [multipass](https://multipass/run). Dabei werden mindestens zwei virtuelle Maschinen (VMs) mit Ubuntu erzeugt, upgedated und die erforderlichen Pakete installiert. Darüber hinaus werden Verzeichnisse der VMs in lokale Verzeichnisse gemountet.

### Voraussetzungen and technische Anforderungen
Benötigt werden:
* Hardware: Mac mit mindestens MacOS 10.X, zwei Cores, minimal  4GB RAM, minimal 10 GB Plattenspeicher,
* Software: Canonical multipass, kubectl
* Internetverbindung zum Laden der Ubuntu- und k3s-Software.
Anmerkung: Bei einer größeren Anzahl von Worker-Knoten sind entsprechend mehr Hardware bereitzustellen.

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
stopCluster <Cluster-Name>
```
### purgeCluster
`purgeCluster` stoppt alle Master- und Worker-Knoten eines Clusters und löscht nicht wiederherstellbar.
```
stopCluster <Cluster-Name>
```
## Hilfreiche Befehle
`multipass list`  
`mulitpass info <Knoten-Name>`  
