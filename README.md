# Solution-vrf-lite-nat-aware-pour-isolation-complete-de-2-reseaux-avec-connectivite-internet
Projet de configuration réseau GNS-3 de 2 LAN multi-couches isolés et connéctés a internet via VRF-LITE + NAT-AWARE
# :clipboard: Structure du projet

```
DALIL/
├── CONFIG LAN1/
|   ├── AC-A1.txt
|   ├── AC-A2.txt
|   ├── DS-A1.txt
|   ├── DS-A2.txt
|   └── R2.txt
|
├── CONFIG LAN2/
|   ├── AC-B1.txt
|   ├── AC-B2.txt
|   ├── DS-B1.txt
|   ├── DS-B2.txt
|   └── R3.txt
|
├── R1.txt
|
├── SCREENSHOOT_GNS3.png
├── SCREENSHOOT_PACKET_TRACER.png
├── TEST_LAN_1.png
├── TEST_LAN_2.png
└── NOTE_IMPORTANTE.txt
```

# 🚀 PRE-REQUIS DE DEMARRAGE

- GNS3 installé (version 2.2 ou + )
- 4GB RAM Minimum, 8GB Recommandé
- IMAGE CISCO IOS (Cisco IOU L3 17.12.1 dans notre cas sinon d'autre version de routeur supportant le vrf)
- 20GB D'ESPACE LIBRE

# 📚 DOCUMENTATION PAR PARTIE

## Partie 1 - Archcitecture réseau : Disposition physique et logique
![Disposition logique sous GNS3](/IMAGE%20GNS3.png)
![Disposition physique sous packet tracer](/IMAGE%20PACKET%20TRACER.png)
### Objectif : 
Avoir une idée de la disposition logique et physique des equipements réseau

## Partie 2 - Configuration de chaque LAN
### Objectif : 
Réaliser une configuration complete des equipements de chaque LAN en procedant de la couche accès vers la couche Core
- Configuration d'interfaces
- Configuration OSPF avec authenfication MD5
- Configuration NTP pour synchronisation d'horloge
- Configuration DHCP pour attribution automatique d'addresses par VLAN
- Configuration VTP
- Configuration MST par instance de vlan
- Configuration VRRP pour redondance de passerelle
- Configuration Port Security
- Configuration BPDU guard et Port-fast
- Configuration VLAN
- Configuration des SVI

## Partie 3 - Configuration VRF-Lite
### Objectif :
Créer les Vrf sur le routeur R1 et l'implementer sur les equipements des LAN et LAN2 ainsi que sur les interfaces concernés.
- Configuration VRF dans les processus OSPF et dans les interfaces
- Configuration route statique par defaut pour chemin vers internet

## Partie 4 - Configuration du Nat-Aware
### Objectif : 
Permettre une connexion internet aux 2 VRF, assurer une translation des addresses et un chemin retour des paquets
- Configuration des ACL pour chaque VLANs
- Configuration du NAT Overload pour chaque vrf (NAT-AWARE) 

⚠️ Important : Il est préferable d'utiliser des images qui supportent bien le Nat-Aware

# 🧪 Tests et validation
Le test s'est fait pour chaque LAN comme suit : 
## LAN 1
- Test ping inter-Vlan dans le meme vrf (pc1 et pc2) : succès ✓
- Test ping extra-Vlan dans des Vrf different (pc1 et pc5) : echec 
- Test ping vers l'addresse publique 8.8.8.8 : succès ✓
- Test ping vers cisco.com : succès ✓
![Capture d'ecran du test LAN 1](/TEST%20LAN1.png)

## LAN 2
- Test ping inter-Vlan dans le meme vrf (pc5 et pc6) : succès ✓
- Test ping extra-Vlan dans des Vrf different (pc5 et pc1) : echec 
- Test ping vers l'addresse publique 8.8.8.8 : succès ✓
- Test ping vers cisco.com : succès ✓
![Capture d'ecran du test LAN 2](/TEST%20LAN2.png)
