# Services

## Service configuration 🔴 

List the activated service on the system

```text
systemctl list-units-files --type service | grep enabled
```

to check the status of a service

```text
systemctl status apache2.service
```

Each service has its own strategy to run and operate so we have to check them one by one and opt for good security of the service

```text
cat /etc/apache2/apache2.conf | grep [A-Z] | grep -v "#"
```

## Partitioning

Set up techniques to execute services in a limited and controlled resource access environment

## Service Account🔴 

```text
ps -edf | grep <service_name>
```

Check for each service the account associated with and give the slightest privilege, in order to obtain details on a specified account

```text
id <compte>
grep <compte> /etc/passwd
grep <compte> /etc/group
```

{% hint style="info" %}
Information: uid less than 100 are reserved for System accounts
{% endhint %}

## Service File 🔴 

Check the rights of files belonging to an apache example service:

```text
chown -R www-data:www-data /var/www/html
```

```text
chmod -R 750 /var/www/html
```

## Virtualize the Application Architecture of a Service ⚫ 

a machine and bone should be allocated for each service but this method are too expensive 💸 but luckily there are alternatives:

* Containers \(Docker\)
* Virtualization
* Kernel hypervisor \(Linux KVM\)

![](../.gitbook/assets/apache_vm.png)

## Chroot 🔴 

The chroot technique used to change the root directory of a process on the host machine.

## 

