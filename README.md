# Vrf-lite-nat-aware_for_Network_Isolation_and_Internet_Connectivity
Ce projet réseau concus sur GNS-3 est un exemple d'utilisation d'un cas ou il y'a lieu d'isoler completement 2 réseaux tout en assurant une connectivité internet ceci a travers le VRF-lite et le NAT-Aware. 2 technologies qui permettent a la fois de rendre transparent le traffic d'un réseau et d'assurer une translation d'addresse efficace pour la connectivité internet.
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
├── IMAGE GNS3.png
├── IMAGE PACKET TRACER.png
├── Screen route globale R1.png
├── Screen route VRF LAN1.png
├── Screen route VRF LAN2.png
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
- Configuration Port Security
- Configuration BPDU guard et Port-fast
- Configuration VLAN
- Configuration des SVI
- Configuration VTP
- Configuration VRRP pour redondance de passerelle
- Configuration MST par instance de vlan
- Configuration NTP pour synchronisation d'horloge
- Configuration DHCP pour attribution automatique d'addresses par VLAN
- Configuration OSPF avec authenfication MD5


## Partie 3 - Configuration VRF-Lite
### Objectif :
Créer les Vrf sur le routeur R1 et l'implementer sur les equipements des LAN1 et LAN2 ainsi que sur les interfaces concernés.
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
## R1
Il s'agit ici de verifier que le routeur R1 a bien distingué après configuration les routes globales des routes VRF LAN1 et LAN2

![](/Screen%20route%20globale%20R1.png)

![](/Screen%20route%20VRF%20LAN1.png)

![](/Screen%20route%20VRF%20LAN2.png)

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
