# DS918-7.1_Proxmox
## VM PROXMOX 
>  Sur Proxmox Nous allons créer une machine virtuelle pour lancer Tiny core, Pour ce faire : 
- Creér une VM Sans HDD 
- Mettre la carte réseau en Intel E1000
- Recupérer le fichier  [tinycore-redpill.v0.4.6.img](https://github.com/pocopico/tinycore-redpill/blob/main/tinycore-redpill.v0.4.6.img.gz?raw=true)
- Transferer le fichier tinycore-redpill.v0.4.6.img  sur votre proxmox dans l'emplacement ***var/lib/vz/dump/*** avec **Filezilla**
- Sur votre proxmox dans **Shell** : monter tinycore-redpill.v0.4.6.img dans votre vm avec la commande : 

      > qm importdisk (le ID de votre VM) /var/lib/vz/dump/tinycore-redpill.v0.4.6.img local-lvm
- metter le disk  en sata 0 puis confirmer 
- Demarrer  votre VM puis sur Tiny core recuperer l'adresse ip avec la commande :

      > ifconfig
  ## Tiny Core en SSH
  - Connecter vous en ssh sur tiny core avec la commande :
  
        > tc@(l'adresse ip de Tiny core)
        > Password : P@ssww0rd
