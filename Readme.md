## Serviços Utilizados:
### Servidor: 

O servidor utilizado nesta box foi o Apache (apache2), pois, ele é o servidor mais popular
e também é muito confiável. O apache é utilizado por gigantes como Netflix, Airbnb, eRay,
Microsoft entre outros. Esse servidor atende às solicitações de acesso de conteúdo de 
vários usuários.

![apache](https://ubiq.co/tech-blog/wp-content/uploads/2020/07/increase-request-timeout-apache.png)

### Linguagem de provisionamento:

A linguagem de provisionamento utilizada foi o Ansible, e foi escolhida pois é uma das mais, você pode lidar com tarefas complexas com uma ferramenta fácil de usar. 
 

![ansible](https://miro.medium.com/max/447/1*eGsQ4xEeXAL_eCoE3Ld1uw.png)

### Serviço provisionado: 

O serviço utilizado neste server proxy foi o Squid, pois o uso do mesmo como Proxy/Cache 
é uma das opções mais utilizadas em ambientes corporativos que adotam software livre para 
administrar a rede, seja atráves da otimização e melhoria do desmpenho da rede atuando 
como servidor de cache ou como proxy, implementando restrições de acesso à internet, que 
nem sempre é possível ser feita por firewall.

![squid](https://www.arduinoecia.com.br/wp-content/uploads/2020/02/squid-logo-png.png) 

## Pré-Requisitos do Linux

```bash
sudo apt update
sudo apt-get update
```

#### VirtualBox instalado

```bash
sudo apt-get install -y virtualbox
```

#### Vagrant instalado

```bash
sudo apt-get install -y vagrant
```

#### Ansible instalado

```bash
sudo apt-get install -y ansible
```

## Rodando a box

***!! Certifique-se que não há nenhuma box com o nome (__serverProxy__) na máquina !!***

Para rodar o arquivo Vagrantfile basta acessar a pasta com os arquivos e rodar o seguinte
comando

```vagrant
vagrant up
```

Acesse a máquina e verifique que o firewall está ativo

```vagrant
vagrant up
```

```vagrant
sudo ufw enable
```

## Site

Após o comando vagrant up, um site será disponibilizado no IP: [192.168.60.58](http://192.168.60.58) na porta 80 (HTTP).

![site_gif](https://user-images.githubusercontent.com/50564212/165188971-ecceabbf-6574-4918-a962-a290b4d8934f.gif)

## Utilizando o servidor proxy

O proxy pode ter várias aplicabilidades, tais quais como bloquear sites por horário, 
bloquear URLs específicas, controlar o limite de banda entre outros.

Você pode encontrar algumas funções nos seguintes links:

* [Autenticação de usuários](https://gist.github.com/jackblk/fdac4c744ddf2a0533278a38888f3caf)
* [Bloqueio de palavras](https://www.vivaolinux.com.br/topico/Squid-Iptables/Bloqueando-palavras-squid)
* [Bloqueio de uma faixa de IP](https://under-linux.org/showthread.php?t=83897)
* [Bloqueio de uma porta](https://www.cyberciti.biz/faq/linux-unix-squid-proxy-filtering-particular-port/)
* [Bloqueio por horário](https://www.vivaolinux.com.br/dica/SQUID-Liberando-Internet-por-horario)
* [Limitação de banda](https://www.vivaolinux.com.br/dica/Squid-Implementando-controle-de-banda)

Como exemplo bloqueamos o acesso de URLs e para testar o serviço você terá que configurar o seu navegador para utilizar o proxy da box que foi criada. Para isso, siga os passos a seguir:

* Encontre o menu de configurações do seu navegador
* Busque por configurações avançadas
* Busque pela opção para configurar o proxy
* Busque pela opção de configuração manual do proxy
* Adicione o seguinte IP como endereço do proxy - [192.168.60.58]()
* Adicione a seguinte porta como porta do serviço - [3128]()

## Testando o proxy

Para testar se o proxy está funcionando basta tentar acessar algum dos sites listados abaixo

#### URLs bloqueadas pelo proxy
- [google.com](https://google.com)
- [bing.com](https://bing.com)
- [yahoo.com](https://yahoo.com)
- [duckduckgo.com](https://duckduckgo.com)
- [ask.com](https://ask.com)
- [aol.com](https://aol.com)
- [searchencrypt.com](https://searchencrypt.com)
- [msn.com](https://msn.com)
- [wolframalpha.com](https://wolframalpha.com)
- [nationmaster.com](https://nationmaster.com)

## Autores

- [@Felipe Schmidt](https://www.github.com/FelipeESchmidt)
- [@Gabriel Walker](https://github.com/GabrielMWalker)
- [@Luis Gustavo Tabile](https://github.com/LuisTabile)

## Repositório

- [___Github___](https://github.com/FelipeESchmidt/vagrant-puppet-proxy)
- 
# Outros Serviços

## Samba
Para rodar esse trabalho você precisará ter instalado os seguintes programas:
   - Vagrant     (apt install vagrant)
  -  VirtualBox  (apt install virtualbox)
 -   Ansible     (apt install ansible)
Com esses programas instalados basta executar o seguinte comando na pasta root do trabalho:
    vagrant up
Após finalizar o comando acesse em seu navegador a seguinte url para demais instruções.
    http://192.168.56.56

Abra o gerenciado de arquivos e na barra de pesquisa digite: smb://192.168.56.56/samba/
Após localizar, será solicitado dados de acesso: Usuário = vagrant e Senha= 123
    
## Email
Configurar o mail server "Postfix" com Ansible



- instale as dependências
- entre na pasta com o Vagrantfile
- rode `$ vagrant up`
- acesse a máquina com `$ vagrant ssh`
- acesse a máquina com `$ vagrant ssh`
- criar usuário dentro da vm
`$ sudo adduser destinatario`
- acesse o server via telnet: `$ telnet localhost 25` (pode ser feito de fora da máquina com `$ telnet 192.168.56.56`)
- no terminal do telnet, entrar os comandos:
```
MAIL FROM: root@localhost
RCPT TO: destinatario@localhost

DATA
Subject: Título do Email

Aqui está o corpo do nosso email

.
```
- o ponto marca o final do corpo do email
- `quit` para sair do telnet
- para testar se o email foi enviado, faça login como destinatario:
`$ su destinatario`
- veja sua caixa de entrada com `$ mail` (do pacote instalado mailutils), o email recebido irá aparecer na caixa de entrada
- dentro da vm, você também pode ver seus emails com o mail client "Mutt", que já irá estar instalado, rode: `$ mutt`, o mutt pode ser usado inclusive para facilmente deletar, responder ou encaminhar os emails
- 
## Firewall
Antes de rodar o vagrant instale o Ansible com o comando: sudo apt get ansible

Com a vm rodando acesse a página com o ip 192.168.56.56 


- Preparação do UFW

$ sudo nano /etc/default/ufw -> Verificar IPV6 = yes, caso não for, altere.
$ sudo ufw disable && sudo ufw enable -> Desliga, e Ligar o Firewall para aplicar o ipv6 caso não aplicou alguma modificação

$ sudo ufw allow ssh || sudo ufw allow 22/tcp -> Ambos tem a mesma função de permitirem conexões por SSH

- Negar Conexões

- Bloquear todos os ips de SSH
$ sudo ufw default deny incoming -> Define o firewall para negar todas as conexões de entrada

- Bloquear ip especifico
$ sudo ufw deny from 203.0.113.4 -> Define um ip especifico para negar,o ip deve ser trocado pelo ip real que você quer bloquear

$ sudo ufw allow www -> Permite acesso a todas as páginas www
$ sudo ufw allow 80/tcp -> Para permitir acesso a porta 80 (permitir conexão http do apache e nginx)
$ sudo ufw allow ftp || sudo ufw allow 21/tcp -> Para permitir conexões FTP

## Serviço de Arquivos FPT

Antes de rodar o vagrant instale o Ansible com o comando: sudo apt get ansible

Com a vm rodando acesse a página com o ip 192.168.56.56 

Para conectar ao servidor de arquivos utilize um client como Filezilla (https://filezilla-project.org)

    - Dentro do Filezilla vá para File > Site Manager
    - Estando lá clique em New Site
    - Selecione TLS explícito nas opções de criptografia
    - Utilize os seguintes dados nos campos:
    - Host: 192.168.56.56
     - Logon Type: Ask Password
       - User: teste
    - Inseridos esses dados, clique em Connect e insira a senha "teste"
    - Para fazer o upload de um arquivo, arraste um arquivo para a janela abaixo de Remote Site
    - Para fazer o download de um arquivo ou pasta, clique com o botão direito e escolha Download
    
## Banco de Dados
Esta instalado o PHP e o PHPmyadmin
