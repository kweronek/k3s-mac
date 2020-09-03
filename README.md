# k3s-mac

### What is it?

Eine Reihe von Shell-Skripten, um auf dem Mac k3s-Cluster.

### Description

### Prerequisites and Technical Requirements

### Skripte und Anwendung:

##### addCluster

`addCluster`erstellt Master- und Worker-Nodes und erzeugt einen neuen k3s Cluster.

```addCluster <Cluster-Name> <Zahl der Worker-Nodes> <Zahl der Master-Nodes>```

Als Cluster-Name wird dann `k3s-<Cluster-Name>` verwendet. Die Knotenbezeichnungen sind dann:
k3s-<Cluster-Name>-master-0
k3s-<Cluster-Name>-worker-i mit i=0... <Zahl der Worker-Nodes>-
  
##### getKubeconfig 

##### stopCluster

##### startCluster

##### purgeCluster

### Hilfreiche Befehle
