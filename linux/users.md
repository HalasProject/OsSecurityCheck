# Users

## User & Password 🔴 

Authentication on linux is based on the **pam** module it is responsible for encrypting the password and storing it

```text
ldd /bin/passwd  | grep pam
```

passwords are encrypted and stored on shadow files

```text
more /etc/shadow
```

so we have to check that the pam module stores the passwords on the shadow file is not on passwd 🔴 

```text
grep shadow /etc/pam.d/*
```

## Strong Password ⚫ 

Should configure settings for a strong password quality

```text
more /etc/security/pwquality.conf
```

## Shell 

We check the accounts that will have a Shell at their connection

```text
cat /etc/passwd |grep -v nologin
```

![](../.gitbook/assets/shell.png)

## Password change 🔴 

We must add a rule to inform our users to change their password every 'x' days

```text
change -m 7 -M 90 -w 10
-m : duré de vie
-M: x jour
-w: message warning vant 10 jour
```

## Default value ⚫ 

Check the default password attribute values for each user:

```text
nano /etc/login.defs
```

## Setuid 🔴 

the setuid allows the user to execute and access a file with the 'sudo' to check all the files that contain the setuid

```text
find / -type f -perm /4000 -ls 2>/dev/null
```

![](../.gitbook/assets/setuid.png)

there are also setuid permissions for a group

```text
find / -type f -perm /6000 -ls 2>/dev/null
```

## Stickbit 🔴 

All users can add and modify but only root has the right to delete example the folder**`/tmp/`**

```text
find / -type d -perm -1000 -exec ls -ld {} \;
```

![](../.gitbook/assets/stickbit.png)

## Sudo 🔴 

we create a new group 'admin' and add the users concerned above as its avoids the call of Command 'sudo' by other user

```text
groupadd admin
chmod 4750 /usr/sbin/sudo
chwon root:admin /usr/bin/sudo
```

```text
ls -lrtha /usr/bin/sudo
```

## Sudoers 🔴 

In order to change the actions that the admin group will have by executing the command 'sudo'

```text
nano /etc/sudoers
```

**`%admin ALL-(ALL) ALL`**

