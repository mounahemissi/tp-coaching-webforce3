# tp-coaching-webforce3
Instruction pour la session de coaching
# Exercice 1  - Scrum 
Préparer le dashboard Scrum pour ce projet
Projet -> New Projet -> choisir le modéle
-> Créer la liste des tâches à effectuer
 -> Faire un screenshot
# Exercice 2  - Linux 
Mettre à jour les packages de votre VM ubuntu:
`sudo apt-get update`
`sudo apt-get upgrade`

Vérifier la version de python3 déjà installée:
`python3 --version`

créer un alias nommé python valide pour le user ubuntu de votre VM:

ouvrir le fichier .bashrc par la commande : `sudo nano ./bashrc` et j'ajoute la ligne suivant `alias python='python3'`
vérifier en faisant  `python -V`
 installation flask:
 on installe pip avec la commande suivante: 
 `sudo apt intsall pip`
 Vérifier si pip est bien installé on tape la commande :

`pip --version` 
Installer Flask:
 `pip install flask`
 Vérifier si flask est bien installé on tape la commande :
 `flask --version`
 # Exercice 3  - Storage 
 
 Recherche le disque supplémentaire de 1Gb connecté à la VM:
 
 `sudo fdisk -l` le disque est: /dev/vdc
 
 
 
 Formattez ce disque au format ext4:
 `mkfs -t ext4 /dev/vdc`
 
 Monter (mount) ce disque sur le point montage /home/ubuntu/tp-coaching-webforce3/log:
 créer le dossier de montage:
 
 `mkdir /home/ubuntu/tp-coaching-webforce3/log`
 
 Monter le disque:
 `sudo mount /dev/vdc/ /home/ubuntu/tp-coaching-webforce3/log`
 
# Exercice 4  - Git/Github 
Dans PyCharm allez dans File->Settings->Version control->github 
![Capture d’écran 2023-03-03 à 15 42 02](https://user-images.githubusercontent.com/122799093/222749650-389d2277-8afd-497c-ad03-3ae05092541a.png)
 
 Vous pouvez maintenant faire des git commit et git push depuis PyCharm:
 `git init`
 `git config --global user.email "sirinarymen@gmail.com"
 `git config --global user.name "mounahemissi"
 `git pull`
 `git commit`
 
 # Exercice 5  - Python
 Créez un fichier blogs.py :
 `nano blogs.py`
 mettre des commentaires 
 
 ```python
 
from flask import Flask
import logging
 # create the app
 # app est une application Flask 
 app = Flask(__name__)
 #effecture la configuration de base du système du journalisation dans la fiche "log/record.log" logging.basicConfig(filename='log/record.log', level=logging.DEBUG, format=f'%(asctime)s %(levelname)s %(name)s %(threadName)s : %(message)s')
  # application route, décorateur pour lier une fonction à une URL@app.route('/blogs')
def blog():
    app.logger.info('Info level log')
    app.logger.warning('Warning level log')
    return f"Welcome to the Blog"
  #l'exectuion de l'application en localhostapp.run(host='localhost', debug=True)
``` 
 Ajouter une variable d'environnement FLASK_APP=blogs:
 
 dans le fichier .bashrc on ajoute cette ligne èxport FLASK_APP=blogs.py`
 
 Lancer le web server avec la commande ```flask run --host=0.0.0.0 -p 30101```  
 ![Capture d’écran 2023-03-03 à 16 02 56](https://user-images.githubusercontent.com/122799093/222754171-d833b897-cc6b-4d4f-adaf-3908fd8df974.png)

Vérifier avec votre navigateur en utilisant l'url `http://<ip_de_votre_vm>:30101/blogs`
![Capture d’écran 2023-03-03 à 16 06 29](https://user-images.githubusercontent.com/122799093/222755022-1b190b87-cebd-40b6-9a8b-feb6745239c9.png)
# Exercice 6  - Pare-feu
trouvez la commande de gestion du firewall sous ubuntu 20.04:
`sudo ufw`
Fermer le port 5000
  `sudo ufw deny 5000`
  
Autoriser le port 30101
  `sudo ufw allow 30101`
  
  
 ## TP ansible 1 
 Nous allons créer un virtualenv python pour installer la derniere version 
d'Ansible: on tape les commandes suivants:
`sh connect.sh`

`cd ~/tp-coaching-webforce3`

`python3 -m venv venv`  

`source venv/bin/activate`  
`pip3 install wheel`  
`pip3 install --upgrade pip` 

`pip3 install ansible`

`pip3 install requests` 

`pip3 install natsort` 

`ansible --version` 

Créer un fichier ansible-1.yaml qui automatise l'exercice 2 ci-dessus:
1. Le script doit mettre à jour les packages ubuntu. 

fichier ansible-1.yaml
on tape la commande:
`vi ansible-1.yml` 

` ---
- name: Mise à jour des packages et installation de Python 3
  hosts: vm_ubuntu # remplacez par le nom de votre machine virtuelle Ubuntu
  become: yes

  tasks:
  - name: Mettre à jour les packages
    apt:
      update_cache: yes
      upgrade: dist

  - name: Vérifier la version de Python 3
    command: python3 --version
    register: python_version
    changed_when: false

  - name: Créer un alias pour Python
    shell: echo "alias python=python3" >> /home/ubuntu/.bashrc
    args:
      creates: /home/ubuntu/.bashrc
    become_user: ubuntu

  - name: Vérifier l'alias Python
    shell: source /home/ubuntu/.bashrc && python --version
    register: python_alias
    changed_when: false

  - name: Installer pip
    when: python_version.stdout.find("Python 3") != -1
    become: yes
    apt:
      name: python3-pip
      state: present

  - name: Installer Flask
    pip:
      name: flask
      executable: pip3
      state: present
    become: yes
    when: python_alias.stdout.find("Python 3") != -1`
    
    
2. Vérifier la version de python3 :
on tape la commande:
  `python3 --version` 
 3. Créer un alias dans ~/.bashrc :
  `echo "aliaspython= python3" /home/ubuntu/.bashrc`
4. installer le package pip:
`python get-pip.py`
## TP ansible 2 
