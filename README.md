# Instalação do MemSQL para RHEL 7.9

Este playbook tem como objetivo instalar e configurar o MemSQL os binários do MemSQL, Aggregators e Lefs.

Este ambiente foi testado apenas com o sistema operacional RHEL 7.9 e os binários aqui descritos.


## Binários utilizados
memsql\roles\memsql\files\memsql-server-7.3.3-df463e2f33.x86_64.rpm

memsql\roles\memsql\files\memsql-client-1.0.2-47adc5d6c9.x86_64.rpm

memsql\roles\memsql\files\memsql-toolbox-1.9.7-62a1139831.x86_64.rpm

memsql\roles\memsql\files\memsql-studio-3.2.2-a252451368.x86_64.rpm


Para executar o playbook, rode:
```bash
ansible-playbook deploy_memsql.yaml -i inventories/inventory_dev
```

Para acessar o MemSQL-Studio:
use: https://<IP-aggregator:8443 em seu browser.

## Alterar arquivo de inventário
Altere o inventário para contemplar os servidores conforme sua necessidade em:

memsql\inventories\inventory_dev

```python
[all:children]
memsql

[memsql:children]
aggregator
leaf

[aggregator]
memsql1

[leaf]
memsql2
memsql3

[multiple_leaf]

[all:vars]
ansible_connection=ssh
ansible_ssh_user="{{ vault_ssh_user }}"
ansible_ssh_pass="{{ vault_ssh_password }}"
```
### Executar playbook
```
ansible-playbook deploy_memsql.yaml -i inventories/inventory_dev
```


## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
