# Logs

{% hint style="info" %}
 **Syslog** c'est le protocole qui gére les journaux d'événements d'un système informatique
{% endhint %}

## Permission ⚫ 

the log files are generally located in the **`/var/log`** folder, we must check the permission settings of the latter and try to separate it in a single partition

## Rotation ⚫ 

We must activate the rotation system which will prevent saturation of log files

```text
more /etc/logrotate.conf
```

## Distance ⚫ 

externalize the trace files in order to write the logs in a remote file using TCP / UDP

```text
more /etc/rsyslog.conf
```

## Monitor log files 🔴 

We will have to check all the alerts coming from our log files and stay up to date in order to avoid any type of attack, so for that we have to configure or install a log file supervisor in order to receive emails for example **logwatch, nagiox**

{% embed url="https://doc.ubuntu-fr.org/logwatch" %}

