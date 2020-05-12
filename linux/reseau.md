# Réseau

## Socket & Ports 🔴 

Le réseau c'est le principal vecteur d'attaque sur un serveur, chaque service ouvert implique l'ouverture de port\(s\) donc on doit vérifier la liste des port ouvert dans notre system

```text
ss -lptun
```

![](../.gitbook/assets/port.png)

| Flag | Description |
| :--- | :--- |
| l | Afficher touts les sockets en écoute |
| p | Afficher le processus utilisant la socket |
| t | Afficher les sockets du protocole TCP |
| u | Afficher les sockets du protocole UDP |
| n | Afficher les ports ouvert en mode numérique |

afin de fermer un port on doit stopper son service exemple

```text
systemctl stop postfix
systemctl disable postfix ( pourdebon )
```

![](../.gitbook/assets/ip.png)

{% hint style="info" %}
Il est préférable de changer les ports par Default des service exemple **`ssh`** qui ecoute sur le port **`22`**
{% endhint %}

## TCP Wrappers 🔴 

le processus tcp wrapper \(libraire libwrap\) contiens deux fichiers **`/etc/hosts.allow`** et **`/etc/hosts.denny`**, le premiers permet l'autorisation de connexion et le dernier en refuse si une regle est cité dans les deux fichiers la propriété est attribué a **`hosts.allow`**

Pour verifier si un service peut etre compatible avec la libraire libwrap

```text
which sshd
ldd /usr/sbin/sshd | grep libwrap
```

enfin on peut par example ajouter dans le fichiers **`hosts.allow`**

**`sshd: 192.176.2.3/255.255.255.0`**

on peut refuserer toute connexion par exemple en ajoutant dans le fichiers **`hosts.deny`**

**`sshd:all`**

{% embed url="https://fr.wikibooks.org/wiki/Administration\_réseau\_sous\_Linux/TCP\_Wrapper" %}

## Firewall \(IPTABLE\) 🔴 

Pour verfier que le noyau est bien compiler pour utuliser le firewall 

```text
version=$(uname -r); grep IPTABLES /boot/config-${version}

CONFIG_IP_NF_IPTABLES=m
CONFIG_IP6_NF_IPTABLES=m
```

le \(m\) signifie module donc il faudrait mieux de recompiler le noyau afin de rendre netfilter intégré et non pas un module

Afin de voir les règle courantes:

```text
sudo iptables -L -n
```

vaudrait mieux configurer netfilter pour ne pas laisser la machine open pour tout le monde si on souhaite bien sécurise notre serveur 

Si on veut ajouter une nouvelle politique on doit l'ajouter sur le fichiers de config, puisque en ligne de commande vas etre valide jusqu'au prochain redémarrage \(a chaud\)

```text
service iptables save
```

## \* /etc/sysctl.conf

## SSH 🔴 

### Version

Vérifier qu'on la récente version du Protocol

```text
ssh -v localhost
```

### Root

Désactiver l'access avec le compte root

```text
more /etc/ssh/sshd.config | grep PermitRootLogin
```

### Port 22

Changer le port 22 afin qu'il ne sois pas connue par le public

```text
grep port /etc/ssh/sshd.config
```

### Empty Password

Empêcher la connexion sans mot de passe

```text
grep PermitEmptyPassword /etc/ssh/sshd.config
```

### Idle

Empêcher la connexion sans activité \(idle\)

```text
grep ClientAliveInterval /etc/ssh/sshd.config
```

### Autorisation 

Autoriser la connexion juste a certain utilisateur ou groupe 

```text
AllowUsers user1,user2
AllowGroups groupe1,groupe2
```

### Trace Failed Auth

Tracé les tentative de connexion échoué, par exemple âpre 2 tentative les les trace seront détaillé

```text
MaxAuthTries 2
```

### Clé

Activer l'authentification juste par clé \(public/privé\)

```text
PasswordAuthentification No
PubKeyAuthentification Yes
```

