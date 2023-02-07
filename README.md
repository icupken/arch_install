## INSTALL
```
cfdisk /dev/sdaX  (make partition for root & efi)
mkfs.fat -F 32 /dev/sdaX1  
mkfs.ext4 /dev/sdaX2  
mount /dev/sdaX2 /mnt  
  
pacstrap /mnt base linux linux-firmware linux-headers 
genfstab -U /mnt >> /mnt/etc/fstab  
arch-chroot /mnt  
  
ln -sf /usr/share/zoneinfo/Asia/Novosibirsk /etc/localtime
hwclock --systohc (sets the hardware clock)
pacman -S nano

nano /etc/locale.gen
locale-gen
nano /etc/hostname
nano /etc/hosts

passwd (set root pass)
useradd -m username (make another user)
passwd username (set that user's password)
usermod -aG wheel,audio,video,optical,storage username

pacman -S base-devel
EDITOR=nano visudo

pacman -S networkmanager
systemctl enable NetworkManager
```

## GRUB
```
pacman -S grub
pacman -S  efibootmgr dosfstools os-prober mtools 
mkdir /boot/EFI 
mount /dev/sda1 /boot/EFI
grub-install --target=x86_64-efi  --bootloader-id=grub_uefi --recheck 
grub-mkconfig -o /boot/grub/grub.cfg
```

## KEYBOARD   
```
sudo localectl --no-convert set-x11-keymap us,ru "" "" grp:alt_shift_toggle 
```
  
## XFCE4 & NVIDIA INSTALL 
```
sudo pacman -S xfce4 xfce4-goodies nvidia-dkms sddm
sudo systemctl enable sddm
``` 

## SOFT 
```
sudo pacman -S pulseaudio pavucontrol firefox telegram-desktop ntfs-3g gvfs
awesome-terminal-fonts ttf-jetbrains-mono exa bat ttf-font-awesome htop
``` 
  
## FISH  
```
sudo pacman -S fish 
fish
curl -sL https://git.io/fisher | source && fisher install jorgebucaran/fisher  
fisher install jorgebucaran/nvm.fish  
fisher install IlanCosman/tide@v5    
set -U fish_greeting  

tide configure - что бы конфигурировать тильды

echo "set PATH $PATH ~/.cargo/bin" >> ~/.config/fish/config.fish
```  
  
## YAY
```
git clone https://aur.archlinux.org/yay.git  
cd yay  
makepkg -si       
``` 

## NVIDIA CHECK 
```
lspci -k | grep -A 2 -E "(VGA|3D)"
```
