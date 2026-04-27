# SSH Setup

Ce document détaille la configuration et l'utilisation du service SSH sur le serveur.

---

## Installation

SSH a été installé directement pendant l'installation du système
en cochant **Install OpenSSH server** dans l'assistant d'installation.

---

## Vérification du service

```bash
# Vérifier que SSH est actif
sudo systemctl status ssh

# Si inactif, l'activer
sudo systemctl enable --now ssh
```

---

## Connexion au serveur

Depuis une machine distante :

```bash
ssh user@192.168.30.138
```

---

## Vérifications utiles

```bash
# Vérifier le port d'écoute (22 par défaut)
sudo ss -tlnp | grep ssh

# Vérifier les logs de connexion
sudo journalctl -u ssh
```

---

## Fichier de configuration

Chemin : `/etc/ssh/sshd_config`

Paramètres par défaut utilisés :

| Paramètre | Valeur |
|---|---|
| Port | 22 |
| PermitRootLogin | no |
| PasswordAuthentication | yes |

---

## Difficultés rencontrées

Aucune difficulté particulière sur cette partie. SSH étant installé
pendant l'installation du système, le service était opérationnel dès
le premier démarrage.
