# WebAppExemple

## Platforme
https://docker.labs.eazytraining.fr/
login: devops
password: devops

## Création et installation
NEW INSTANCE of eazytraining/ansible
```cmd
sudo su admin
cd
git clone https://github.com/Chatbrume/WebAppExemple.git
```

NEW INSTANCE of eazytraining/client
```cmd
sudo su admin
cd
```

## build
Sur l'instance eazytraining/ansible

Modif de l'adresse ip
```cmd
vi prod.yml
```
Remplacer "10.0.7.4" par le numéro du eazytraining/client

Rappel commande vi:
Insert: taper sur la lettre i
Sauvegarder et quittez le fichier:
1) taper sur la touche echap
2) ecriver :wq
3) taper sur entrée

Installation du module ansible-lint
```cmd
sudo yum install ansible-lint
```

code:
```cmd
ansible-lint deploy.yml
```
resultat:
```cmd
[301] Commands should not change things if nothing needs doing
deploy.yml:22
Task/Handler: install python-pip

[401] Git checkouts must contain explicit version
deploy.yml:32
Task/Handler: git clone webserver files
```

code:
```cmd
ansible-playbook -i prod.yml deploy.yml
```
resultat:
```cmd

PLAY [Deploy an Container] *****************************************************

TASK [Gathering Facts] *********************************************************
ok: [client]

TASK [install dependencies] ****************************************************
ok: [client]

TASK [install dependencies] ****************************************************
ok: [client]

TASK [download Python-pip for docker module] ***********************************
ok: [client]

TASK [install python-pip] ******************************************************
changed: [client]

TASK [Install docker python] ***************************************************
changed: [client]

TASK [create WebAppExemple directory] ******************************************
changed: [client]

TASK [git clone webserver files] ***********************************************
changed: [client]

TASK [launch docker container"] ************************************************
changed: [client]

PLAY RECAP *********************************************************************
client                     : ok=9    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## resultat
Sur l'instance eazytraining/client

Ouvrir le port 80

Pour ce point générer le clé ssh sur le admin 
avec le
ssh-keygen -t rsa

et après le copier sur le client 

ssh-copy-id admin@IP
