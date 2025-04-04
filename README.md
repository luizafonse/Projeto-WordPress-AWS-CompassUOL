# Configuração de Servidor Web utilizando o Docker

### Aplicações utilizadas:

### GitHub, Amazon Web Services, Microsoft Store, WSL, Visual Studio Code, Docker.

<div align="center">
  <br>
  <a href="https://github.com/">
    <img src="/imgs/gitlogo.png" alt="GitHub" width="100">
  </a>&ensp;

  <a href="https://www.googleadservices.com/pagead/aclk?sa=L&ai=DChcSEwjKuL74ltWLAxXoEUQIHY40KqwYABAAGgJkeg&co=1&ase=2&gclid=CjwKCAiA5eC9BhAuEiwA3CKwQp-uZ-EhfKVs_yaTVCZmvhF8olLyCz4sF_rQXc-KTkKjJ6zjkq_KbRoCmx0QAvD_BwE&ei=46i4Z7zJLbLb5OUP_NnOYQ&ohost=www.google.com&cid=CAESVeD2mSl7f0Xe0yyJImaMygYDsAuUvVqE8TXk7HbEuO8df6HhHkyj13nbeuQIUd6NDilzCovM3hpvmJWnXIKlBj1rDcr0Uva9DVYGZCTyi2T-YG-tn0A&sig=AOD64_3dqO5hHHx21zCm5ROWF8TSPV62pA&q&sqi=2&nis=4&adurl&ved=2ahUKEwj8xrT4ltWLAxWyLbkGHfysMwwQ0Qx6BAgIEAE">
    <img src="/imgs/amazonicon.webp" alt="Amazon Web Services" width="100" height="100">
  </a>&ensp;

  <a href="https://apps.microsoft.com/home?hl=pt-BR&gl=BR">
    <img src="/imgs/micstorelogo.png" alt="Microsoft Store" width="100" height="100">
  </a>&ensp;

  <a href="https://www.microsoft.com/store/productId/9P9TQF7MRM4R?ocid=libraryshare">
    <img src="/imgs/wsllogoo.png" alt="WSL" width="100" height="100">
  </a>&ensp;

  <a href="https://code.visualstudio.com/">
    <img src="/imgs/vscodelogo.png" alt="Visual Studio Code" width="100" height="100">
  </a>&ensp;

  <a href="https://hub.docker.com/">
    <img src="/imgs/dockerlogo.webp" alt="Nginx" width="100" height="100">
  </a>&ensp;
</div>

> [OBS]
> Aplicações obrigatórias para o funcionamento são o **GitHub**, **Amazon Web Services** e o **Docker**. Outras utilizações foram opcionais.

> [Utilizações]
> - **GitHub:** Documentação do projeto.
> - **Amazon Web Services (AWS):** Criação da infraestrutura de TI.
> - **Microsoft Store:** Baixar o WSL e o Ubuntu 24.04.
> - **WSL (Windows Subsystem for Linux):** Executa um ambiente Linux diretamente no sistema operacional Windows.
> - **Visual Studio Code:** Editor de código e terminal.
> - **Docker:** Container do wordpress como servidor web.

---

## Linguagens:
**Bash:** É uma linguagem de script e um interpretador de comandos.

**Markdown:** É uma linguagem de marcação leve.

> [OBS]
> Você pode utilizar a linguagem Python ao invés de Bash.


---


O objetivo do projeto é de criar instâncias na AWS que conteram o Docker (por meio de containers do WordPress), integrando-as a múltiplos serviços, como:

- EFS (Elastic File System)
- RDS (Relational Database Service)
- CLB (Classic Load Balancer)
- ASG (Auto Scalling Groups)
- CloudWatch

```
1. instalação e configuração do DOCKER ou CONTAINERD no host EC2;
SEGUIR DESENHO TOPOLOGIA DISPOSTA.
Ponto adicional para o trabalho utilizar a instalação via script de Start Instance (user_data.sh)
2. Efetuar Deploy de uma aplicação Wordpress com: container de aplicação RDS database Mysql
3. configuração da utilização do serviço EFS AWS para estáticos do container de aplicação Wordpress
4. configuração do serviço de Load Balancer AWS para a aplicação Wordpress

```

![1](/imgs/doc.png)


### Primeira etapa `local`: Criação do ambiente de testes.

<div>
<details align="left">
    <summary></summary>
1 - Baixe o wsl (Pela loja da Microsoft || Por linha de comando).

```
wsl --install
```


2 - Instale a versão mais atual do ubuntu (Pela loja da Microsoft || Por linha de comando).

```
wsl --install -d Ubuntu-24.04
```

3 - Instale o um editor de código de sua preferência (VScode).

```
https://code.visualstudio.com/download
```

4 - Faça um conexão ao wsl.

Instale o WSL na Microsoft Store.
![2](/imgs/WSL.png)

Após isso, aceite as extensões que o seu VSCode deseja instalar. Elas serã responsáveis por fornecer esse suporte a sistemas no Shell do próprio Visual Studio. Após isso, verá estas Aspas, clique nelas;
![3](/imgs/aspinhas.png)

Selecione "Connect to WSL" e você será redirecionado para uma tela de shell do seu Subsistema.
![4](/imgs/connecttowsl.png)

Nele, atualize a máquina:
```
sudo apt update && sudo apt upgrade -y
```

Por conseguinte, realize as instalações:
```
#Certificados necessários
sudo apt install -y ca-certificates curl gnupg

#Chave oficial do Docker
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

#Repositório docker no APT
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

#Atualize
sudo apt update

sudo apt upgrade -y

#Instale o docker e o docker compose.
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

#Opcional, mas recomendado adicionar o usuário ao grupo do docker
sudo usermod -aG docker $USER

#Habilite o dokcer para iniciar com o sistema, para facilitar seu funcionamento
sudo systemctl enable docker
sudo systemctl start docker
```
</div>

### Segunda etapa `local`: Teste de implementação do *Wordpress*.

<div>
<details align="left">
    <summary></summary>
Para o projeto, será necessário nomear sua rede (redefonte), e criar dois volumes, um para armazenar os arquivos do WordPress e o outro para o banco de dados.


Criação de volumes para arquivos do site e do banco de dados.

```
#Cria um volume para o Wordpress.
docker volume create wordp

#Criação do volume para o banco MySQL.
docker volume create dbm

#Verificação dos volumes em listagem.
docker volume ls
```


3- Criar uma rede para permitir uma conexão entre o banco e o site.

```
#Cria uma rede com o nome 'redefonte'.
docker network create redefonte

#Verificação da criação da rede em listagem.
docker network ls
```

4- Criar pastas para armazenar arquivos referentes ao projeto.

```
1- mkdir projetinho
2- cd projetinho

----------------------------------------------------------------------------------------

1- Cria uma diretório com o nome 'projetinho'
2- Entra no diretório especificado (Por mais leigo que seja, fazer uma estrutura para um projeto é essencial).
```

5- Checar a documentação  do docker-hub

```
https://hub.docker.com/_/wordpress
```

6- Criar uma abstração do banco de dados (Opcional).

```
|- DB NAME 'projetinho'
|-- DB USER 'cariani'
|-- DB PASSWORD '0311'
```

7- Criar um compose seguindo a documentação acima.

nano `docker-compose.yml`: 
```
services:
  web:
    image: wordpress
    restart: always
    ports:
      - "80:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: cariani
      WORDPRESS_DB_PASSWORD: 0311
      WORDPRESS_DB_NAME: projetinho
    volumes:
      - wordp:/var/www/html
    networks:
      - tunel

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: projetinho
      MYSQL_USER: cariani
      MYSQL_PASSWORD: 0311
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - dbm:/var/lib/mysql
    networks:
      - tunel

networks:
  tunel:
    driver: bridge

volumes:
  wordp:
  dbm:

```

8- Executar o compose, e após o teste apagar ele.

```
1- docker compose up -d

2- docker compose down

----------------------------------------------------------------------------------------
 
1- Executa o arquivo 'docker-compose.yml'
2- Exclui os containers gerados(Caso não tenha criado os volumes e a rede antes de executar, o mesmo irá criar as redes serão excluidas más os volumes permanecerão)
```

9- Resultado.