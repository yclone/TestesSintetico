# Projeto de Submódulos

este é um projeto criado para apresentar o conceito de testes sinteticos

<img loading="lazy" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" width="40" height="40"/>

## 📋 Vamos por partes

1. 🐳 [Criando as imagens docker](#criando-as-imagens-docker)
2. 📅 [Copiando os volumes do docker](#copiando-volumes)
3. 🚀 [Dando um UP nos container](#dandoup-containers)
4. 🧪 [Tests](#tests)

## <a name="criando-as-imagens-docker">🐳 CRIANDO AS IMAGENS DOCKER</a>

primeiro eu tenho que criar todas as imagens que eu vou usar para mostrar o exeplo de aplicação com testes sinteticos, que são:

#### ▶️ Commands
```bash
# frontend de teste
docker build -t pet-front .
	
# backend de teste
docker build -t pet-backend .

# imagem do projeto de teste do backend
docker build -t backend-sintetico .

# imagem do projeto de teste do Frontend
docker build -t web-sintetico .

# imagem do jenkins com o docker instalado
docker build -t custom-jenkins-docker .

```
🚀🚀

## <a name="copiando-volumes">📅 COPIANDO OS VOLUMES DO JENKINS, GRAFANA E INFLUXDB </a>

nesse momento eu tenho que pegar o volume do jenkins, grafana e influxdb2

### ▶️ Commands
```bash

Grafana - https://drive.google.com/file/d/1SiQxVrVLUx7LflFvbiwStCKKiaq-J3BC/view?usp=drive_link
Influx - https://drive.google.com/file/d/1XbzbeLVHQ9ky2vzD5KxN-8781WHn6-F-/view?usp=drive_link
Jenkins - https://drive.google.com/file/d/1XLAzddXAj-428q-YE7Taa9JG2vrQGd7W/view?usp=drive_link
```
🚀🚀

#### Recomendo utilizar a ferramenta de importação do Docker chamada "Volumes Backup & Share"

## <a name="dandoup-containers">🚀 DANDO UM UP NOS CONTAINERS </a>

agora é só subir o compose e temos todas as imagens criadas e prontas para serem utilizadas!

#### ▶️ Commands
```bash
docker-compose up -d
```

para acessar cada container na maquina basta entrar no navegador com as seguintes URLS:

#### ▶️ Commands
```bash
# FRONTEND
http://localhost:8000/

# BACKEND
http://localhost:8080/user

#jENKINS
http://localhost:8081/
    USER: vinicius_marra
    PASS: SuperSecret

#GRAFANA
http://localhost:3000/
    USER: admin
    PASS: admin

#INFLUXDB
http://localhost:8086/
    USER: sintetico Test
    PASS: admin123
    Bucket: sinteticoTestJmeter
    BucketK6: k6sintetico
    organization:  Testes Sinteticos
    Token: SwhyVBasxMxplf49VwJYL-ZReMPHmVikcrV_2S2naOh4tfSurvA-EKQ1KpqrVPHquurSbZHjNktfODjtGQM8Qg==
```

## <a name="tests">🧪 EXECUTANDO OS TESTES</a>

#### 📣 ATENÇÃO

<b>para verificar os alertas é necessario:
* configurar o jenkins com o plugin do teams
* criar uma equipe para receber os alertas
* adicionar no teams o plugin do jenkins para os teses das pipelines
* adicionar no teams o plugin do grafana para os alertas do grafana
</b>


PASSOS:
PARAR O CONTAINER DO BACKEND
EXECUTAR OS TESTES NO JMETER OU NO K6 PARA PODER GERAR OS ALERTAS
VALIDAR OS ALERTAS GERADOS


# EXTRAS

## JMETER

para rodar os testes com o jmeter é necessario instalar os seguintes plugins:


## K6
para rodar os testes do K6 com o conector do influx é necessario instalar o Go
entra dentro da pasta do teste de performance e executa os comandos:
### Install xk6
go install go.k6.io/xk6/cmd/xk6@latest

### Build the k6 binary
xk6 build --with github.com/grafana/xk6-output-influxdb

para executar o teste basta dar o comando (esse comando esta no site do K6, ele funciona para o influxdb2):
#### ▶️ Commands
```bash
$ K6_INFLUXDB_ORGANIZATION="Testes Sinteticos" K6_INFLUXDB_BUCKET="k6sintetico" K6_INFLUXDB_TOKEN="SwhyVBasxMxplf49VwJYL-ZReMPHmVikcrV_2S2naOh4tfSurvA-EKQ1KpqrVPHquurSbZHjNktfODjtGQM8Qg==" K6_INFLUXDB_ADDR="http://localhost:8086" ./k6 run scenarios/Get-health.js -o xk6-influxdb
```




# proximos passos:

4. 🚀 [Build](#build)
5. 🐳 [Docker](#docker)
6. 💯 [Tests](#tests)
7. ☑️ [Code analysis and consistency](#code-analysis-and-consistency)
8. 📈 [Releases & Changelog](#versions)
9. ✨ [Misc commands](#misc-commands)
10. ©️ [License](#license)
11. ❤️ [Contributors](#contributors)


criar um alerta para um tempo de resposta grande, que vai acontecer durante a execuação do teste de performance


Como usar
### Para clonar o repositório e seus submódulos, execute o seguinte comando:

git clone --recursive https://github.com/yclone/PetFront
Isso irá clonar o repositório principal e seus submódulos.

Para criar as imagens Docker dos projetos front-end e back-end, execute os seguintes comandos:


Para subir as aplicações, execute o seguinte comando:


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