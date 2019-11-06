# Easy DNS 

O projeto consiste em uma interface web onde é possível realizar tarefas adminstrativas básicas em um servidor DNS, 
sendo possível listar, cadastrar, atualizar e remover registros em um domínio específico. 

O projeto foi dividido nos seguintes modulos. 

## Easy-dns-ui 
Aplicação React que contempla a interface gráfica da aplicação. O projeto foi construído com a ferramenta utilitária 
create-react-app junto com a versão v11.15.0 do NodeJS. 


## Easy-dns-api 
Aplicação Python3 que realiza a interface de comunicação entre a aplicação web e o servidor DNS. Foi utilizada a versão 3.7 do Python. 
junto com o PipEnv para gerenciamento de dependências. 

As configurações do projeto são lidas pela aplicação através de variaveis de ambiente, porém em ambiente de desenvolvimento, também 
é possível adicionar um arquivo de configuração config.ini na raiz do projeto. 
O projeto necessita de uma chave TSIG para realizar as alterações no servidor DNS, a mesma deverá estar associda ao domínio utilizado. 

```
[dns]
server_host = #endereço do servidor DNS
avaliable_zones = ["test.example.com"]
connection_timeout = 5
[tsig]
key = #chave tsig
[auth]
username = #nome de usuário
password = #senha criptografada com sha 256
token_expires_in_minutes = 120
```

## Bind9 
Servidor DNS utilizado para armazenar os registros do domínio. Foi criado um arquivo de zona simples já pré configurado. 

## Arquitetura

![alt text](https://raw.githubusercontent.com/ribeiro-rodrigo/easy-dns/master/easy-dns.png)

## Baixando o projeto 
O projeto agrupa todos os submodulos listados acima, é possível baixar todos utilizando o comando de clonagem recursiva 
exemplificado abaixo.

```shell
git clone --recursive https://github.com/ribeiro-rodrigo/easy-dns
```
## Rodando o projeto 
O projeto foi testado em servidores Bedian 9, porém para fins práticos, foi disponibilizado um ambiente Docker Compose onde é possível
executar toda a solução com o objetívo de validação com apenas poucos comandos. Foi utilizada a versão 18.09.6, build 481bc77
do Docker e a versão 1.24.1, build 4667896b do Docker Compose. 

```shell
docker-compose build 
```

```shell
docker-compose up
```
## Validando a solução 
O projeto foi testado realizando as alterações pela interface gráfica e pela API e posteriormente realizando as querys diretamente no servidor DNS conforme mostra o exemplo abaixo. 

```shell
dig @167.71.166.167 host1.test.example.com A +answer

; <<>> DiG 9.10.3-P4-Debian <<>> @167.71.166.167 host1.test.example.com A +answer
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 33662
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 3

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;host1.test.example.com.		IN	A

;; ANSWER SECTION:
host1.test.example.com.	300	IN	A	201.17.89.171

;; AUTHORITY SECTION:
test.example.com.	604800	IN	NS	ns2.test.example.com.
test.example.com.	604800	IN	NS	ns1.test.example.com.

;; ADDITIONAL SECTION:
ns1.test.example.com.	604800	IN	A	167.71.166.167
ns2.test.example.com.	604800	IN	A	167.71.166.167

;; Query time: 124 msec
;; SERVER: 167.71.166.167#53(167.71.166.167)
;; WHEN: Wed Nov 06 16:48:02 -02 2019
;; MSG SIZE  rcvd: 135

```
