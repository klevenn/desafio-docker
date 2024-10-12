# desafio-docker

Este repositório contém um arquivo docker-compose.yml que configura um ambiente de contêineres utilizando o Docker. O ambiente inclui um proxy reverso com Nginx e vários serviços web, formando uma aplicação web robusta. A versão utilizada é a 3.8, que permite recursos avançados do Docker Compose.
Serviços
1. Nginx (Proxy Reverso)

    Imagem: nginx:alpine
    Volumes:
        Mapeia nginx.conf para configurar o Nginx.
        Mapeia um diretório para armazenar logs do Nginx.
    Portas: Expõe a porta 8080 do host para a porta 80 do contêiner, servindo como ponto de entrada da aplicação.
    Nome do Contêiner: servidor-proxy
    Rede: Conectado à app-network.
    Verificação de Saúde: Realiza chamadas HTTP a localhost a cada 10 segundos para garantir o funcionamento do serviço.

2. web

    Construção: Baseada no diretório ./base.
    Rede: Conectado à app-network.
    Verificação de Saúde: Verifica a saúde a cada 10 segundos.
    Nome do Contêiner: pagina-estatica.

3. web1

    Construção: Baseada no diretório ./base1.
    Rede: Conectado à app-network.
    Verificação de Saúde: Igual ao serviço anterior.
    Nome do Contêiner: pagina-estatica1.

4. web2

    Construção: Baseada no diretório ./base2.
    Rede: Conectado à app-network.
    Verificação de Saúde: Igual aos serviços anteriores.
    Nome do Contêiner: cep.

5. db

    Imagem: mysql:5.7
    Variáveis de Ambiente: Configurações do banco de dados, incluindo credenciais.
    Volumes: Persistência dos dados do MySQL em db_data.
    Rede: Conectado à app-network.
    Verificação de Saúde: Realiza uma verificação de ping no MySQL a cada 10 segundos.
    Nome do Contêiner: banco-mysql.

Volumes

    db_data: Usado para persistir dados do banco de dados.
    nginx_logs: Armazena logs do Nginx.

Redes

    app-network: Rede do tipo bridge, permitindo comunicação entre contêineres.

Conclusão

Este ambiente Docker configura uma aplicação web onde o Nginx atua como um proxy reverso, gerenciando o tráfego para vários serviços web e garantindo escalabilidade e manutenção. O banco de dados MySQL é incluído com persistência de dados. As verificações de saúde garantem que todos os serviços estejam operacionais, proporcionando uma experiência confiável ao usuário.