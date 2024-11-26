---
layout: post
title: KMail - Fix postgres db cluster upgrade failed error

categories: [how-to, linux]
slug: kmail-fix-postgres-cluster-upgrade-failed
---

After a recent update on Calculate Linux (Gentoo-based), KMail stopped launching and running it from the terminal showed the following error as the root cause of failure:  

```bash
Postgres db cluster upgrade failed, Akonadi will fail to start. Sorry.
```

The update process had bumped up PostgreSQL from version 16 to 17, and that’s where the problem lied. Fixing this with all the KMail data intact turned out to be a relatively simpler task.  
<!--more-->

For me, the update had removed PostgreSQL version 16, and the data migration process requires both major versions (16 and 17 in this case) to be present on the system, so the first thing to do was to install PostgreSQL 16,  

```bash
emerge -a1 =dev-db/postgresql-16.5
```

After installation was completed, the next step was to make sure that Akonadi was not running,  

```bash
akonadictl stop
```

Before starting the data migration process, I backed up the current KMail database,  

```bash
cp -R $HOME/.local/share/akonadi/db_data/ $HOME/.local/share/akonadi/db_data_16
mv $HOME/.local/share/akonadi/db_data/ $HOME/.local/share/akonadi/db_data_old
```

Then it was time to create a new database using the latest version of PostgreSQL (17 in this case),  

```bash
/usr/lib64/postgresql-17/bin/initdb --pgdata=$HOME/.local/share/akonadi/db_data --encoding=UTF-8
```

Before starting the actual upgrade, I made sure that the upgrade was safe to carry out,    

```bash
/usr/lib64/postgresql-17/bin/pg_upgrade -b /usr/lib64/postgresql-16/bin -B /usr/lib64//postgresql-17/bin -d $HOME/.local/share/akonadi/db_data_old/ -D $HOME/.local/share/akonadi/db_data --check
```

PostgreSQL didn't complain and gave me an all-green signal, so, I went ahead with the database upgrade,  

```bash
/usr/lib64/postgresql-17/bin/pg_upgrade -b /usr/lib64/postgresql-16/bin -B /usr/lib64//postgresql-17/bin -d $HOME/.local/share/akonadi/db_data_old/ -D $HOME/.local/share/akonadi/db_data
```

Finally, it was time to restart Akonadi services,  

```bash
akonadictl start &
akonadictl fsck &
```

Some house cleaning,  

```bash
rm -rf $HOME/.local/share/akonadi/db_data_16
rm -rf $HOME/.local/share/akonadi/db_data_old
```

And, Voilà! KMail was up and running again!  
One thing I'd like to mention at the end is that all the commands above should be run as a regular user and not as root or with sudo. Hopefully, someone with a similar issue will find this post useful. They might have to slightly adjust a couple of things here and there, but it shouldn't be too difficult. Fingers crossed!  

![A quilted piece depicting migrating elephants](https://raw.githubusercontent.com/hakerdefo/hakerdefo.github.io/main/assets/image/migrating_elephants.webp "A quilted piece depicting migrating elephants")  
<figcaption>Image courtesy judy_and_ed</figcaption>  
