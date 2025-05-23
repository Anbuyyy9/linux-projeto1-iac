# Projeto Linux - IAC (Infraestrutura como Código)

Este projeto contém scripts **bash** para automatizar a criação de usuários, grupos e diretórios em um sistema Linux, aplicando boas práticas de permissão e organização de acessos.

---

## Descrição dos Scripts

### 1. `criar_user.sh`

Script para criar usuários convidados (`guest10` a `guest13`), com senha padrão, shell bash e com senha expirada para forçar a troca no primeiro login.

```bash
#!/bin/bash

echo "Criando usuários do sistema...."

useradd guest10 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest10 -e

useradd guest11 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest11 -e

useradd guest12 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest12 -e

useradd guest13 -c "Usuário convidado" -s /bin/bash -m -p $(openssl passwd -crypt Senha123)
passwd guest13 -e

echo "Finalizado!!"


----------------------------------------------------------------------------------------------------------------------------------------

#!/bin/bash

echo "Criando diretórios..."

mkdir /publico
mkdir /adm
mkdir /ven
mkdir /sec

echo "Criando grupos de usuários..."

groupadd GRP_ADM
groupadd GRP_VEN
groupadd GRP_SEC

echo "Criando usuários..."

useradd carlos -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd maria -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd joao -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM

useradd debora -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN
useradd sebastiana -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN
useradd roberto -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN

useradd josefina -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd amanda -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd rogerio -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC

echo "Especificando permissões dos diretórios...."

chown root:GRP_ADM /adm
chown root:GRP_VEN /ven
chown root:GRP_SEC /sec

chmod 770 /adm
chmod 770 /ven
chmod 770 /sec
chmod 777 /publico

echo "Fim....."

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

      Como executar

1.Dê permissão de execução para os scripts:
  chmod +x criar_user.sh iac1.sh

2.Execute os scripts como root ou usando sudo:
  sudo ./criar_user.sh
  sudo ./iac1.sh

Considerações
As senhas padrão definidas são Senha123 e as contas terão senha expirada para forçar a troca no primeiro login.

Os diretórios possuem permissões específicas para garantir a segurança e organização do sistema:

/adm, /ven e /sec são acessados somente pelos respectivos grupos.

/publico é aberto para todos.

Pode ser adaptado para provisionamento rápido de ambientes Linux em projetos de infraestrutura.



