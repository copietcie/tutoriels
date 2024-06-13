# Installation de Vagrant

## Etape 1
Activer d'abord le sous systeme Linux pour Windows : Panneau de configuration > Activer ou désactiver des fonctionnalités Windows > Faire suivant jusqu'à arriver dans Fonctionnalité et cocher "Windows subsystem for Linux". 

Redémarrer si nécessaire puis lancer cette commande pour installer une distribution Linux (ici Debian) : 
```
wsl --install -d Debian
```
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/5b97ce96-d59a-4755-b8e1-36dbd6df8c1c)
S'il faut effectuer une mise à jour de WSL : 
```
wsl --update
```
Il faut redémarrer le serveur.
```
shutdown /r /t 00
```
Au redémarrage ça va télécharger la distribution et demande un nom d'utilisateur et un mot de passe : 
![image](https://github.com/kawaiiineko-website/tutoriels/assets/118014015/81067102-5d37-4105-b9b5-732744eeaf9a)

Pour désinstaller la distribution Linux : 
```
wsl --unregister Debian
```
Lancer le sous système et installer les paquets Ansible et Python3 (pas obligé d'être en root): 
```
wsl
sudo apt update && sudo apt install virtualbox ansible python3-pip
```

On récupère le dépôt de Vagrant et sa clé et on installe le paquet : 
```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant
```
Mettre les variables d'environnement : 
```
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
export PATH="$PATH:/mnt/c/Program Files/Hyper-V"
```

Installer une bibliothèque Python "pywinrm"
```
python3 -m pip install pywinrm
```
Installer les plugins Vagrant : 
```
vagrant plugin install winrm 
vagrant plugin install winrm-elevated 
vagrant plugin install winrm-fs
```
=> ça permet de se connecter à une VM et à faire des configurations dedans

Installation de plugin Ansible : 
```
ansible-galaxy collection install community.windows 
ansible-galaxy collection install ansible.windows
```

Faire une arborescence et créer un Vagrantfile : 
```
nano Vagrantfile
```

Pour un Vagrantfile de Debian : 
```
Vagrant.configure("2") do |config|
   config.vm.box = "generic/debian10"
   config.vm.provider "hyperv" do |hv|
config.vm.synced_folder ".", "/vagrant", disabled: true
      hv.cpus = "2"
      hv.memory = "2048"
      hv.linked_clone = true
   end

   config.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbook-ansible.yml"
   end
end
```

