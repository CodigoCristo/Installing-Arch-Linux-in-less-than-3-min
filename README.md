## ENGLISH - Install Arch in two steps

First we must identify which is our main disk, we can see it with the following command:

`fdisk -l`

```
/dev/sdX    > disk name

/dev/sdX1   > partition name
```

Now let's run the two steps.

**Step 1**

Here you will erase all the partitions that the disk has and it will only create a partition in MBR for bios legacy

Proceed to format and mount and install the programs.

```
(echo o; echo n; echo p; echo 1; echo ""; echo "";  echo a; echo w) | fdisk /dev/sdX ; mkfs.ext4 /dev/sdX1 ;  mount /dev/sdX1  /mnt  ;  pacstrap /mnt base linux grub nano reflector python rsync neofetch networkmanager dhcpcd
```

**Step 2**

Generate `fstab` file and activate network services, generate mirrorlist then

install grub with its configuration file for later

create root password and finally reboot.

```
genfstab -U /mnt > /mnt/etc/fstab ; arch-chroot /mnt /bin/bash -c "systemctl enable --now NetworkManager dhcpcd ; reflector --verbose --latest 10 --sort rate --save /etc/pacman.d/mirrorlist ; grub-install /dev/sdX ;  grub-mkconfig -o /boot/grub/grub.cfg ;  (echo Clave123 ; echo Clave123) | passwd root " ;  reboot
```

Demonstration video: https://youtu.be/mRa-OO_3Ewo

Within the already installed system you can continue installing and modifying your ArchLinux system!




# ESPAÑOL - Instalar Arch en dos pasos

Primero debemos tener nuestro teclado en nuestro idioma bien en español o para latinoamericanos

`loadkeys es`

`loadkeys la-latin1`

Luego debemos identificar cual es nuestro disco principal, lo podemos ver con el siguiente comando:

`fdisk -l`

```
/dev/sdX    > nombre de disco

/dev/sdX1   > nombre de partición
```

Ahora ejecutemos los dos pasos.

**Paso 1**

Aquí borrará todas las particiones que tiene el disco y solo creará una partición en MBR para bios legacy

Procede a formatear y montar e instalar los programas.

```
(echo o; echo n; echo p; echo 1; echo ""; echo "";  echo a; echo w) | fdisk /dev/sdX ; mkfs.ext4 /dev/sdX1 ;  mount /dev/sdX1  /mnt  ;  pacstrap /mnt base linux grub nano reflector python rsync neofetch networkmanager dhcpcd
```

**Paso 2**

Genera el archivo `fstab` y activa servicios de red, genera lista de mirrorlist luego 

instala grub con su archivo de configuración para luego

crear la contraseña de root y finalmente reiniciar.

```
genfstab -U /mnt > /mnt/etc/fstab ; arch-chroot /mnt /bin/bash -c "systemctl enable --now NetworkManager dhcpcd ; reflector --verbose --latest 10 --sort rate --save /etc/pacman.d/mirrorlist ; grub-install /dev/sdX ;  grub-mkconfig -o /boot/grub/grub.cfg ;  (echo Clave123 ; echo Clave123) | passwd root " ;  reboot
```

Video demostrativo: https://youtu.be/mRa-OO_3Ewo

Dentro del sistema ya instalado pueden seguir instalando y modificando su sistema ArchLinux! 
