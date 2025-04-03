# Configuração de Servidor Web utilizando o Docker

### Aplicações utilizadas:

### GitHub, Amazon Web Services, Microsoft Store, WSL, Visual Studio Code, Docker.

<div align="center">
  <br>
  <a href="https://github.com/">
    <img src="/Projeto-WordPress-AWS-CompassUOL/imgs/gitlogo.png" alt="GitHub" width="150">
  </a>&ensp;

  <a href="https://www.googleadservices.com/pagead/aclk?sa=L&ai=DChcSEwjKuL74ltWLAxXoEUQIHY40KqwYABAAGgJkeg&co=1&ase=2&gclid=CjwKCAiA5eC9BhAuEiwA3CKwQp-uZ-EhfKVs_yaTVCZmvhF8olLyCz4sF_rQXc-KTkKjJ6zjkq_KbRoCmx0QAvD_BwE&ei=46i4Z7zJLbLb5OUP_NnOYQ&ohost=www.google.com&cid=CAESVeD2mSl7f0Xe0yyJImaMygYDsAuUvVqE8TXk7HbEuO8df6HhHkyj13nbeuQIUd6NDilzCovM3hpvmJWnXIKlBj1rDcr0Uva9DVYGZCTyi2T-YG-tn0A&sig=AOD64_3dqO5hHHx21zCm5ROWF8TSPV62pA&q&sqi=2&nis=4&adurl&ved=2ahUKEwj8xrT4ltWLAxWyLbkGHfysMwwQ0Qx6BAgIEAE">
    <img src="/Projeto-WordPress-AWS-CompassUOL/imgs/amazonicon.webp" alt="Amazon Web Services" width="150" height="150">
  </a>&ensp;

  <a href="https://apps.microsoft.com/home?hl=pt-BR&gl=BR">
    <img src="/Projeto-WordPress-AWS-CompassUOL/imgs/micstorelogo.png" alt="Microsoft Store" width="150" height="150">
  </a>&ensp;

  <a href="https://www.microsoft.com/store/productId/9P9TQF7MRM4R?ocid=libraryshare">
    <img src="/Projeto-WordPress-AWS-CompassUOL/imgs/wsllogoo.png" alt="WSL" width="150" height="150">
  </a>&ensp;

  <a href="https://code.visualstudio.com/">
    <img src="/Projeto-WordPress-AWS-CompassUOL/imgs/vscodelogo.png" alt="Visual Studio Code" width="150" height="150">
  </a>&ensp;

  <a href="https://hub.docker.com/">
    <img src="/Projeto-WordPress-AWS-CompassUOL/imgs/dockerlogo.webp" alt="Nginx" width="150" height="150">
  </a>&ensp;
</div>

> [!IMPORTANT]
> As únicas aplicações específicas que se pede a utilização no projeto são o **GitHub**, **Amazon Web Services** e o **Docker**. As outras foram questão de preferência!

> [!TIP]
> - **GitHub:** Utilizado para a documentação do projeto.
> - **Amazon Web Services (AWS):** Utilizado para a criação da infraestrutura de TI.
> - **Microsoft Store:** Utilizado para baixar o WSL e o Ubuntu 24.04.
> - **WSL (Windows Subsystem for Linux):** Permite executar um ambiente Linux diretamente no sistema operacional Windows.
> - **Visual Studio Code:** Utilizado como editor de código e terminal.
> - **Docker:** Utilizado um container do wordpress como servidor web.

---

## Linguagens utilizadas:

### Bash, Markdown.

<div align="left">
  <br>
  <a href="https://www.gnu.org/software/bash/">
    <img src="https://github.com/Daijinpala/projeto_1/blob/main/logo/bashlogo.jpeg" alt="Bash" width="150" height="150">
  </a>&ensp;

  <a href="https://www.markdownguide.org/">
    <img src="https://github.com/Daijinpala/projeto_1/blob/main/logo/marklogo.png" alt="Markdown" width="150" height="150">
  </a>&ensp;
</div>

> [!IMPORTANT]
> Você pode utilizar a linguagem Python ao invés de Bash.

> [!TIP]
> - **Bash:** É uma linguagem de script e um interpretador de comandos.
> - **Markdown:** É uma linguagem de marcação leve.

---


O projeto consiste em utilizar uma instância na AWS que conterá o Docker (estamos usando o contêiner do WordPress), que por sua vez, teremos que fazer uma integração utilizando múltiplos serviços, sendo eles:

- EFS
- RDS
- CLB/ALB
- ASG
- CloudWatch

```
1. Instalação e configuração do DOCKER ou CONTAINERD no host EC2; SEGUIR DESENHO TOPOLOGIA DISPOSTA. `Ponto adicional para o trabalho utilizar a instalação via script deStart Instance (user_data.sh)`

2. Efetuar Deploy de uma aplicação Wordpress com: container de aplicação RDS database Mysql. 

3. Configuração da utilização do serviço EFS AWS para estáticos do container de aplicação Wordpress .

4. Configuração do serviço de Load Balancer AWS para a aplicação Wordpress.

```

![1](png/print.png)

<hr>