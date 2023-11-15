# Cours
Script bash auto install jenkins debian 11

Télécharger Debian 11 : https://lecrabeinfo.net/telecharger/debian-11-64-bits

Voici le script expliqué, il vous suffira de un copier/coller dans un fichier sur votre debian 


#!/bin/bash

#Mettre à jour la liste des paquets
apt update -y

#Installer wget gpg et java
apt install wget gpg openjdk-11-jdk -y

#Ajouter la clé du dépôt Jenkins
wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

#Ajouter le dépôt Jenkins au système
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

#Mettre à jour à nouveau la liste des paquets
apt-get update -y

#Installer Jenkins
apt-get install jenkins

#Activer le démarrage automatique de Jenkins
service jenkins start

echo "Mot de passe d'administration Jenkins :"
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

echo "Script d'installation de Jenkins terminé."
echo "Vous pouvez accéder à Jenkins à l'adresse http://localhost:8080/"
