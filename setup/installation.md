# Installation – Ubuntu Server 22.04 LTS

Ce document détaille les étapes pour reproduire l'environnement du projet.

---

## 1. Création de la machine virtuelle

- Logiciel : VMware / VirtualBox
- RAM : 2 Go minimum
- Disque : 20 Go minimum
- Réseau : mode **Bridged** (pour avoir une IP sur le réseau local)
- ISO : [Ubuntu Server 22.04 LTS](https://ubuntu.com/download/server)

---

## 2. Installation du système

Lors de l'installation, configurer :

- Langue : French / English (selon préférence)
- Nom de la machine : `ubuntu-server` (ou au choix)
- Nom d'utilisateur : `user`
- Mot de passe : *(choisir un mot de passe fort)*
- Cocher **Install OpenSSH server** pendant l'installation

---

## 3. Configuration réseau (Netplan)

Identifier l'interface réseau :

```bash
ip link show
```

Éditer le fichier Netplan :

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Contenu du fichier :

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

Appliquer :

```bash
sudo netplan apply

# Vérifier
ip a
```

---

## 4. Configuration SSH

Vérifier que SSH est actif :

```bash
sudo systemctl status ssh

# Si inactif, l'activer
sudo systemctl enable --now ssh
```

Tester la connexion depuis une autre machine :

```bash
ssh user@192.168.30.138
```

---

## 5. Création d'un utilisateur secondaire

```bash
# Créer l'utilisateur
sudo adduser admin1

# Lui donner les droits sudo
sudo usermod -aG sudo admin1

# Vérifier
groups admin1
```

---

## 6. Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Vérifications finales

| Etape | Commande | Résultat attendu |
|---|---|---|
| IP statique active | `ip a` | `192.168.30.138/24` visible |
| SSH actif | `systemctl status ssh` | `active (running)` |
| Connexion distante | `ssh user@192.168.30.138` | Connexion établie |
| Utilisateur sudo | `groups admin1` | `sudo` présent |
| Système à jour | `apt list --upgradable` | Liste vide |
