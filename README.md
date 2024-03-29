# 🚀 Bem-vindo ao Projeto de Testes Sintéticos!
[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)

![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat) ![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)

<img loading="" src="https://www.svgviewer.dev/static-svgs/34448/docker.svg" width="40" height="40"/> <img loading="" src="https://www.svgrepo.com/show/184143/java.svg" width="40" height="40"/> <img loading="" src="https://www.svgrepo.com/show/333604/spring-boot.svg" width="40" height="40"/> <img loading="" src="https://www.svgrepo.com/download/353625/cucumber.svg" width="40" height="40"/> <img loading="" src="https://www.svgrepo.com/show/373699/jenkins.svg" width="40" height="40"/> <img loading="" src="https://www.svgrepo.com/show/448457/grafana.svg" width="40" height="40"/>


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
5. ✨ [EXTRAS](#EXTRAS)
6. 🤝 [Contribuindo](#Contribuindo)
7. 👀 [Contato](#Contato)
7. ⚠️ [License](#License)

</n>
</n>

## <a name="criando-as-imagens-docker">🐳 CRIANDO AS IMAGENS DOCKER</a>

primeiro eu tenho que criar todas as imagens que eu vou usar para mostrar o exeplo de aplicação com testes sinteticos, que são:

#### ▶️ Commands
```bash
# frontend de teste
git clone --recursive https://github.com/yclone/PetFront.git
docker build -t pet-front -f PetFront/Dockerfile PetFront
	
# backend de teste
git clone --recursive https://github.com/yclone/PetBackend.git
docker build -t pet-backend -f PetBackend/Dockerfile PetBackend

# imagem do projeto de teste do backend
git clone --recursive https://github.com/yclone/apiSintetico.git
docker build -t backend-sintetico -f apiSintetico/Dockerfile apiSintetico

# imagem do projeto de teste do Frontend
git clone --recursive https://github.com/yclone/webSintetico.git
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
* <b>Frontend =</b> http://localhost:8000/

* <b>Brackend =</b> http://localhost:8080/user
```bash
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
```
* <b> Jenkins = </b> http://localhost:8081/
```bash
    USER: vinicius_marra
    PASS: SuperSecret
```
* <b> Grafana =</b> http://localhost:3000/ 
```bash
    USER: admin
    PASS: admin
```
* <b> Influxdb =</b> http://localhost:8086/
```bash
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

#### JMETER

para rodar os testes com o jmeter é necessario instalar os seguintes plugins:

* 3 Basic Graphs
* Custom Thread Groups
* Throughput Shaping Timer

depois é só abri o projeto e executar, esta configurado para exexutar com 100 threads em 100 ms

#### Passos para simular os erros:
PARAR O CONTAINER DO BACKEND
EXECUTAR OS TESTES NO JMETER PARA PODER GERAR OS ALERTAS
VALIDAR OS ALERTAS GERADOS


## <a name="Contribuindo"> 🤝 Contribuindo </a>

Solicitações pull são bem-vindas. Para mudanças importantes, abra um problema primeiro
para discutir o que você gostaria de mudar.


## <a name="Contato"> 👀 Contato </a>
Se você tiver alguma dúvida ou problema, por favor, entre em contato comigo pelo [Linkedin](https://www.linkedin.com/in/vinicius-marra-santos-20b17949/) ou pelo e-mail vinicius_marra@hotmail.com.

## <a name="License">⚠️ License </a>

[MIT](https://github.com/yclone)