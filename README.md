# k3s-mac

## What is it?

Eine Reihe von Shell-Skripten, um auf dem Mac k3s-Cluster.

## Description

## Prerequisites and Technical Requirements

## Skripte und Anwendung:

### addCluster
`addCluster` erstellt Master- und Worker-Nodes und erzeugt einen neuen k3s Cluster.  
Syntax:  
```addCluster <*Cluster-Name*> <Zahl der Worker-Nodes> <Zahl der Master-Nodes>```

Als Cluster-Name wird dann `k3s-<Cluster-Name>` verwendet. Die Knotenbezeichnungen sind dann:  
`k3s-<Cluster-Name>-master-0`  
`k3s-<Cluster-Name>-worker-<i>` mit `<i>=0 ... <Zahl der Worker-Nodes>`
  
Hinweis: in der aktuellen Version ist nur ein Master-Node möglich (Einsatz von SQ-Lite)
### getKubeconfig
`getKubeconfig` holt die Kubeconfig-Datei `<Master-Node-Name>/etc/rancher/k3s/k3s.yaml` vom Master und  
kopiert diese mit dem Namen `.kubeconfig` in das lokale Verzeichnis  

### stopCluster
`stopCluster` stoppt alle Master- und Worker-Knoten eines Clusters.

Syntax:  
```stopCluster <Cluster-Name>```
### startCluster
`startCluster` startet alle Master- und Worker-Knoten eines Clusters.

Syntax:
```stopCluster <Cluster-Name>```
### purgeCluster
`purgeCluster` stoppt alle Master- und Worker-Knoten eines Clusters und löscht nicht wiederherstellbar.

Syntax:
```stopCluster <Cluster-Name>```

## Hilfreiche Befehle
`multipass get notes`  
`mulitpass get info <Knoten-Name>`  
