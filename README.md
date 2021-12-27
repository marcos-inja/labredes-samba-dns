# Configurando Servidor Samba

O SAMBA é um servidor e conjunto de ferramentas que permite que máquinas Linux e Windows se comuniquem entre si, compartilhando serviços (arquivos, diretório, impressão) através do protocolo SMB (Server Message Block)/CIFS (Common Internet File System), equivalentes a implementação NetBEUI no Windows.

## Instalação
```sh
$ sudo apt update
$ sudo apt install samba
```
![samba](images/samba/1.png)

Após instalar podemos checar o status do funcionamento usando os comandos
```sh
$ sudo systemctl status smbd
$ netstat -an | grep LISTEN
```
![status](images/samba/2.png)

> Com o samba em pleno funcionamento podemos fazer o backup das configurações iniciais dele e começarmos a personalizar!

## Configurando o Serviço
* abra o arquivo de configurações em `/etc/samba/smb.conf`
```sh
$ sudo vim /etc/samba/smb.conf
```
* agora vamos restringir o acesso aos usuários do grupo sambashare e adicionar opções de configurações mais especificas pra rede
![smb1](images/samba/3.png)
* após configurarmos o samba, reiniciaremos o serviço pra que ele possa aplicar as configurações
```sh
$ sudo systemctl restart smbd
```
* após a reinicialização iremos configurar os dados de autenticação dentro do samba para permitir acessa-lo por via de uma autenticação baseada em senha, usando os comandos
    ```sh
    $ sudo adduser aluno

    $ sudo smbpasswd -a aluno

    $ sudo usermod -aG sambashare aluno
    ```
## Compartilhando arquivos
Precisamos criar uma pasta que vai ser usada como repositorio aberto do servidor de arquivos

* para aplicar o compartilhamento precisamos criar uma pasta chamada sambashare no **aluno**, e então criar uma pasta public em um diretório samba na raiz, usando os comandos:
    ```sh
    $ mkdir /home/aluno/sambashare/

    $ sudo mkdir -p /samba/public
    ```
* agora após a criação da pasta, devemos dá permições a elas
    ```sh
    $ sudo chown -R nobody:nogroup /samba/public

    $ sudo chmod -R 0775 /samba/public

    $ sudo chgrp sambashare /samba/public
    ```

## Teste de compartilhamento
Assista o video abaixo para ver o samba rodando:

[![Teste Samba](images/samba/4.png)](https://www.youtube.com/watch?v=RHCmBywV_Mg&ab_channel=MarcosVas)


## Veja tambem:
Configurando o dns slave: [DNS Slave](DNS.md)

Configurando o dns master: [DNS Master](BIND9.md)

