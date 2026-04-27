# Home Lab – Linux Server (Ubuntu Server)

## Objectif

Dans ce projet, j’ai mis en place un serveur Linux sans interface graphique pour m’entraîner à l’administration système et réseau. L’idée était de comprendre concrètement comment installer un serveur, le configurer et pouvoir y accéder à distance.

## Environnement

J’ai travaillé sur une machine virtuelle avec Ubuntu Server 22.04 LTS, uniquement en ligne de commande.

## Installation

J’ai installé le système puis configuré les éléments de base :

* création de l’utilisateur principal
* activation du service SSH
* première prise en main du terminal

## Configuration réseau

J’ai configuré une adresse IP statique avec Netplan :

* IP : 192.168.30.138/24
* Passerelle : 192.168.30.1
* DNS : 8.8.8.8 et 1.1.1.1

Ça m’a permis de comprendre comment fonctionne un réseau local côté serveur.

## Accès SSH

J’ai activé SSH pour pouvoir me connecter au serveur à distance :

```
ssh user@192.168.30.138
```

J’ai aussi vérifié que le service fonctionne correctement avec systemctl.

## Gestion des utilisateurs

J’ai créé un utilisateur secondaire et lui ai donné les droits sudo pour simuler une gestion d’accès classique :

```
sudo adduser admin1
sudo usermod -aG sudo admin1
```

## Mise à jour du système

J’ai mis à jour le serveur avec :

```
sudo apt update && sudo apt upgrade -y
```

## Ce que j’ai appris

Ce projet m’a permis de mieux comprendre :

* l’installation d’un serveur Linux
* la configuration réseau (IP, gateway, DNS)
* l’accès distant avec SSH
* la gestion des utilisateurs

## Difficultés rencontrées

Au début, j’ai eu un peu de mal avec :

* la configuration Netplan
* le choix de la bonne interface réseau
* les erreurs de configuration IP

Mais après quelques tests, tout a fonctionné correctement.

## Auteur

Julien Azonko
Licence Réseaux et Systèmes d’Information
