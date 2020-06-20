# Cluster Kubernetes de test avec vagrant et virtualbox


## Si nécessaire installation vagrant et vbox

```
apt-get install virtualbox
curl https://releases.hashicorp.com/vagrant/2.2.5/vagrant_2.2.5_x86_64.deb
dpkg -i vagrant_2.2.5_x86_64.deb
```


## Création

* modifiez le token dans les scripts install_node et master si vous le souhaitez

* ajoutez ou retirez des nodes si vous le souhaitez avec la variable numberSrv du Vagrantfile

* lancez le Vagrantfile en vous plaçant dans le répertoire 

```
vagrant up
```

## Clean

Pour tout nettoyer :

```
vagrant destroy
```
