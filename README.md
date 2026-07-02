# TP  - Configuration OSPF Multi-Aires et Redistribution EIGRP

## 📝 Présentation

Ce projet a été réalisé dans le cadre du module **Routage et Commutation** de la Licence 3 Systèmes, Réseaux et Télécommunications.

L'objectif de ce TP est de mettre en place un réseau utilisant le protocole **OSPF** sur plusieurs aires, puis de connecter ces différentes aires à l'aide du protocole **EIGRP**. Pour permettre l'échange des routes entre les deux protocoles, une **redistribution bidirectionnelle** est configurée sur les routeurs de bordure.

L'ensemble des configurations et des tests a été réalisé avec **Cisco Packet Tracer 9.0.0**.

---

# 🎯 Objectifs

Les principaux objectifs de ce TP sont :

- Configurer un réseau OSPF Multi-Aires.
- Configurer EIGRP (AS 100) entre les routeurs de bordure.
- Mettre en place une redistribution bidirectionnelle entre OSPF et EIGRP.
- Vérifier les tables de routage et les voisinages.
- Tester la communication entre tous les réseaux.
- Comprendre le fonctionnement de la redistribution entre deux protocoles de routage.

---

# 🗺️ Topologie du réseau

Le réseau est composé de **6 routeurs Cisco** :

- **LAB_A**
- **LAB_B**
- **LAB_C**
- **LAB_D**
- **LAB_E**
- **LAB_F**

Les routeurs **LAB_A** et **LAB_B** jouent le rôle de **routeurs de bordure (ASBR)**. Ils assurent la communication entre le domaine OSPF et le domaine EIGRP grâce à la redistribution des routes.

---

# 🌐 Protocoles utilisés

## OSPF

- Process ID : **1**
- Architecture : **Multi-Aires**
- Router-ID configuré manuellement sur chaque routeur.

## EIGRP

- Autonomous System : **100**
- Utilisé entre **LAB_A** et **LAB_B**.

---

# 🔄 Redistribution des routes

Afin de permettre aux deux protocoles de partager leurs informations de routage, une redistribution bidirectionnelle est configurée sur les routeurs **LAB_A** et **LAB_B**.

## OSPF vers EIGRP

```cisco
router eigrp 100
 redistribute ospf 1 metric 10000 100 255 1 1500
```

Cette commande permet d'importer les routes OSPF dans EIGRP en leur attribuant une métrique compatible avec EIGRP.

---

## EIGRP vers OSPF

```cisco
router ospf 1
 redistribute eigrp 100 subnets
```

Cette commande permet de redistribuer les routes EIGRP dans OSPF, y compris les sous-réseaux.

---

# ✅ Vérifications réalisées

Après la configuration, plusieurs commandes Cisco ont été utilisées afin de vérifier le bon fonctionnement du réseau.

### Vérification des voisins OSPF

```bash
show ip ospf neighbor
```

### Vérification des voisins EIGRP

```bash
show ip eigrp neighbors
```

### Vérification des protocoles actifs

```bash
show ip protocols
```

### Vérification de la table de routage

```bash
show ip route
```

### Vérification du chemin emprunté

```bash
traceroute
```

Ces différentes commandes permettent de confirmer :

- l'établissement des voisinages ;
- la présence des routes apprises ;
- le bon fonctionnement de la redistribution ;
- la connectivité entre les différents réseaux.

---

# ⚠️ Difficultés rencontrées

Au cours de ce TP, plusieurs difficultés ont été rencontrées :

- compréhension du fonctionnement de la redistribution entre OSPF et EIGRP ;
- choix du meilleur chemin par les protocoles de routage ;
- interprétation des routes **D EX**, **O IA**, **O E1** et **O E2** ;
- comportement particulier observé avec Cisco Packet Tracer lors de la redistribution.

Ces difficultés ont été résolues grâce à l'analyse des tables de routage, des voisinages et des différentes commandes de diagnostic.

---

# 📁 Organisation du dépôt

```
TP-OSPF-EIGRP/
│
├── README.md
├── Rapport/
│   └── Rapport_TP.pdf
│
├── Configurations/
│   ├── LAB_A.txt
│   ├── LAB_B.txt
│   ├── LAB_C.txt
│   ├── LAB_D.txt
│   ├── LAB_E.txt
│   └── LAB_F.txt
│
├── Images/
│   ├── Topologie.png
│   ├── OSPF_Neighbors.png
│   ├── EIGRP_Neighbors.png
│   ├── Routing_Table.png
│   └── Traceroute.png
│
└── packet-tracer/
    └── TP_OSPF_EIGRP.pkt
```

---

# 🛠️ Outils utilisés

- Cisco Packet Tracer 9.0.0
- Cisco IOS
- Git
- GitHub

---

# 📚 Compétences acquises

À travers ce TP, j'ai appris à :

- configurer un réseau OSPF Multi-Aires ;
- configurer EIGRP ;
- mettre en place une redistribution entre deux protocoles de routage ;
- analyser une table de routage Cisco ;
- utiliser les principales commandes de diagnostic réseau ;
- identifier et résoudre des problèmes de routage.

---

# 📌 Conclusion

Ce TP m'a permis de mieux comprendre le fonctionnement des protocoles de routage dynamique OSPF et EIGRP ainsi que la redistribution des routes entre ces deux protocoles. Il m'a également permis de renforcer mes compétences en configuration Cisco et en analyse des tables de routage.

---

# 👨‍💻 Auteur

**Abdoulaye Diallo**

Étudiant en Licence 3 Systèmes, Réseaux et Télécommunications

Université Alioune Diop de Bambey (UADB)

Sénégal 🇸🇳
