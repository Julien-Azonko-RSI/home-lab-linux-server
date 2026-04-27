# Commandes utiles

Référence des commandes utilisées tout au long du projet.

---

## Réseau

```bash
# Afficher les interfaces réseau
ip link show

# Afficher les adresses IP
ip a

# Afficher la table de routage
ip route show

# Tester la connectivité
ping -c 4 8.8.8.8

# Appliquer la configuration Netplan
sudo netplan apply
```

---

## SSH

```bash
# Vérifier le statut du service SSH
sudo systemctl status ssh

# Activer SSH au démarrage
sudo systemctl enable --now ssh

# Se connecter au serveur
ssh user@192.168.30.138

# Vérifier le port d'écoute
sudo ss -tlnp | grep ssh

# Consulter les logs SSH
sudo journalctl -u ssh
```

---

## Gestion des utilisateurs

```bash
# Créer un utilisateur
sudo adduser admin1

# Ajouter au groupe sudo
sudo usermod -aG sudo admin1

# Vérifier les groupes d'un utilisateur
groups admin1

# Lister les utilisateurs du système
cat /etc/passwd
```

---

## Système

```bash
# Mettre à jour les paquets
sudo apt update && sudo apt upgrade -y

# Vérifier l'espace disque
df -h

# Vérifier la mémoire
free -h

# Afficher les processus actifs
top

# Afficher les logs système
sudo journalctl -xe
```

---

## Fichiers de configuration

| Fichier | Description |
|---|---|
| `/etc/netplan/00-installer-config.yaml` | Configuration réseau |
| `/etc/ssh/sshd_config` | Configuration SSH |
| `/etc/passwd` | Liste des utilisateurs |
| `/etc/group` | Liste des groupes |
