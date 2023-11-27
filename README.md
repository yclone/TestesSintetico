# 🚀 Bem-vindo ao Projeto de Testes Sintéticos!

<img loading="" src="https://www.svgviewer.dev/static-svgs/34448/docker.svg" width="40" height="40"/>
<img loading="" src="https://www.svgrepo.com/show/184143/java.svg" width="40" height="40"/>
<img loading="" src="https://www.svgrepo.com/show/333604/spring-boot.svg" width="40" height="40"/>
<img loading="" src="https://www.svgrepo.com/download/353625/cucumber.svg" width="40" height="40"/>
<img loading="" src="https://www.svgrepo.com/show/373699/jenkins.svg" width="40" height="40"/>
<img loading="" src="https://www.svgrepo.com/show/448457/grafana.svg" width="40" height="40"/>

</n></n>


![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat) ![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)



Você acabou de entrar no mundo incrível onde a magia dos testes sintéticos acontece! ✨ Este projeto foi criado com o propósito nobre de desvendar os mistérios por trás dos testes sintéticos de uma forma simples e educativa.

#### 🧪 O que esperar por aqui?
Prepare-se para uma jornada emocionante pelos corredores dos testes, onde cada linha de código é um passo mais perto da compreensão profunda dos testes sintéticos. Nossa missão? Fazer do processo de teste algo tão natural quanto um abraço de um amigo.

#### 💡 Por que sintéticos?
Porque adoramos a ideia de criar um ambiente de testes que seja mais brilhante que um unicórnio colorido! Os testes sintéticos são como a fada madrinha dos testes - eles aparecem, fazem a mágica acontecer e deixam tudo mais fácil.

#### 🎉 Junte-se a nós!
Quer ser parte dessa jornada? Clone este repositório e embarque na aventura dos testes sintéticos. Sua presença é mais do que bem-vinda - é essencial!

Vamos transformar o mundano em extraordinário, uma linha de código por vez.🚀❤️




## 📋 Vamos por partes

1. 🐳 [Criando as imagens docker](#criando-as-imagens-docker)
2. 📅 [Copiando os volumes do docker](#copiando-volumes)
3. 🚀 [Dando um UP nos container](#dandoup-containers)
4. 🧪 [Tests](#tests)

</n>
</n>

## <a name="criando-as-imagens-docker">🐳 CRIANDO AS IMAGENS DOCKER</a>

primeiro eu tenho que criar todas as imagens que eu vou usar para mostrar o exeplo de aplicação com testes sinteticos, que são:

#### ▶️ Commands
```bash
# frontend de teste
git clone --recursive git@github.com:yclone/PetFront.git
docker build -t pet-front -f PetFront/Dockerfile PetFront
	
# backend de teste
git clone --recursive git@github.com:yclone/PetBackend.git
docker build -t pet-backend -f PetBackend/Dockerfile PetBackend

# imagem do projeto de teste do backend
git clone --recursive git@github.com:yclone/apiSintetico.git
docker build -t backend-sintetico -f apiSintetico/Dockerfile apiSintetico

# imagem do projeto de teste do Frontend
git clone --recursive git@github.com:yclone/webSintetico.git
docker build -t web-sintetico -f webSintetico/Dockerfile webSintetico

# imagem do jenkins com o docker instalado
docker build -t custom-jenkins-docker -f custom-jenkins/Dockerfile custom-jenkins

```
🚀🚀
</n>
</n>
## <a name="copiando-volumes">📅 COPIANDO OS VOLUMES DO JENKINS, GRAFANA E INFLUXDB </a>

nesse momento eu tenho que baixar os volumes do jenkins, grafana e influxdb2 e depois importar para o meu DOCKER

### ▶️ Commands

* [Grafana](https://drive.google.com/file/d/1SiQxVrVLUx7LflFvbiwStCKKiaq-J3BC/view?usp=drive_link) 
* [Influx](https://drive.google.com/file/d/1XbzbeLVHQ9ky2vzD5KxN-8781WHn6-F-/view?usp=drive_link) 
* [Jenkins](https://drive.google.com/file/d/1XLAzddXAj-428q-YE7Taa9JG2vrQGd7W/view?usp=drive_link) 

🚀🚀


<b> os nomes dos volumes devem ser: </b>
* grafana-storage
* influxdb-storage
* jenkins-data

#### Recomendo utilizar uma extenção do Docker Desktop de importação de volumes chamada "Volumes Backup & Share"
https://www.docker.com/blog/back-up-and-share-docker-volumes-with-this-extension/
</n>
</n>

## <a name="dandoup-containers">🚀 DANDO UM UP NOS CONTAINERS </a>

agora é só subir o compose e temos todas as imagens criadas e prontas para serem utilizadas!

#### ▶️ Commands
```bash
docker-compose up -d
```

para acessar cada container na maquina basta entrar no navegador com as seguintes URLS:

#### ▶️ Links, users, pass, etc.
```bash
# FRONTEND
http://localhost:8000/

# BACKEND
http://localhost:8080/user
curl --request POST \
  --url http://localhost:8080/user \
  --header 'Content-Type: application/json' \
  --header 'User-Agent: Insomnia/2023.5.6' \
  --data '{
		"username": "teste@teste.com",
		"email": "f4594430-7b45-402f-89ad-dded69e2a776@teste.com",
		"nome": "Teste",
		"sobrenome": "Teste",
		"password": "2cc3a653-96bf-4080-9562-744fc8ef4684"
}'

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


# ✨EXTRAS

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


Contato
Se você tiver alguma dúvida ou problema, por favor, entre em contato comigo pelo e-mail vinicius_marra@hotmail.com.


# :

4. 🚀 [Build](#build)
5. 🐳 [Docker](#docker)
6. 💯 [Tests](#tests)
7. ☑️ [Code analysis and consistency](#code-analysis-and-consistency)
8. 📈 [Releases & Changelog](#versions)
9. ✨ [Misc commands](#misc-commands)
10. ©️ [License](#license)
11. ❤️ [Contributors](#contributors)