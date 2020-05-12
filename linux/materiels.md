# Matériels

## CPU Flag 🔴 

```text
dmseg | grep cpu
```

```text
more /proc/cpuinfo
```

Vérifier que le CPU dispose des flags **PAE** et **NX** 

![](../.gitbook/assets/cpu_flags.png)

{% hint style="info" %}
Pae & nx Protège l’exécution d'instruction stockée dans la région mémoire non-autorisé
{% endhint %}

{% embed url="https://superuser.com/questions/1118712/when-i-have-to-use-pae-nx" %}

## Mémoire

```text
dmesg | grep memory
```

```text
more /proc/meminfo
```

```text
vmstate -s | grep memory
```

## Swap

Une fois la memoire est saturé le System vas basculer automatiquement vers la mémoire swap donc on doit vérifier sa présence et avoir un minimum de mémoire SWAP sur notre system

```text
vmstat -s | grep swap
```

## Disque

```text
dmesg | grep disk
```

```text
lsblk
```

On doit vérifier l'aspect partitionnement du disque et identifier les défaut de partitionnement ainsi les mauvaise option de montage **\(Cette partie est avant l’installation du OS\)**

```text
sudo fdisk -l
```

Pour avoir plus de détaille sur un partitionnement

```text
blkid /dev/sda2 
```

![](../.gitbook/assets/disk_linux.png)

il existe un autre type nomé **LVM2 plus solide que celui la** 

Donc une autre remarque faudrait bien vérifier le partitionnement et l'isolation qui protège les composant du System example le dossier **/tmp**/ faudrait l'isoler 😉 

Vérifier les la liste des partition qui sont monté automatiquement au démarrage 

```text
cat /etc/fstab
```

