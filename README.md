# DS918-7.1_Proxmox

## VM PROXMOX 
>  Sur Proxmox Nous allons créer une machine virtuelle pour lancer Tiny core, Pour ce faire : 
- Creér une VM Sans HDD 
- Mettre la carte réseau en **Intel E1000**
- Recupérer le fichier  [tinycore-redpill.v0.4.6.img](https://github.com/pocopico/tinycore-redpill/blob/main/tinycore-redpill.v0.4.6.img.gz?raw=true)
- Transferer le fichier tinycore-redpill.v0.4.6.img  sur votre proxmox dans l'emplacement ***var/lib/vz/dump/*** avec **Filezilla**
- Sur votre proxmox dans **Shell** : monter tinycore-redpill.v0.4.6.img dans votre vm avec la commande : 

      > qm importdisk (le ID de votre VM) /var/lib/vz/dump/tinycore-redpill.v0.4.6.img local-lvm
- Puis metter le disk  en sata 0 puis confirmer 
- Demarrer  votre VM puis sur Tiny core recuperer l'adresse ip avec la commande :

      > ifconfig
  ## Tiny Core en SSH
  - Connecter vous en ssh sur tiny core avec la commande :
  
        > tc@(l'adresse ip de Tiny core)
        > Password : P@ssww0rd
        
 ## Creation du Chargeur DSM 7.1
 
  - **Important**, Pour certaines actions Vous devez Taper **y** puis la touche **Entrée** pour confirmer 
  
        > sudo su
        
        > ./rploader.sh update now
       
        > ./rploader.sh fullupgrade now

        > ./rploader.sh serialgen DS918+
        
        > ./rploader.sh satamap now
        
        > ./rploader.sh ext apollolake-7.0.1-42218 add https://raw.githubusercontent.com/pocopico/rp-ext/master/e1000/rpext-index.json
        
        > ./rploader.sh build apollolake-7.0.1-42218

        > ./rploader.sh clean now
        
        > ./rploader.sh ext apollolake-7.1.0-42661 add https://raw.githubusercontent.com/pocopico/rp-ext/master/e1000/rpext-index.json

        > ./rploader.sh build apollolake-7.1.0-42661
   
  ## Récupération du Fichier loader.img
  - le fichier **loader.img** est le fichier Contenant la compilation finale de la version **7.1** du Model **DS918+** avce le pilote **intel e1000**
  - Vous Pouvez la recupérer avec **Filezilla** ou **scp** et le mettre sur votre PC
  - L'emplacement du fichier loader
  
      > /home/tc/redpill-load
      
  - Elle vous permettra de recréer Un autre  Nas en VM sur proxmox sans refaire tout la procedure de compilation
  
  ## Action Finale Sauvegarder Votre Session sur Tiny Core 
  
  - Taper cette commande :
  
 
             > ./rploader.sh clean now;  rm -rf /mnt/sdb3/auxfiles;  rm -rf /home/tc/custom-module;  ./rploader.sh backup now;
