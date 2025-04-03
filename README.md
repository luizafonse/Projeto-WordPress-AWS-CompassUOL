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