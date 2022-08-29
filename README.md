## Setting up a PostgreSQL Lab using Vagrant and Ansible on Windows (WSL 2 with VirtualBox)

```
$ vagrant up

$ vagrant status
Current machine states:

pgsql-12                  running (virtualbox)
pgsql-13                  running (virtualbox)
pgsql-14                  running (virtualbox)

$ psql -h 192.168.56.12 -p 5432 -U postgres -c "select version();" -t
 PostgreSQL 12.12 on x86_64-pc-linux-gnu, compiled by gcc (GCC) 8.5.0 20210514 (Red Hat 8.5.0-10), 64-bit

$ psql -h 192.168.56.13 -p 5432 -U postgres -c "select version();" -t
 PostgreSQL 13.8 on x86_64-pc-linux-gnu, compiled by gcc (GCC) 8.5.0 20210514 (Red Hat 8.5.0-10), 64-bit

$ psql -h 192.168.56.14 -p 5432 -U postgres -c "select version();" -t
 PostgreSQL 14.5 on x86_64-pc-linux-gnu, compiled by gcc (GCC) 8.5.0 20210514 (Red Hat 8.5.0-10), 64-bit
```