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

Acesse a máquina e certifique que o firewall está ativo

```vagrant
vagrant ssh
```

```vagrant
sudo ufw status
sudo ufw enable
```

## Site

Após o comando vagrant up, um site será disponibilizado no IP: [192.168.60.58](http://192.168.60.58) na porta 80 (HTTP).

![site_gif](https://user-images.githubusercontent.com/50564212/165188971-ecceabbf-6574-4918-a962-a290b4d8934f.gif)


### Regras dos serviços: 

#### **Samba**

**Regra 1:**
Diretório ‘/basic’ poderá ser acessado por usuários dos grupos basic e admin.]

***Usuário para teste:***

    user: baUser 
    senha: baUser


**Regra 2:** Diretório ‘/admin poderá ser acessado por usuários do grupo admin.

***Usuário para teste:***

    user: adUser
    senha: adUser

**Regra 3:** Fazer com que arquivos com as seguintes extensões sejam bloqueados. Exemplos: .exe, .bin, .csh, .bat, .ksh, .out, .run

***Usuário para teste:***

    user: adUser || baUser
    senha: adUser || baUser


![Samba](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bd/Logo_Samba_Software.svg/1280px-Logo_Samba_Software.svg.png) 
## ⠀⠀⠀
#### **Proxy**

**Regra 1:**
Lista de sites bloqueados e palavras bloqueadas.

***Exemplo de sites para teste:***

    google.com (BLOCK BY denyWebsites.lst)
    github.com (BLOCK BY denyWords.lst)
    unijui.edu.br (GOOD)



**Regra 2:** Fazer com que a regra 1 não seja ativada em um certo horário, ou seja, em um determinado horário será possível acessar os sites e palavras bloqueadas.

***Horário de bloqueio:***

    início: 08:00
    fim: 17:00

***Exemplo:***

    sudo timedatectl set-ntp off
    sudo timedatectl set-time 10:00:00
    faça o teste    
    sudo timedatectl set-ntp on


**Regra 3:** Limitar a velocidade máxima da banda.


![Proxy](https://www.fasim.com.br/wp-content/uploads/2017/10/Squid-proxy-logo.jpg) 
## ⠀⠀⠀
#### **Email**

**Regra 1:**
Limitar o tamanho de anexos no email.

***Teste com:***

 Na máquina externa entre na pasta /files/test-files

copie o conteúdo do arquivo “big.txt”

    $ telnet 192.168.60.58 25

    MAIL FROM: root@localhost
    RCPT TO: vagrant@localhost


    DATA
    Subject: Teste limite


    ${Conteúdo arquivo “big.txt”}


    .
    ```
    quit

Na máquina provisionada, entre no usuário vagrant (padrão) e digite
    
    $ mail

**Regra 2:** Bloquear uma lista de extensões para os arquivos de anexos.

***Exemplo de extensões para teste:*** .bin (BLOCK) .pdf (GOOD)

***Teste com:*** Entre na pasta ->files/test-files

    $ echo "Mensagem" | mutt -s "Subject" vagrant@192.168.60.58:25 -a ./some.exe

**Regra 3:** Limitar a quantidade de remetentes para um email, visando implementar uma regra de anti-spam.

***Teste com:***

    MAIL FROM: root@localhost
    RCPT TO: vagrant@localhost
    RCPT TO: adUser@localhost

![Email](https://wiki.deimos.fr/images/3/34/Postfix_logo.png) 
## ⠀⠀⠀
#### **Firewall**

**Regra 1:** Bloquear o acesso por SSH porta 22.

***Usuário para teste:***
 user: baUser
 senha: baUser


**Regra 2:** Bloqueia todas as portas que não serão usadas.

***Teste com:***
 
    sudo ufw enable
    sudo ufw status
	curl https://www.google.com	– Erro
	sudo ufw disable
	curl https://www.google.com	– Sucesso

**Regra 3:** Adiciona log para solicitações no Firewall.

***Teste com:***

Faça alguma ação com a máquina provisionada (telnet, samba, proxy…)

E então verifique o arquivo de log do Firewall

    $ sudo nano /var/log/ufw.log

![Firewall](https://lintut.com/wp-content/uploads/2021/04/ubuntu_ufw.png) 
## ⠀⠀⠀
#### **FTP**

**Regra 1:**
Apenas acesso com login e senha

***Usuário para teste:***
 user: baUser
 senha: baUser

***Teste com:***

Dentro do Filezilla vá para File > Site Manager

Estando lá clique em New Site

Selecione TLS explícito nas opções de criptografia

Utilize os seguintes dados nos campos:

    Host: 192.168.60.58
    Logon Type: Ask Password
    User: adUser
Inseridos esses dados, clique em Connect e insira a senha "adUser"



**Regra 2:** Bloquear downloads.

**Regra 3:** Bloquear certas extensões de arquivos e também uma lista de nomes de pastas/arquivos que será bloqueada.

***Teste com:***

Na máquina externa entre na pasta /files/test-files

tente transferir o arquivo “some.exe” (BLOCK BY *.exe)

tente transferir o arquivo “senha-felipe.txt” (BLOCK BY *felipe*)


![FTP](https://www.linuxcloudvps.com/blog/wp-content/uploads/2014/03/vsftpd.jpg) 

## Autores

- [@Felipe Schmidt](https://www.github.com/FelipeESchmidt)
- [@Gabriel Walker](https://github.com/GabrielMWalker)
- [@Luis Gustavo Tabile](https://github.com/LuisTabile)

## Repositório

- [___GitHub___](https://github.com/FelipeESchmidt/ansible-box-services)

![GitHub](https://logos-world.net/wp-content/uploads/2020/11/GitHub-Emblem.png) 
