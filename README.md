#  Home Lab – Serveur Linux Ubuntu Server

![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04_LTS-E95420?style=flat&logo=ubuntu&logoColor=white)
![SSH](https://img.shields.io/badge/SSH-Enabled-238636?style=flat&logo=gnubash&logoColor=white)
![CLI](https://img.shields.io/badge/Interface-CLI_Only-9e6a03?style=flat)

---

##  Objectif

Mise en place d'un serveur Linux sans interface graphique pour pratiquer l'administration système et réseau en conditions réelles : installation, configuration, accès distant et gestion des utilisateurs.

---

##  Environnement

| Élément | Détail |
|---|---|
| OS | Ubuntu Server 22.04 LTS |
| Type | Machine virtuelle |
| Interface | CLI uniquement (pas de GUI) |

---

##  Installation

Étapes réalisées après l'installation initiale du système :

- Création de l'utilisateur principal
- Activation du service SSH
- Prise en main du terminal Linux

---

##  Configuration réseau (Netplan)

Configuration d'une adresse IP statique via `/etc/netplan/*.yaml`.

>  **Note** : `gateway4` est déprécié sur les versions récentes de Netplan.  
> J'ai utilisé la syntaxe `routes:` à la place, ce qui a nécessité quelques recherches avant de trouver la bonne approche.

```yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.30.138/24
      routes:
        - to: default
          via: 192.168.30.2
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1
```

Appliquer la configuration :

```bash
sudo netplan apply
```

---

##  Accès SSH

Activation et vérification du service SSH :

```bash
# Vérifier le statut
sudo systemctl status ssh

# Connexion depuis une machine distante
ssh user@192.168.30.138
```

---

##  Gestion des utilisateurs

Création d'un utilisateur secondaire avec droits sudo :

```bash
# Créer l'utilisateur
sudo adduser admin1

# Lui accorder les droits sudo
sudo usermod -aG sudo admin1

# Vérifier les groupes
groups admin1
```

---

##  Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y
```

---

##  Compétences développées

-  **Installation d'un serveur Linux** en environnement CLI
-  **Configuration réseau** : IP statique, passerelle, DNS avec Netplan
-  **Accès SSH** : configuration, vérification et connexion distante
-  **Gestion des utilisateurs** : création de comptes et droits sudo

---

##  Difficultés rencontrées

| Problème | Solution |
|---|---|
| `gateway4` déprécié dans Netplan | Remplacé par `routes: - to: default / via: 192.168.30.2` |
| Erreurs d'adressage IP | Diagnostiquées avec `ip a` après chaque `netplan apply` |

---

##  Auteur

**Julien Azonko**  
Licence Réseaux et Systèmes d'Information

---

> 🏷️ *Tags : Linux · Ubuntu · SSH · Netplan · Sysadmin · Homelab · CLI*
