 ## Sources

learn.micrsoft.com AZ-900
Book Kofler second edition, pages 999-444

## AZ-900

### LP 1-3

* Describe cloud concepts

  * 3 modules gemacht: 1 Zusammengefasst.
  
* Describe Azure architectes and services (Ende Januar)

  * 1 / 4 modules
  
* Describe Azure management and governance (Mitte Februar)
  
  * 0 / 4 modules

## Definitionen

* Azure regions
  * geographische Region  
* Azure region pairs
  * benachbarte Regionen, mindestens 300 Meilen auseinander. Für Rollouts gedacht oder strukturiertes
    wieder herauffahren. Daten in selbem Rechtsraum wegen Steuer- und Datenschutzbestimmungen.
* Sovereign regions
  * Isolierte Zentren, zb. für amerikanischen Staat oder China.
* Availability zones
  * Innerhalb einer Region, treten zumindest zu dritt auf. Nicht in jeder Region vorhanden.
  * Gedacht für SQL Server, disks, virtuelle Maschinen. Wenn genutzt, sollen alle Abhängigkeiten 
    dupliziert werden.
* datacenters
  * physischer Ort

Management Infrastruktur
* resources 
  * Basisbaustein in Azure
* resource groups
  * können nicht verschachtelt werden, jede Resource gehört zu einer Gruppe.
* subscriptions
  * Grenze für Abrechnung und Zugriff
* management groups
  * Benutzt um Subscriptions zu gruppieren, ist ein Baum mit MGs oder Subscriptions als Children.

### Hierarchie einiger Begriffe

Ein Account kann mehrere Subscriptions haben, an einer Subscription sind eine oder mehrere Resource groups.
Jede Resource gehört zu genau einer Resource group. Account->Subscription->Resource group -> Resource.

[https://learn.microsoft.com/en-gb/training/wwl-azure/describe-core-architectural-components-of-azure/media/account-scope-levels-9ceb3abd.png](src: learn.microsoft.com)

### Azure Shell for Beginners

```powershell
az interactive
```

Es wird zwischen physischer und management Infrastruktur unterschieden: physisch ist gleichbedeutend mit Datacenters.
Datencenter sind ausschliesslich über Azure Regions oder Availability Zones zugänglich. Eine Region entspricht einer physischen
Region, Datencenter sind mit low-latency Netzwerk verbunden.

Eine Availability Zone ist in einer Region, falls vorhanden besteht sie mindestens aus drei Zonen, welche einander unterstützen.





