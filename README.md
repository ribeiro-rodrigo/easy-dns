# Easy DNS 

O projeto consiste em uma interface web onde é possível realizar tarefas adminstrativas básicas em um servidor DNS, 
sendo possível listar, cadastrar, atualizar e remover registros em um domínio específico. 

O projeto foi dividido nos seguintes modulos. 

## Easy-dns-ui 
Aplicação React que contempla a interface gráfica da aplicação. O projeto foi construído com a ferramenta utilitária 
create-react-app junto com a versão v11.15.0 do NodeJS. 


## Easy-dns-api 
Aplicação Python3 que realiza a interface de comunicação entre a aplicação web e o servidor DNS. Foi utilizada a versão 3.7 do Python
junto com o PipEnv para gerenciamento de dependências. 

As configurações do projeto são lidas pela aplicação através de variaveis de ambiente, porem em ambiente de desenvolvimento, também 
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
