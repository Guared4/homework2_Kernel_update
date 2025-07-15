Версия ядра до обновления:    
vagrant@kernel-update:~$ uname -mrs    
Linux 5.15.0-116-generic x86_64    

Обновление ядра    
__________________________________
1. Выполнил команду загрузки последней версии ядра с сайта www.kernel.org     
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.11.tar.xz     
"Saving to: ‘linux-6.11.tar.xz’     

linux-6.11.tar.xz                                  100%  [===============================================================================================================>] 140,09M  1,76MB/s    in 81s     

2024-09-24 11:45:25 (1,74 MB/s) - ‘linux-6.11.tar.xz’ saved [146900704/146900704]"     
___________________________________
2. Извлек исходный код командой:    
 tar xvf linux-6.11.tar.xz     
 ___________________________________
3. Установил необходимые пакеты:    
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison     
___________________________________
4. Выполнил настройку ядра

cd linux-6.11    
cp -v /boot/config-$(uname -r) .config    
make defconfig     
"*** Default configuration is based on 'x86_64_defconfig'     
#    
 configuration written to .config     
#         
___________________________________
5. Выполнил сборку ядра:    
make     
make modules_install     
make install     
___________________________________
6. Обновил загрузчик:    
update-initramfs -c -k 6.11    
update-grub     
___________________________________
7. Выполнил перезагрузку ОС и проверил версию ядра:     
uname -mrs     

root@guared:/home/guared# uname -mrs     
Linux 6.11.0 x86_64     
___________________________________
end
