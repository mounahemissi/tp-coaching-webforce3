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
  
