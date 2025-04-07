# lab3
1. Create a user account with the following attribute
   • username: “your first name”
   • Fullname/comment: “full name”
   • Password: islam
ubuntu@memorable-mite:~$ sudo useradd -m -c "nesma ibrahim" nesma
ubuntu@memorable-mite:~$ sudo passwd nesma
New password: 
Retype new password: 
passwd: password updated successfully
ubuntu@memorable-mite:~$ sudo usermod -aG sudo nesma

2. Create a user account with the following attribute
   • Username: baduser
   • Full name/comment: Bad User
   • Password: baduser
ubuntu@memorable-mite:~$ sudo useradd -m -c "Bad User" baduser
ubuntu@memorable-mite:~$ sudo passwd baduser
New password: 
Retype new password: 
passwd: password updated successfully
ubuntu@memorable-mite:~$ sudo usermod -aG sudo baduser

3. Create a supplementary (Secondary) group called pgroup with group ID of 30000
ubuntu@memorable-mite:~$ sudo groupadd -g 30000 pgroup

4. Create a supplementary group called badgroup
ubuntu@memorable-mite:~$ sudo groupadd badgroup
ubuntu@memorable-mite:~$ cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,ubuntu
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:ubuntu
floppy:x:25:
tape:x:26:
sudo:x:27:ubuntu,nesma,baduser
audio:x:29:
dip:x:30:ubuntu
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-journal:x:999:
systemd-network:x:998:
crontab:x:997:
systemd-timesync:x:996:
input:x:995:
sgx:x:994:
kvm:x:993:
render:x:992:
messagebus:x:101:
syslog:x:102:
systemd-resolve:x:991:
uuidd:x:103:
tss:x:104:
lxd:x:105:ubuntu
_ssh:x:106:
rdma:x:107:
tcpdump:x:108:
landscape:x:109:
fwupd-refresh:x:990:
polkitd:x:989:
admin:x:110:
netdev:x:111:
ubuntu:x:1000:
nesma:x:1001:
baduser:x:1002:
pgroup:x:30000:
badgroup:x:30001:
   
5. Add islam user to the pgroup group as a supplementary group
ubuntu@memorable-mite:~$ sudo usermod -aG pgroup nesma

6. Modify the password of islam's account to password
ubuntu@memorable-mite:~$ echo "nesma:password" | sudo chpasswd

7. Modify islam's account so the password expires after 30 days
ubuntu@memorable-mite:~$ sudo chage -M 30 nesma

8. Lock bad user account so he can't log in
ubuntu@memorable-mite:~$ usermod --help
Usage: usermod [options] LOGIN

Options:
  -a, --append                  append the user to the supplemental GROUPS
                                mentioned by the -G option without removing
                                the user from other groups
  -b, --badname                 allow bad names
  -c, --comment COMMENT         new value of the GECOS field
  -d, --home HOME_DIR           new home directory for the user account
  -e, --expiredate EXPIRE_DATE  set account expiration date to EXPIRE_DATE
  -f, --inactive INACTIVE       set password inactive after expiration
                                to INACTIVE
  -g, --gid GROUP               force use GROUP as new primary group
  -G, --groups GROUPS           new list of supplementary GROUPS
  -h, --help                    display this help message and exit
  -l, --login NEW_LOGIN         new value of the login name
  -L, --lock                    lock the user account
  -m, --move-home               move contents of the home directory to the
                                new location (use only with -d)
  -o, --non-unique              allow using duplicate (non-unique) UID
  -p, --password PASSWORD       use encrypted password for the new password
  -P, --prefix PREFIX_DIR       prefix directory where are located the /etc/* files
  -r, --remove                  remove the user from only the supplemental GROUPS
                                mentioned by the -G option without removing
                                the user from other groups
  -R, --root CHROOT_DIR         directory to chroot into
  -s, --shell SHELL             new login shell for the user account
  -u, --uid UID                 new UID for the user account
  -U, --unlock                  unlock the user account
  -v, --add-subuids FIRST-LAST  add range of subordinate uids
  -V, --del-subuids FIRST-LAST  remove range of subordinate uids
  -w, --add-subgids FIRST-LAST  add range of subordinate gids
  -W, --del-subgids FIRST-LAST  remove range of subordinate gids
  -Z, --selinux-user SEUSER     new SELinux user mapping for the user account

ubuntu@memorable-mite:~$ sudo usermod -L baduser

9. Delete bad user account
ubuntu@memorable-mite:~$ sudo userdel -r -f baduser

10. Delete the supplementary group called badgroup
ubuntu@memorable-mite:~$ sudo groupdel badgroup

11. Create a folder called myteam in your home directory and change its permissions to read only for the owner.
ubuntu@memorable-mite:~$ mkdir myteam
ubuntu@memorable-mite:~$ chmod 400 myteam

12. Log out and log in by another user
ubuntu@memorable-mite:~$ logout
Last login: Mon Apr  7 12:40:02 2025 from 192.168.64.1
ubuntu@memorable-mite:~$ su - nesma
Password: 
$ whoami
nesma

13. Try to access (by cd command) the folder (myteam)
$ cd myteam                  
-sh: 3: cd: can't cd to myteam
nesma is not the owner of myteam so it will be hidden for it

14. Using the command Line
    • Change the permissions of oldpasswd file to give owner read and write permissions and for group write and execute and execute only 
    for the others (using chmod in 2 different ways)
    root@memorable-mite:/home/nesma# touch oldpasswd
    root@memorable-mite:/home/nesma# chmod u=rw,g=wx,o=x oldpasswd
    root@memorable-mite:/home/nesma# chmod 631 oldpasswd
    root@memorable-mite:/home/nesma# ls -l oldpasswd
    -rw--wx--x 1 root root 10 Apr  7 13:40 oldpasswd
    
    • Change your default permissions to be as above.
    root@memorable-mite:/home/nesma# touch myfile
    root@memorable-mite:/home/nesma# chmod 631 myfile
    root@memorable-mite:/home/nesma# ls -l myfile
    -rw--wx--x 1 root root 0 Apr  7 14:29 myfile
    root@memorable-mite:/home/nesma# umask 035

    • What is the maximum permission a file can have, by default when it is just created? And what is that for directory.
    maximum permission number after creation is 666 ,and directory is 777
    
    • Change your default permissions to be no permission to everyone then create a directory and a file to verify.
    root@memorable-mite:/home/nesma# umask 0777
    root@memorable-mite:/home/nesma# touch test7
    root@memorable-mite:/home/nesma# mkdir testdir
    root@memorable-mite:/home/nesma# ls -l test7
    ---------- 1 root root 0 Apr  7 14:38 test7
    root@memorable-mite:/home/nesma# ls -ld testdir
    d--------- 2 root root 4096 Apr  7 14:38 testdir


15. Starting from your home directory, find all files that were modified in the last two day.
$ sudo su
[sudo] password for nesma: 
root@memorable-mite:/home# cd /home/nesma
root@memorable-mite:/home/nesma# find . -type f -mtime -2
./.sudo_as_admin_successful

16. Starting from /etc, find files owned by root user.
root@memorable-mite:/home/nesma# sudo find /etc -user root
/etc
/etc/profile
/etc/ethertypes
/etc/rc0.d
/etc/rc0.d/K01cryptdisks
/etc/rc0.d/K01uuidd
/etc/rc0.d/K01cryptdisks-early
/etc/rc0.d/K01iscsid
/etc/rc0.d/K01open-vm-tools
/etc/rc0.d/K01plymouth
/etc/rc0.d/K01unattended-upgrades
/etc/rc0.d/K01open-iscsi
/etc/libibverbs.d
/etc/libibverbs.d/efa.driver
/etc/libibverbs.d/cxgb4.driver
/etc/libibverbs.d/irdma.driver
/etc/libibverbs.d/mlx4.driver
/etc/libibverbs.d/ocrdma.driver
/etc/libibverbs.d/rxe.driver
/etc/libibverbs.d/erdma.driver
/etc/libibverbs.d/ipathverbs.driver
/etc/libibverbs.d/mlx5.driver
/etc/libibverbs.d/mana.driver
/etc/libibverbs.d/hfi1verbs.driver
/etc/libibverbs.d/bnxt_re.driver
/etc/libibverbs.d/qedr.driver
/etc/libibverbs.d/hns.driver
/etc/libibverbs.d/mthca.driver
/etc/libibverbs.d/vmw_pvrdma.driver
/etc/libibverbs.d/siw.driver
/etc/resolv.conf
/etc/ca-certificates
/etc/ca-certificates/update.d
/etc/gss
/etc/gss/mech.d
/etc/sgml
/etc/sgml/catalog
/etc/sgml/xml-core.cat
/etc/overlayroot.conf
/etc/sensors.d
/etc/sensors.d/.placeholder
/etc/passwd
/etc/sensors3.conf
/etc/mime.types
/etc/byobu
/etc/byobu/socketdir
/etc/byobu/backend
/etc/gnutls
...

17. Find all directories in your home directory.
ubuntu@memorable-mite:~$ find ~ -type d
/home/ubuntu
/home/ubuntu/.cache
/home/ubuntu/.ssh
/home/ubuntu/myteam

18. Write a command to search for all files on the system that, its name is ".profile".
ubuntu@memorable-mite:~$ sudo find / -type f -name ".profile"
/root/.profile
/home/ubuntu/.profile
/home/nesma/.profile
/etc/skel/.profile

19. Identify the file types of the following: /etc/passwd, /dev/pts/0, /etc, /dev/sda
ubuntu@memorable-mite:~$ file /etc/passwd /dev/pts/0 /etc /dev/sda
/etc/passwd: ASCII text
/dev/pts/0:  character special (136/0)
/etc:        directory
/dev/sda:    block special (8/0)

20. List the inode numbers of /, /etc, /etc/hosts.
ubuntu@memorable-mite:~$ ls -i / /etc /etc/hosts
43 /etc/hosts

/:
   12 bin                    1 dev    1731 lib                   11 lost+found   1736 opt       1 run                  1745 snap   1748 tmp
   13 bin.usr-is-merged     42 etc    1732 lib.usr-is-merged   1734 media           1 proc   1743 sbin                 1746 srv    1749 usr
    2 boot                1730 home   1733 lib64               1735 mnt          1738 root   1744 sbin.usr-is-merged      1 sys   80767 var

/etc:
 1632 ModemManager              286 e2scrub.conf      1469 libibverbs.d              546 pam.conf        1660 sos
 1655 PackageKit                114 ec2_version       1466 libnl-3                   547 pam.d           1409 ssh
 1043 X11                       112 environment        105 locale.alias            84945 passwd           699 ssl
  106 adduser.conf              621 ethertypes         633 locale.conf             84890 passwd-        84884 subgid
  148 alternatives             1515 fonts              110 locale.gen               1430 perl             146 subgid-
 1461 apparmor                  145 fstab              634 localtime                1587 pki            84896 subuid
 1093 apparmor.d                627 fuse.conf         1369 logcheck                 1489 plymouth         280 subuid-
 1402 apport                   1566 fwupd              571 login.defs               1598 pm               630 sudo.conf
  116 apt                       521 gai.conf           619 logrotate.conf           1630 polkit-1         631 sudo_logsrvd.conf
  111 bash.bashrc              1072 gnutls             267 logrotate.d              1658 pollinate        632 sudoers
   44 bash_completion          1463 groff              528 lsb-release               107 profile         1380 sudoers.d
 1596 bash_completion.d       84933 group             1609 lvm                        77 profile.d       1036 supercat
  520 bindresvport.blacklist    659 group-             616 machine-id                622 protocols        599 sysctl.conf
  660 binfmt.d                 1574 grub.d             641 magic                    1400 python3          600 sysctl.d
 1493 byobu                   84893 gshadow            642 magic.mime                695 python3.12      1490 sysstat
  697 ca-certificates           281 gshadow-           646 manpath.config            289 rc0.d            377 systemd
  636 ca-certificates.conf     1074 gss               1621 mdadm                     298 rc1.d            572 terminfo
 1669 cloud                     643 hdparm.conf        620 mime.types                304 rc2.d            104 timezone
  996 console-setup              75 host.conf          287 mke2fs.conf               317 rc3.d            676 tmpfiles.d
  661 credstore                 614 hostname          1064 modprobe.d                330 rc4.d           1385 ubuntu-advantage
  662 credstore.encrypted        43 hosts              628 modules                   343 rc5.d            635 ucf.conf
  282 cron.d                    655 hosts.allow        674 modules-load.d            356 rc6.d           1392 udev
  259 cron.daily                656 hosts.deny         617 mtab                      365 rcS.d           1666 udisks2
  686 cron.hourly               575 init.d           84609 multipath                 637 resolv.conf     1417 ufw
  688 cron.monthly             1496 initramfs-tools    651 multipath.conf            530 rmt             1387 update-manager
  690 cron.weekly               638 inputrc            647 nanorc                    624 rpc               90 update-motd.d
  693 cron.yearly              1048 iproute2          1635 needrestart               629 rsyslog.conf    1436 update-notifier
  615 crontab                  1406 iscsi              626 netconfig                1376 rsyslog.d        653 usb_modeswitch.conf
 1513 cryptsetup-initramfs      526 issue             1080 netplan                   650 screenrc        1729 usb_modeswitch.d
  649 crypttab                  527 issue.net         1081 network                   531 security         618 vconsole.conf
 1039 dbus-1                    663 kernel            1086 networkd-dispatcher       569 selinux         1397 vim
  144 debconf.conf             1602 landscape          108 networks                 1487 sensors.d       1437 vmware-tools
   45 debian_version          84755 ld.so.cache       1076 newt                      645 sensors3.conf    639 vtrgb
   46 default                   522 ld.so.conf         648 nftables.conf             625 services         644 wgetrc
  115 deluser.conf              523 ld.so.conf.d       288 nsswitch.conf            1433 sgml             518 xattr.conf
 1062 depmod.d                 1607 ldap               109 opt                     84891 shadow           678 xdg
 1382 dhcp                       76 legal              574 os-release                658 shadow-         1623 xml
  623 dhcpcd.conf               519 libaudit.conf      652 overlayroot.conf          657 shells           640 zsh_command_not_found
   67 dpkg                     1603 libblockdev        529 overlayroot.local.conf     86 skel

21. Copy /etc/passwd to your home directory, use the commands diff and cmp, and Edit in the file you copied, and then use these commands again, and check the output.
ubuntu@memorable-mite:~$ sudo cp /etc/passwd ~/
ubuntu@memorable-mite:~$ diff /etc/passwd ~/passwd
ubuntu@memorable-mite:~$ cmp /etc/passwd ~/passwd
ubuntu@memorable-mite:~$ nano ~/passwd
ubuntu@memorable-mite:~$ diff /etc/passwd ~/passwd
0a1
> #lalal
ubuntu@memorable-mite:~$ cmp /etc/passwd ~/passwd
/etc/passwd /home/ubuntu/passwd differ: byte 1, line 1

22. Create a symbolic link of /etc/passwd in /boot.
ubuntu@memorable-mite:~$ sudo ln -s /etc/passwd /boot/passwd_link
ubuntu@memorable-mite:~$ ls -l /boot
total 51533
-rw------- 1 root root  9081735 Mar 14 17:48 System.map-6.8.0-57-generic
-rw-r--r-- 1 root root   287562 Mar 14 17:48 config-6.8.0-57-generic
drwx------ 3 root root      512 Jan  1  1970 efi
drwxr-xr-x 6 root root     4096 Apr  3 12:57 grub
lrwxrwxrwx 1 root root       27 Apr  3 12:56 initrd.img -> initrd.img-6.8.0-57-generic
-rw-r--r-- 1 root root 28379487 Apr  3 12:56 initrd.img-6.8.0-57-generic
lrwxrwxrwx 1 root root       27 Apr  3 12:56 initrd.img.old -> initrd.img-6.8.0-57-generic
drwx------ 2 root root    16384 Apr  3 12:57 lost+found
lrwxrwxrwx 1 root root       11 Apr  7 15:14 passwd_link -> /etc/passwd
lrwxrwxrwx 1 root root       24 Apr  3 12:56 vmlinuz -> vmlinuz-6.8.0-57-generic
-rw------- 1 root root 14989704 Mar 15 12:43 vmlinuz-6.8.0-57-generic
lrwxrwxrwx 1 root root       24 Apr  3 12:56 vmlinuz.old -> vmlinuz-6.8.0-57-generic

23. Create a hard link of /etc/passwd in /boot. Could you? Why?
ubuntu@memorable-mite:~$ sudo ln /etc/passwd /boot/passwd_link
ln: failed to create hard link '/boot/passwd_link': File exists
no i can't because /etc/passwd and /boot are in two different filesystems and hard link cannot span across filesystems
