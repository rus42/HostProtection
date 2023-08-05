Защита хоста. Васёв А.В.

## Задание 1

    Установите eCryptfs.
    Добавьте пользователя cryptouser.
    Зашифруйте домашний каталог пользователя с помощью eCryptfs.


Для выполнения данного задания выполнены следующие действия:

1. Выполнена установка 

```java
$ sudo apt install ecryptfs-utils cryptsetup
```

2. Создан дополнительный пользователь crypt с правами администратора, так как зашифровать домашний каталог пользователя, под которым выполнен вход, невозможно.

3. Выполнен вход от имени пользователя crypt.

4. Выполнено шифрование домашнего каталога пользователя netology

```java
$ sudo ecryptfs-migrate-home -u netology
```

5. В результате видим, что каталог пользователя /home/netology зашфирован. Также в процессе шифрования была создана копия каталога пользователя /home/netology.
На скрине ниже видно, что при просмотре содержимого каталога /home/netology пользователем crypt информация в данном каталоге зашифрована. В папке копии /home/netology данные в первичном виде. При входе в систему под пользователем netology данные в домашнем каталоге расшифровываются.

![alt text](https://github.com/rus42/HostProtection/blob/main/Task_1.png)

## Задание 2

    Установите поддержку LUKS.
    Создайте небольшой раздел, например, 100 Мб.
    Зашифруйте созданный раздел с помощью LUKS.

Для работы с LUKS и модулем dm-crypt используется утилита Cryptsetup

1. Выполнена установка 

```java
$ sudo apt install cryptsetup
```

2. После подключения дополнительного диска инициализируем и шифруем раздел /dev/sdb

```java
$ sudo cryptsetup luksFormat /dev/sdb
```

3. Расшифровываем подключенный диск

$ sudo cryptsetup luksOpen /dev/sdb crypt

![alt text](https://github.com/rus42/HostProtection/blob/main/Task_2.1.png)

4. Просматриваем информацию о подключенном диске

![alt text](https://github.com/rus42/HostProtection/blob/main/Task_2.2.png)

5. Создаем раздел EXT4

```java
$ sudo mkfs.ext4 /dev/mapper/crypt
```

6. Монтируем диск

```java
$ sudo mkdir /mnt/crypt
$ sudo mount /dev/mapper/crypt /mnt/crypt
```
