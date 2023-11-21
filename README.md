Projeto de Submódulos
Este projeto é um exemplo de como usar submódulos no Git. Ele contém dois submódulos:

CRIANDO AS IMAGENS DOCKER
primeiro eu tenho que criar todas as imagens que eu vou usar na aplicação, que são:

um frontend de teste
um backend de teste
uma imagem do projeto de teste do backend
uma imagem do projet ode teste do Frontend
uma imagem do jenkins com o docker instalado

COPIANDO O VOLUME DO JENKINS

nesse momento eu tenho que pegar o volume do jenkins existe e copiar para maquina que vai executar os testes
depois de copiar o volume é possivel acessar o jenkins já configurado, com as execuçãoes de teste programadas e os builds configurados

SUBINDO TODOS OS CONTAINERS

agora eu tenho que subir o compose que eu executo essas imagens todas dentro de uma mesma rede

para acessar cada container na maquina basta entrar no navegador com as seguintes URLS:

FRONTEND = http://localhost:8000/
BACKEND = http://localhost:8080/user
jENKINS = http://localhost:8081/

SUBIR GRAFANA

usuario: admin
senha: admin

Influx DB
usuario: sintetico Test
senha: admin123
Bucket: k6sintetico
organization:  Testes Sinteticos
Token: SwhyVBasxMxplf49VwJYL-ZReMPHmVikcrV_2S2naOh4tfSurvA-EKQ1KpqrVPHquurSbZHjNktfODjtGQM8Qg==


proximos passos:

 * criar o grafana com influx DB para os testes de carga


rodar ferramenta de teste de carga
ver se vale a pena colocar em um container para poder rodar com o jenkins durante a apresentação

ver como o K6 se conecta com o influx db

ver se tem algum painel pronto para o K6

criar um painel que valida o tempo de resposta da aplicação e rodar o teste de carga e ver o painel mostrando o aumento no tempo de resposta

criar um alerta para um tempo de resposta grande, que vai acontecer durante a execuação do teste de performance











pet-front: Um projeto que contém o front-end da aplicação.
pet-backend: Um projeto que contém o back-end da aplicação.
Como usar
Para clonar o repositório e seus submódulos, execute o seguinte comando:

git clone --recursive https://github.com/yclone/PetFront
Isso irá clonar o repositório principal e seus submódulos.

Para criar as imagens Docker dos projetos front-end e back-end, execute os seguintes comandos:

docker build -t pet-front pet-front
docker build -t pet-backend pet-backend
Isso irá criar duas imagens Docker, uma para o front-end e outra para o back-end.

Para subir as aplicações, execute o seguinte comando:

docker-compose up -d
Isso irá subir as aplicações front-end e back-end, bem como o banco de dados.

Para parar as aplicações, execute o seguinte comando:

docker-compose down
Comandos úteis
Os seguintes comandos podem ser úteis para trabalhar com este projeto:

Para entrar na imagem Docker e fazer testes via SSH:
docker run -d {IMAGEM} sleep infinity
docker exec -it {ID DO CONTAINER} /bin/bash
Para subir o Selenium na porta 8888:
java -jar selenium-server-4.13.0.jar standalone --port 8888
Para criar a imagem Docker dos testes de front:
docker build -t web-sintetico .
Para rodar os testes de front:
docker run --network dev_sinteticos-network --ip 172.18.0.55 --rm web-sintetico mvn clean test
Para criar a imagem Docker dos testes de backend:
docker build -t backend-sintetico .
Para rodar os testes de backend:
docker run --network dev_sinteticos-network --ip 172.18.0.56 --rm backend-sintetico mvn clean test
Jenkins
Para usar o Jenkins com este projeto, você precisará configurar um pipeline para rodar os testes e construir as imagens Docker.

Contato
Se você tiver alguma dúvida ou problema, por favor, entre em contato comigo pelo e-mail vinicius_marra@hotmail.com.