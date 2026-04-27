# Configuration réseau

Ce document détaille la configuration réseau mise en place sur le serveur.

---

## Interface réseau

L'interface réseau utilisée a été identifiée avec la commande suivante :

```bash
ip link show
```

Interface détectée : `ens33`

---

## Adressage IP statique

Le DHCP a été désactivé afin d'attribuer une adresse IP fixe au serveur,
garantissant une connexion SSH stable et prévisible.

| Paramètre | Valeur |
|---|---|
| Adresse IP | 192.168.30.138 |
| Masque | /24 (255.255.255.0) |
| Passerelle | 192.168.30.2 |
| DNS primaire | 8.8.8.8 |
| DNS secondaire | 1.1.1.1 |

---

## Fichier Netplan

Chemin : `/etc/netplan/00-installer-config.yaml`

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

---

## Application de la configuration

```bash
sudo netplan apply
```

Vérification :

```bash
# Vérifier l'adresse IP attribuée
ip a

# Vérifier la passerelle
ip route show

# Tester la connectivité
ping -c 4 8.8.8.8
```

---

## Difficultés rencontrées

| Problème | Solution |
|---|---|
| `gateway4` déprécié dans Netplan | Remplacé par `routes: - to: default / via: 192.168.30.2` |
| Erreurs d'adressage IP | Diagnostiquées avec `ip a` après chaque `netplan apply` |
