# Install Openserach

```shell
$ ansible-playbook opensearch_install.yml -i inventorys/dev
```


# Install Redis-Sentinel

```shell
Отключить transparent_hugepage - отключение прозрачных страниц стандарт 4кб делать больше размер
Увеличить числ о открытых файлов /proc/sys/fs/file-max всем пользователям
Увеличить количество соединений к сокету net.core.somaxconn
Уменьшить vm.swappines сброс грязных страниц на диск либо 1 либо 0 чтобы свода не было 

Установить vm.overcommit_memory=1
```

```shell
$ ansible-playbook redis_sentinel_install.yml -i inventorys/dev -l redis-sentinel-group
$ ansible-playbook redis_exporter_install.yml -i inventorys/dev -l redis-sentinel-group
$ ansible-playbook fluent_bit_install.yml -i inventorys/dev -l redis-sentinel-group
```