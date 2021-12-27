# Configurando o Bind9

> O Bind9 é um sistema de DNS flexivel e de fácil implementação que será a base para a configuração do sistema de nomes usado na nossa máquina que posteriormente será usado para fazer a ligação do cliente externo ao servidor samba

Antes de usarmos o Bind9 precisamos fazer a instalação do pacote

## Instalação
```shell
$ sudo apt update
$ sudo apt install sudo apt-get install bind9 dnsutils bind9-doc
```
![install bind9](images/dns/1.png)

> Após a instalação do bind9 podemos verificar o staus do serviço usando o comando

```shell
$ sudo systemctl status bind9
```
![install bind9](images/dns/3.png)

Agora com o bind9 configurado, precisamos configuarar as zonas que serão utilizadas no nosso "sistema de diretórios customizados" dentro do dns via bind9.

* primeiro criamos a pasta onde serão armazenadas as zonas, usando o comando
```shell
$ sudo mkdir /etc/bind/zones
```
* agora precisamos configurar as zonas dentro do diretório
  ```shell
  $ sudo cp /etc/bind/db.empty /etc/bind/zones/db.jonathanmarcos924.labredes.ifalarapiraca.local
  $ sudo vim /etc/bind/zones/db.jonathanmarcos924.labredes.ifalarapiraca.local
  ```
  ![create by template](images/dns/4.png)
  * editamos o arquivo de zona direta colocando as infromações referentes a dupla e ao sistema de nomes que será usado
  ![create by template](images/dns/5.png)
  * agora criamos o arquivo de zona inversa, usando o IP referente da nossa máquina e template existente no bind9 bem semelhante a como foi configurado o direto
  * editamos o arquivo criado de configuração para inserir os dados referentes a nossa rede usando o comando
  ```shell
  $ sudo nano /etc/bind/zones/db.10.9.24.rev
  ```
  ![create by template](images/dns/6.png)
* com os arquivos de zona devidamente configurados devemos agora ativa-los dentro da configuração do serviço de nomes, pra isso, precisamos editar o arquivo `/etc/bind/named.conf.local`
```shell
$ sudo nano /etc/bind/named.conf.local
```
![named conf](images/dns/7.png)
* após configurar o `named.conf.local` podemos testar a sintaxe usando o comando
```shell
$sudo named-checkconf
```
* então, iremos configurar o arquivo `/etc/default/named` para permitir resolver endereços IPv4
```shell
$sudo nano /etc/default/named
```
![create by template](images/dns/8.png)
```diff
+ Adicionar a linha OPTIONS="-4 -u bind"
```
* por fim, podemos executar o serviço do bind9
```shell
$ sudo systemctl enable bind9
$ sudo systemctl restart bind9
```

Pronto! com isso os serviços do bind9 estão configurados
___
Agora devemos adicionar o DNS ao netplan
* primeiro, editamos o arquivo base
```shell
$ sudo vim /etc/netplan/50-cloud-init.yaml
```
![cloud init](images/dns/9.png)
* Para resolver os DNS configurados e verificar os campos
```shell
$ resolvectl status
```
![cloud init](images/dns/10.png)

## Testes
* Teste de DNS para a maquina ns1
```shell
$ dig ns1.jonathanmarcos924.labredes.ifalarapiraca.local
```
![cloud init](images/dns/11.png)
* Teste de DNS para a máquina do samba
```shell
$ dig samba.jonathanmarcos924.labredes.ifalarapiraca.local
```
![cloud init](images/dns/12.png)
* Teste de DNS para a máquina do gateway
```shell
$ dig gw.jonathanmarcos924.labredes.ifalarapiraca.local
```
![cloud init](images/dns/13.png)
* Teste de DNS reverso para a máquina
```shell
$ dig 10.9.14.132 
```
![cloud init](images/dns/14.png)

* Teste ping samba
```shell
$ ping samba
```
![cloud init](images/dns/15.png)