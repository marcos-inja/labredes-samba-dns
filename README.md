# <p align="center">INSTITUTO FEDERAL DE ALAGOAS CAMPUS ARAPIRACA - IFAL</p>
**Disciplina:** SRED </br>
**Professor:** Alaelson Jatobá </br>
**Aluno:** Jonathan Candido </br>
**Aluno:** Marcos Vinicius </br>
**Turma**: 924
## Introdução
<p align="justify">
Esse trabalho tem como objetivo implementantar o sevidor de compartilhamento de arquivos Samba junto com o DNS.
</p>

### Samba
<p align="justify">
Servidor Samba é um software executado em servidores Linux, responsável por estabelecer interações com redes constituídas por computadores com Windows.
</p>

### DNS
<p align="justify">
O Sistema de Nomes de Domínio, mais conhecido pela nomenclatura em Inglês Domain Name System, é um sistema hierárquico e distribuído de gestão de nomes para computadores, serviços ou qualquer máquina conectada à Internet ou a uma rede privada.
</p>

## Definições
Nas tabelas abaixo pode ser visto as definições de rede e nomes

### Definições de Rede
|Tipo|IP
|-|-
|Rede|10.9.24.0
|Máscara|255.255.255
|Gateway|10.9.24.1
|Broadcast|10.9.24.255
|ns1|10.9.24.114
|samba|10.9.24.114

### Definições de Nomes
|Tipo|Nome
|-|-
|Gateway|gw.jonathanmarcos924.labredes.ifalarapiraca.local|
|Name Server|ns1.jonathanmarcos924.labredes.ifalarapiraca.local|
|Samba|samba.jonathanmarcos924.labredes.ifalarapiraca.local|

## Implementado o Samba/DNS:

|Link
|-
[Configuração do DNS slave](DNS.md)
[Implementando o servidor samba](SAMBA.md) 
[Configuração Bind9](BIND9.md)

