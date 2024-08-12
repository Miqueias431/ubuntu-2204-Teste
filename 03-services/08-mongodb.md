#Autor: Robson Vaamonde<br>
#Procedimentos em TI: http://procedimentosemti.com.br<br>
#Bora para Prática: http://boraparapratica.com.br<br>
#Robson Vaamonde: http://vaamonde.com.br<br>
#Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi<br>
#Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica<br>
#Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem<br>
#YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica<br>
#Data de criação: 30/01/2023<br>
#Data de atualização: 12/08/2024<br>
#Versão: 0.26<br>

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO MONGODB SE VOCÊ CONSEGUIU FAZER O DESAFIO COM A SEGUINTE FRASE: Desafio do MongoDB realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTAGRAM) MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/08-mongodb.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver #ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiomongodb #desafiocompass

Conteúdo estudado nesse desafio:<br>
#01_ Instalando as Dependências do MongoDB Server<br>
#02_ Adicionando o Repositório do MongoDB Server<br>
#03_ Instalando o MongoDB Server no Ubuntu Server<br>
#04_ Verificando o Serviço e Versão do MongoDB Server<br>
#05_ Verificando a Porta de Conexão do MongoDB Server<br>
#06_ Diretórios e Arquivos de Configuração do MongoDB Server<br>
#07_ Adicionando o Usuário Local no Grupo do MongoDB Server<br>
#08_ Acessando o Console do MongoDB Server<br>
#09_ Comandos Básicos do MongoDB Server<br>
#10_ Criando o Usuário de Administração do MongoDB Server<br>
#11_ Configurando o Acesso Remoto do MongoDB com Autenticação<br>
#12_ Acessando o MongoDB Server com Compass GUI<br>
#13_ Acessando o MongoDB Server com Visual Studio Code VSCode<br>
#14_ Desafios do Banco de Dados MongoDB Server.

Site Oficial do MongoDB: https://www.mongodb.com/<br>
Site Oficial do MongoDB Compass: https://www.mongodb.com/products/compass<br>
Site Oficial da MongoDB Atlas: https://www.mongodb.com/atlas/database

Site Oficial do W3C School MongoDB: https://www.w3schools.com/mongodb/<br>
Site Oficial do W3C School JSON: https://www.w3schools.com/js/js_json.asp

MongoDB é um software de banco de dados orientado a documentos livre, de código aberto e multiplataforma, escrito na linguagem C++. Classificado como um programa de banco de dados NoSQL, o MongoDB usa documentos semelhantes a JSON com esquemas.

[![MongoDB Server](http://img.youtube.com/vi/qs-zRXaSmuM/0.jpg)](https://www.youtube.com/watch?v=qs-zRXaSmuM "MongoDB Server")

Link da vídeo aula: https://www.youtube.com/watch?v=qs-zRXaSmuM

#01_ Instalando as Dependências do MongoDB Server<br>
```bash
#atualizando as lista do apt
sudo apt update

#instalando as dependências do MongoDB Server
sudo apt install git vim build-essential software-properties-common gnupg apt-transport-https ca-certificates

#download da última versão do Libssl (link atualizado em 02/08/2024)
#OBSERVAÇÃO IMPORTANTE: o tempo todo a Biblioteca Libssl sofre alteração, antes de faze o download do 
#arquivo verifique a versão no link: http://nz2.archive.ubuntu.com/ubuntu/pool/main/o/openssl/
wget http://nz2.archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.23_amd64.deb

#instalando a biblioteca Libssl no Ubuntu Server
#opção do comando dpkg: -i (install)
sudo dpkg -i libssl*.deb
```

#02_ Baixando e instalando a Chave GPG do MongoDB Server<br>
```bash
#download da Chave GPG do MongoDB Server (VERSÃO ESTÁVEL ATÉ O MOMENTO: 7.0 EM: 06/04/2024)
#Mais informações acesse: https://www.mongodb.com/pt-br/docs/manual/release-notes/
#OBSERVAÇÃO IMPORTANTE: o MongoDB Server possui várias versões, para verificar as chaves GPG 
#de cada versão acesse o link: https://www.mongodb.org/static/pgp/
#opção do comando curl: -f (fail), -s (silent), -S (show-error), -L (location)
#opção do redirecionador |: Conecta a saída padrão com a entrada padrão de outro comando
#opção do comando gpg: -o (output)
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-7.0.gpg
```

#03_ Criando o repositório do MongoDB Server<br>
```bash
#opção do redirecionador |: Conecta a saída padrão com a entrada padrão de outro comando
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```

#04_ Atualizando as Lista do Apt com o novo Repositório do MongoDB Server<br>
```bash
#atualizando as listas do Apt
sudo apt update
```

#05_ Instalando o MongoDB Server e Client<br>
```bash
#instalando o MongoDB Server e Shell (Console)
sudo apt install mongodb-org
```

#06_ Habilitando o Serviço do MongoDB Server<br>
```bash
#habilitando o serviço do MongoDB Server
sudo systemctl daemon-reload
sudo systemctl enable mongod
sudo systemctl start mongod
```

#07_ Verificando o Serviço e Versão do MongoDB Server e do Client<br>
```bash
#verificando o serviço do MongoDB Server
sudo systemctl status mongod
sudo systemctl restart mongod
sudo systemctl stop mongod
sudo systemctl start mongod

#analisando os Log's e mensagens de erro do Servidor do MongoDB (NÃO COMENTADO NO VÍDEO)
#opção do comando journalctl: -t (identifier), x (catalog), e (pager-end), u (unit)
sudo journalctl -t mongod
sudo journalctl -xeu mongod

#verificando as versões do MongoDB Server e do Client
sudo mongod --version
sudo mongosh --version
```

#08_ Verificando a Porta de Conexão do MongoDB Server<br>
```bash
#OBSERVAÇÃO IMPORTANTE: no Ubuntu Server as Regras de Firewall utilizando o comando: 
#iptables ou: ufw está desabilitado por padrão (INACTIVE), caso você tenha habilitado 
#algum recurso de Firewall é necessário fazer a liberação do Fluxo de Entrada, Porta 
#e Protocolo TCP do Serviço corresponde nas tabelas do firewall e testar a conexão.

#opção do comando lsof: -n (network number), -P (port number), -i (list IP Address), -s (alone directs)
sudo lsof -nP -iTCP:'27017' -sTCP:LISTEN
```

#09_ Localização dos Arquivos de Configuração do MongoDB Server<br>
```bash
/etc/mongod.conf  <-- arquivo de configuração do MongoDB Server
/var/log/mongodb  <-- diretório dos arquivos de Log do MongoDB Sever
/var/lib/mongodb  <-- diretório dos arquivos de Banco de Dados do MongoDB Server
```

#10_ Adicionado o Usuário Local no Grupo Padrão do MongoDB Server<br>
```bash
#opções do comando usermod: -a (append), -G (groups), $USER (environment variable)
#OBSERVAÇÃO IMPORTANTE: você pode substituir a variável de ambiente $USER pelo
#nome do usuário existente no sistema para adicionar no Grupo desejado.
sudo usermod -a -G mongodb $USER

#fazendo login em um novo grupo do MONGODB
newgrp mongodb

#verificando os identificadores de usuário e grupos
id

#verificando informações do grupo MONGODB
sudo getent group mongodb

#recomendo fazer logout do usuário para testar as permissões de grupos
#OBSERVAÇÃO: você pode utilizar o comando: exit ou tecla de atalho: Ctrl +D
exit
```

#11_ Testando a Conexão Local com o MongoDB Server via Shell<br>
```bash
#acessando o MongoDB Server via Shell (MongoDB Shell/Console)
mongosh
```

#12_ Comandos Básicos do MongoDB Server<br>
```bash
#exibindo os bancos de dados existentes no MongoDB
show dbs

#alterar o database informe no MongoDB
use admin

#listar o database informe atual no MongoDB
db

#exibir os collections do database informe atual no MongoDB
show collections

#sair do MongoDB
quit
```

#13_ Criando o usuário de administração do MongoDB Server<br>
```bash
#acessando o MongoDB Server via Shell (MongoDB Shell/Console)
mongosh

#alterar o database informe no MongoDB
use admin

#OBSERVAÇÃO IMPORTANTE: na gravação do vídeo não consta os dois papeis que foram adicionados
#posteriormente na linha roles: "root" e "clusterAdmin", conforme testes e comentários nos
#vídeos, no momento do desenvolvimento de aplicações Node.JS junto com o recurso de conexão 
#com o MongoDB utilizando o Mongoose acontecia uma falha de: "Erro de permissão", essa falha 
#foi corrigida adicionando essas "Roles" e na conexão com o Banco de Dados foi adicionado a 
#opção: ?authSource=admin

#OBSERVAÇÃO IMPORTANTE: No software MongoDB Compass, na aba de Performance, tanto no GNU/Linux
#ou no Microsoft Windows a falha de acesso de permissão para monitorar o MongoDB e apresentada
#com a seguinte mensagem: Command "top" returned error "not authorized on admin to execute command 
#{ top: 1, lsid: { id: UUID("ed17ae23-570c-4652-a151-b0875183faa1") }, $db: "admin" }", and other 
#2 problems. View all, para resolver essa e outras falhas foi adicionado mais Roles (Papéis)
#no usuário admin conforme o link: https://www.mongodb.com/docs/manual/tutorial/manage-users-and-roles/
```
```javascript
db.createUser(
  {
    user: "admin",
    pwd: "pti@2018",
    roles: [
      { role: 'root', db: 'admin' },
      { role: 'read', db: 'admin' },
      { role: 'hostManager', db: 'admin' },
      { role: 'backup', db: 'admin' },
      { role: 'dbAdmin', db: 'admin' },
      { role: 'userAdmin', db: 'admin' },
      { role: 'userAdminAnyDatabase', db: 'admin' },
      { role: 'dbAdminAnyDatabase', db: 'admin' },
      { role: 'readWriteAnyDatabase', db: 'admin' },
      { role: 'readAnyDatabase', db: 'admin' },
      { role: 'clusterAdmin', db: 'admin' },
      { role: 'clusterMonitor', db: 'admin' },
      { role: 'clusterManager', db: 'admin' }
    ]
  }
)
```
```bash
#visualizando os usuários do MongoDB
db.getUsers()

#saindo do MongoDB
exit
```

#14_ Configurando o MongoDB Server para suportar autenticação e Acesso Remoto<br>
```bash
#fazendo o backup do arquivo de configuração do MongoDB Server
#opção do comando cp: -v (verbose)
sudo cp -v etc/mongod.conf etc/mongod.conf.old

#editando o arquivo de configuração do MongoDB Server
sudo vim /etc/mongod.conf
INSERT
	
	#habilitando o suporte remoto do MongoDB Server na linha: 18
	#alterar a linha: bindIp: 127.0.0.1 para: bindIp: 0.0.0.0
	net:
	  port: 27017
	  bindIp: 0.0.0.0
	
	#habilitando o recurso de autenticação do MongoDB Server na linha: 28
	#descomentar a linha: #security, adicionar o valor: authorization: enabled
	security:
	  authorization: enabled

#salvar e sair do arquivo
ESC SHIFT :x <ENTER>

#reiniciar o serviço do MongoDB Server
sudo systemctl restart mongod
sudo systemctl status mongod
```

#15_ Acessando o MongoDB COM e SEM autenticação<br>
```bash
#acessando novamente o console do MongoDB
mongosh

#exibir os bancos de dados existentes no MongoDB
show dbs

#saindo do MongoDB Server
quit

#opção do comando mongosh: admin (database) -u (username), -p (password)
mongosh admin -u admin -p

#exibir os bancos de dados existentes no MongoDB
show dbs

#saindo do MongoDB Server
quit
```

#16_ Integrando o MongoDB Server com o Compass GUI (graphical user interface)<br>
```bash
Link de download do MongoDB Compass: https://www.mongodb.com/products/tools/compass

#criando uma nova conexão com o MongoDB Server
<New connection+>
	New Connection
		URL: mongodb://172.16.120:27017
	Advanced Connection Options
		Connection String Scheme
			mongodb
		Host:
			172.16.1.20:27017 (alterar o endereço IPv4 do seu servidor)
	Authentication
		Username/Password
			Username: admin 
			Password: pti@2018 (alterar a senha do usuário admin do seu servidor)
			Authentication Database: admin
		Authentication Mechanism
			Default
	<Save & Connect>
```

#17_ Integrando o MongoDB Server com o Visual Studio Code VSCode<br>
```bash
#instalando a Extensão do MongoDB
VSCode
  Extensões
    Pesquisar
      MongoDB for VS Code
        Instalar

#configurando a conexão com o MongoDB Server
VSCode
  MongoDB
    CONNECTIONS
      Add Connection
        Advanced Connection String: <Open From>
          New Connection
            General
              Connection Type: Standalone
              Hostname: 172.16.1.20 
              Port: 27017
              Authentication: Username/Password
                Username: admin
                Password: pti@2018
                Authentication Database: admin
           <Connect>
        <Close>
```

========================================DESAFIOS=========================================

**#18_ DESAFIO-01:** CRIAR UM BANCO DE DADOS COM O: __`seu_nome`__ (TUDO EM MINÚSCULO), DENTRO DESSE BANCO DE DADOS CRIAR UM COLLECTION CHAMADO: __`cadastro`__ (TUDO EM MINÚSCULO) E DENTRO DESSE COLLECTION INSERIR OS DOCUMENTS: __`nome: Seu Nome e Sobrenome, idade: Sua Idade`__ LISTAR AS INFORMAÇÕES NO VSCODE OU NO COMPASS (VEJA O SITE W3SCHOOLS).

**#19_ DESAFIO-02:** CONHECER O PROJETO: __`MongoDB Atlas`__, FAZER O CADASTRO NO SITE OFICIAL PARA A CRIAÇÃO DE UMA __`CONTA FREE`__ NO LINK: https://www.mongodb.com/cloud/atlas/register, ESCOLHER A OPÇÃO: __`LEARN FREE`__, FINALIZAR O CADASTRO CRIANDO UM USUÁRIO E FAZER A CRIAÇÃO DO MESMO BANCO DE DADOS DO DESAFIO-O1, TESTAR A CONEXÃO NO MONGODB COMPASS E NO VSCODE. OBSERVAÇÃO: VEJA A DOCUMENTAÇÃO NA OPÇÃO DE: CONNECT EM: __`MongoDB for VS Code`__, CUIDADO PRINCIPALMENTE COM AS OPÇÕES DE CARACTERES ESPECIAIS NA SENHA, VEJA A DOCUMENTAÇÃO ABAIXO:

https://www.mongodb.com/docs/atlas/troubleshoot-connection/#special-characters-in-connection-string-password

**#20_ DESAFIO-03:** ADICIONAR O USUÁRIO: __`admin`__ E O: __`seu_usuário`__ CRIADOS NO DESAFIO DO OPENSSH NO GRUPO DO MONGODB PARA FACILITAR A ADMINISTRAÇÃO E GERENCIAMENTO SEM A NECESSIDADE DO SUDO.

=========================================================================================

OBSERVAÇÃO IMPORTANTE: COMENTAR NO VÍDEO DO MONGODB SE VOCÊ CONSEGUIU FAZER O DESAFIO COM A SEGUINTE FRASE: Desafio do MongoDB realizado com sucesso!!! #BoraParaPrática

COMPARTILHAR O SELO DO DESAFIO NAS SUAS REDES SOCIAIS (LINKEDIN, FACEBOOK, INSTAGRAM) MARCANDO: ROBSON VAAMONDE COM AS HASHTAGS E CONTEÚDO DO DESAFIO ABAIXO: 

LINK DO SELO: https://github.com/vaamonde/ubuntu-2204/blob/main/selos/08-mongodb.png

#boraparapratica #boraparaprática #vaamonde #robsonvaamonde #procedimentosemti #ubuntuserver #ubuntuserver2204 #desafiovaamonde #desafioboraparapratica #desafiomongodb #desafiocompass