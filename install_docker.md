# Docker

## Installer Docker
Mettez à jour votre liste de packages existante :

```
sudo apt update
```

Ensuite, installez quelques packages prérequis qui permettent aptd'utiliser des packages via HTTPS :

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

Ajoutez ensuite la clé GPG du référentiel Docker officiel à votre système :

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Ajoutez le dépôt Docker aux sources APT :

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Mettez à nouveau à jour votre liste de packages existante pour que l'ajout soit reconnu :

```
sudo apt update
```

Assurez-vous que vous êtes sur le point d'installer à partir du dépôt Docker au lieu du dépôt Ubuntu par défaut :

```
apt-cache policy docker-ce
```

Enfin, installez Docker :

```
sudo apt install docker-ce
```

Docker doit maintenant être installé, le démon démarré et le processus activé pour démarrer au démarrage. Vérifiez qu'il fonctionne :

```
sudo systemctl status docker
```

## Exécution de la commande Docker sans Sudo
Si vous souhaitez éviter de taper sudoà chaque fois que vous exécutez la dockercommande, ajoutez votre nom d'utilisateur au dockergroupe :

```
sudo usermod -aG docker ${USER}
```

Pour appliquer la nouvelle appartenance au groupe, déconnectez-vous du serveur et reconnectez-vous, ou saisissez ce qui suit :

```
su - ${USER}
```

```
sudo usermod -aG docker username
```

Redemarrer la machine Virtuel

## Installer Docker-compose

```
sudo apt install docker-compose
```