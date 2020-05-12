# Services

## Configuration d'un service 🔴 

Lister les service activé sur le system

```text
systemctl list-units-files --type service | grep enabled
```

pour vérifier le statue d'un service

```text
systemctl status apache2.service
```

Chaque service a sa propre stratégie d’exécuter et de fonctionner donc on doit les vérifier un par un et opter pour une bonne sécurité du service 

```text
cat /etc/apache2/apache2.conf | grep [A-Z] | grep -v "#"
```

## Cloisonnement

Mettre en place des technique pour exécute des services dans un environnement d’accès aux ressource limité et contrôlé 

## Compte Service🔴 

```text
ps -edf | grep <service_name>
```

Vérifier pour chaque service le compte associé avec et donner le moindre privilège, afin d'obtenir des detailles sur un compte specifié

```text
id <compte>
grep <compte> /etc/passwd
grep <compte> /etc/group
```

{% hint style="info" %}
**Information**: les iud inférieur a 100 s'ont réserver aux compte System
{% endhint %}

## Dossier Service 🔴 

Vérifier les droit des dossier appartenant a un service example apache:

```text
chown -R www-data:www-data /var/www/html
```

```text
chmod -R 750 /var/www/html
```

## Virtualiser l'architecture Applicative d'un Service ⚫ 

il faudrait attribuer une machine et os pour chaque service mais cette méthode et impeu trop coûteuse 💸 mais heureusement il a des alternative:

* Les Conteneur \(Docker\)
* La Virtualisation
* Hyper viseur noyau \(Linux KVM\)

![](../.gitbook/assets/apache_vm.png)

## Chroot 🔴 

la technique de chroot permettant de changer le répertoire racine d'un processus de la machine hôte.

## 

