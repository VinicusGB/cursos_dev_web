# API com Django 3: Versionamento, cabeçalhos e CORS - 6h
**Professor:** Guilherme Lima

**Disponível:** [ALURA]('https://cursos.alura.com.br/course/api-django-3-versionamento-cabecalhos-cors')

**Conteúdo:**
- Aprenda na prática o que é versionamento de API
- Saiba como definir diferentes níveis de permissões de usuários
- Aprenda como limitar o número de requisições dos recursos
- Inclua informações extras no cabeçalho das requisições
- Descubra como integrar uma API Django com um React front-end

## 1. Versionamento
### Apresentação

[00:00] Meu nome é Guilherme Lima e seja muito bem-vindo ao treinamento de Django REST Framework: Versionamento de API. O que nós vamos fazer nesse curso?

[00:09] Nesse curso vamos pegar o modelo do projeto criado no curso 1 de API, só que com algumas alterações que vamos ver e vamos aprender como criar versionamento de API, como eu atualizo a minha API sem perder os endpoints que já estavam funcionando.

[00:28] Vamos aprender também como lidar com níveis de permissões diferentes na nossa API. Então um determinado usuário vai poder realizar certas ações, outro usuário vai fazer outras ações, como fazemos isso aqui no Django REST.

[00:43] Vamos entender também como lidar com permissões de uma forma um pouco diferente, como conseguimos limitar o número de requisições de um determinado recurso da nossa API ou o uso até da nossa API mesmo. Então eu vou falar: “Se for um usuário anônimo, vou permitir 50 requisições, cinco requisições”. Vamos aprender isso nesse curso também.

[01:03] E vamos aprender sobre modelo de maturidade, como deixamos nossas APIs REST com um nível de maturidade um pouco maior. E para finalizar esse curso, vamos integrar a nossa API, desenvolvida com o Python e Django REST, com uma API desenvolvida com React.

[01:21] Então temos na nossa API alunos, cursos, matrículas e nessa parte de cursos eu quero conectar a minha API que está funcionando local com uma aplicação local também, desenvolvida em React. O que acontece? Quais são os passos necessários para eu conseguir ligar a minha API React com a minha API Django REST Framework?

[01:43] Sabendo de tudo isso, o que teremos em mente durante esse treinamento? Vamos disponibilizar um projeto inicial e todos os passos dados serão bem guiados para vocês, para que todo mundo consiga seguir esse treinamento.

[02:00] Esse projeto em React, nós vamos entregar para vocês, mas o nosso foco principal é a parte do Django REST, não vamos mexer em nenhuma linha de código do React, vamos simplesmente executar o comando, instalar o que é necessário para o React funcionar e executar o comando para subir o nosso servidor.

[02:18] E vamos ver quais são as implicações, o que acontece, como eu faço um projeto em uma linguagem conversar com outro projeto, o front-end com oback-end, tudo isso nós veremos nesse curso.

[02:31] Eu espero que você se sinta empolgado, eu super recomendo que você tenha visto os cursos anteriores de Django. Se você viu e se você está preparado para esse desafio, eu te convido a começar esse treinamento.

### Preparando o ambiente

Olá!
É muito bom receber você neste curso de API com Django 3: Versionamento, cabeçalhos e CORS.

Espero que seja uma experiência de aprendizado incrível, e que possamos vencer todos os desafios juntos. Neste curso, aprofundar nossos conhecimentos no Django Rest Framework e aprender como versionar a API, incluir diferentes níveis de permissões, CORS e como integrar um frontend REACT com a API.

Preparando ambiente
Além disso, para que tenhamos o mesmo resultado, é recomendado que você faça o download da mesma versão do Python e do Django que utilizei quando o curso foi gravado, que poderá ser encontrada aqui:

    Python 3.7.4
    Django 3.0.7

O Django pode ser instalado através do comando:

    pip install Django==3.0.7

Este projeto é inspirado no projeto do curso API com Django 3, porém não é uma continuação.

Sendo assim, para o acompanhamento é altamente recomendado realizar o download do projeto base [neste link]('https://github.com/guilhermeonrails/drf-escola-projeto_inicial/archive/master.zip'), e na próxima atividade, seguir os passos para carregar o projeto e aprender muito.

Em caso de dúvidas durante o curso, conte com o fórum da Alura, pois sua questão pode ser respondida pela nossa comunidade!

:)

### Carregando o projeto

[00:00] Vamos iniciar então os nossos estudos de API com Django REST? Nós queremos evoluir uma API. Eu tenho uma API que está funcionando e eu quero incluir novas funcionalidades, novos recursos, remover um determinado recurso.

[00:15] E o que eu preciso fazer? Primeiro lugar, precisamos de uma API. Pensando nisso, na atividade anterior temos um link para você fazer download do projeto base que vamos utilizar no decorrer de todo esse treinamento.

[00:29] Eu já fiz o download desse projeto, vou renomear esse projeto para “drf-clientes”, já que vamos trabalhar com a ideia de outros clientes consumindo os recursos da nossa API, então vou deixar “drf-clientes”.

[00:47] Vou abrir o VS Code como editor de código. Arrastando o projeto aqui para dentro, temos esse projeto aqui. Podemos dar uma olhada, é um projeto de escola, onde temos nos nossos modelos um aluno, um curso e fazemos as matrículas, vinculando o aluno e o curso, e indicando o período dessa matrícula.

[01:13] Mas como eu carrego esse projeto aqui na minha máquina? Que ele já é um projeto que foi feito. Nós utilizamos como referência o projeto criado na primeira parte do nosso curso de Django REST Framework, então ele é um projeto referência, existem algumas mudanças e eu recomendo que você também faça o download e continue o projeto a partir desse stage que temos aqui.

[01:40] Fizemos o download do projeto, primeira coisa que vamos fazer para carregar outro projeto Django é criar um ambiente virtual para ele.

[01:48] Se observarmos, temos aqui à esquerda a “escola”, o “setup”, onde ficam todas as configurações desse projeto, temos o “manage.py”, temos um arquivo chamado “requirements.txt”, onde vamos listar todas as dependências e módulos necessários para esse projeto, e temos aqui um arquivo chamado “seed.py”, que eu já vou falar dele.

[02:08] A primeira coisa que vamos fazer vai ser criar um ambiente virtual para esse projeto aqui. O que eu vou fazer? Vou fechar esse aqui, “seed.py”, só para ficarmos com a tela mais limpa e vou jogar nosso terminal aqui para cima.

[02:19] Para criarmos um ambiente virtual, assim como vimos em todos os cursos de Django, python -m venv ./venv. Dou um “Enter” aqui, nós veremos que vai aparecer uma “venv” aqui à esquerda, uma pasta, era o que queríamos. O que eu vou fazer agora vai ser ativar essa minha venv. Para ativar, source venv/bin/activate. Dou um “Enter” e eu ativei a minha venv.

[02:53] O que eu preciso fazer agora? Eu preciso pegar todas as dependências deste projeto e instalar nesse ambiente virtual que eu acabei de criar. Como eu faço isso? Para instalar as dependências, pip install.

[03:06] Para eu pegar todas as dependências desse meu arquivo e conseguir instalar nesse meu ambiente virtual, o que eu vou fazer? Vou utilizar a flag -r e vou passar o nome desse arquivo aqui, requirements.txt. E quando eu dou um “Enter” ele vai pegar todas essas dependências, tudo que o meu projeto precisa para funcionar, e vai instalar nesse meu ambiente virtual.

[03:34] Lembrando que estamos na fase 1 do nosso projeto, nós queremos evoluir uma API, qual API? Essa API que estamos instalando aqui e fazendo as configurações na nossa máquina.

[03:45] Fiz aqui a instalação, vou atualizar o pip com o comando pip install --upgrade pip’. Se essa mensagem não apareceu para você, não se preocupe você continua no próximo passo que houver aqui.

[04:00] Então já instalamos as dependências, se eu coloco aqui pip freeze, vamos poder visualizar aqui as mesmas dependências descritas no “requirements.txt”, que são as dependências que temos aqui também.

[04:14] Lembra que eu mostrei para vocês que nesse app de escola eu tenho modelos que têm aluno, que têm cursos e matrículas? Eu preciso agora criar o meu banco de dados para manter esses recursos também.

[04:29] Para eu gerar o script para criar no banco de dados, já sabemos, vou utilizar python manage.py makemigrations. Vou dar um “Enter” e ele vai gerar as migrações. Ele criou o script, agora eu preciso de fato pegar esses scripts e criar a minha base de dados, então eu uso python manage.py migrate, quando eu dou um “Enter” ele vai aplicar todas as migrações.

[04:56] O que eu vou fazer agora? Eu vou subir o meu servidor, python manage.py runserver e vou abrir aqui uma nova aba, no “localhost:8000”, e temos alunos, cursos e matrículas. Quando eu clico em “alunos”, ele pede uma senha. Precisamos criar uma senha de super usuário para conseguir navegar na nossa API.

[05:22] O que eu vou fazer? Vou parar o meu servidor, depois eu o carrego mais uma vez. E para criarmos um superusuário, nós utilizamos o comando python manage.py createsuperuser.

[05:41] O nome que eu vou dar para ele é um nome super simples, para facilitar o nosso ambiente de desenvolvimento, então vou deixar só o “gui”, não vou colocar e-mail, vou colocar a senha mais simples. A senha mais simples de novo, ele falou que a senha é muito curta, você já sabe qual senha eu coloquei, eu dou aqui um y que quero confirmar e eu criei o meu super usuário.

[05:58] Vou rodar mais uma vez o meu servidor, abrindo aqui o “localhost:8000/alunos/”. Deixa eu voltar aqui, vou clicar em “alunos” para eu visualizar, vou colocar o “gui”, que é o usuário que eu criei, e a senha que você já sabe qual é, e não temos nenhum aluno aqui. Podemos dar um post para criar.

[06:16] Só que esse tempo de criarmos aluno, ficarmos criando cursos e matrículas na mão, vamos gastar um tempo não necessário, queremos focar em coisas novas no nosso treinamento. Então o que eu fiz?

[06:28] Temos aqui um script chamado “seed.py”. Esse script vai nos gerar uma determinada quantidade de alunos e cursos, e ele não vai nos gerar uma quantidade de matrículas, por quê? Isso nós veremos no decorrer do curso e vamos criando no decorrer do nosso treinamento. Eu quero rodar esse script e gerar aqui 200 alunos e cinco cursos. Como eu faço?

[06:53] Lá no meu terminal, deixa eu parar o meu terminal de novo, eu vou utilizar o comando python para rodar esse script passando o nome dele, python seed.py. Quando eu dou um “Enter” não apareceu nenhuma mensagem.

[07:09] Vou rodar meu servidor de novo, abrindo a nossa lista de alunos, quando eu atualizar observe que agora eu tenho uma lista com 200 alunos. Vou scrollar tudo aqui, para vermos lá no final, 200 alunos. E se eu for em “cursos”, eu tenho todos os cursos também que eu criei, tem cinco cursos diferentes.

[07:32] O que eu quero fazer agora? Temos a nossa API funcionando, eu preciso incluir novos recursos, eu preciso incluir novas funcionalidades na minha API, porém eu preciso garantir que as pessoas e sistemas que já consomem a minha API vão continuar utilizando. Eu não posso criar uma API nova e não posso colocar as mudanças que eu quero na minha API local.

[07:53] No próximo vídeo vamos entender como existem formas diferentes de evoluirmos a nossa API e criar versões da nossa API, garantindo que essas novas funcionalidades funcionem para os clientes que precisem consumir nossa API e os clientes que já utilizavam as versões anteriores vão continuar utilizando a nossa API. Isso nós veremos a seguir.

### Tipos de Versionamento

O DJANGO-REST possui o versionamento de API, onde é possivel adicionar novas funcionadlidades e criar uma nova versão da API sem inutilizar a versão anterior. 5 tipos:

- **AcceptHeaderVersioning**
    - _Transferência do número da versão através do cabeçalho da requisição._
        
            GET /alunos/ HTTP/1.1
            Host: exemplo.com
            Accept: application/json; version=1.0

- **URLPathVersioning**
    - _Adiciona a versão no endereço do recurso de uma variável (o caminho é especificado no DRF por meio do parâmetro VERSION_PARAM)._

            urlpatterns = [
                url(r'^(?P<version>(v1|v2))/alunos/$', alunos_listname='alunos-lista'
                )
            ]

- **NamespaceVersionig**
    - _A versão é informada através do namespace da url._

            urlpatterns = [
                ulr(r'^v1/alunos/',include(alunos.urls', namespace='v1')),
                ulr(r'^v2/alunos/',include(alunos.urls', namespace='v2'))

            ]

- **HostNameVersioning**
    - _A versão é definida pelo nome de domínio._

            http://v1.exemplo.com/alunos/
            http://v2.exemplo.com/alunos/

- **QueryParameterVersioning**
    - _Transfere a versão através do parâmetro GET._

            http://exemplo.com/alunos/?version=1
            http://exemplo.com/alunos/?version=2

---

[00:00] Nessa aula vamos aprender o que é versionamento de API. Para começar, vamos pensar nesse seguinte cenário, já temos a nossa API funcionando e vamos imaginar que a nossa API funciona para dois tipos de clientes diferentes, um cliente mobile e um cliente web, um sistema web.

[00:17] E eu preciso atualizar a minha API incluindo novas funcionalidades ou outras informações dos recursos que disponibilizamos. Só que essas mudanças e essas novas funcionalidades nós não vamos colocar direto na API, vamos criar uma nova versão da nossa API.

[00:34] Isso não significa que vai ser uma API nova, vai ser outra versão da API que já temos, para atender os clientes que precisam dessas novas funcionalidades e continuar atendendo os clientes que já utilizavam a versão anterior da nossa API.

[00:50] No Django REST existem alguns tipos de versionamento que podemos escolher, dependendo da abordagem de cada cenário que nós vamos analisar aqui.

[01:01] Existe um tipo de versionamento chamado AcceptHeaderVersioning, o que ele significa? Nós passamos o número da versão através do cabeçalho da requisição. Então nós vamos fazer um get de alunos, por exemplo, e eu vou passar lá a versão específica que eu quero utilizar. Esse tipo tem esse nome, AcceptHeaderVersioning.

[01:22] Existe outro tipo também chamado URLPathVersioning, que nós vamos adicionar no recurso de uma variável a versão que queremos utilizar. Então teremos lá a nossa URL e vamos passar qual versão iremos utilizar, se é a versão 1 ou a versão 2 da nossa API. E lá na nossa view nós recuperamos esse valor através desse parâmetro “VERSION_PARAM”. Esse é outro tipo também.

[01:54] Temos outro tipo chamado NamespaceVersioning, então a versão é fornecida através do namespace da URL. Então temos “v1/alunos/’, include(aluno.urls’,namespace=’v1’))” e ele tem aqui as URLs e todos os arquivos responsáveis por aquela versão que estamos utilizando, ou a versão 2 e todos os arquivos responsáveis pela versão 2. Esse tipo se chama NamespaceVersioning.

[02:20] Existe outro também chamado HostNameVersioning, onde vamos incluir a versão da nossa API definida através do domínio, junto com o domínio do nosso host. Temos aqui “v1.exemplo.com/alunos/” ou “v2.exemplo.com/alunos/”.

[02:38] E existe outro tipo também chamadoQueryParameterVersioning, o que ele significa? Significa que vamos transferir, através do parâmetro get, a versão que queremos utilizar. Então eu tenho aqui o meu host “/alunos/?version=1” ou “version=2”.

[02:58] E por questão de tempo infelizmente nós não conseguimos mostrar na prática, criando vídeos, todos esses tipos de versionamentos de API, então vamos utilizar esse tipo aqui, QueryParameterVersioning.

[03:10] No próximo vídeo vamos criar um cenário onde eu preciso criar uma versão 2 da minha API, atendendo todos aqueles requisitos que eu já passei. Eu quero continuar atendendo os clientes que já utilizavam a minha API, que já consumiam os recursos, só que eu preciso incluir novas funcionalidades e eu vou utilizar esse QueryParameterVersioning no próximo vídeo.

### Query Parameter Versioning

1. Para utilizar ´QueryParameterVersioning´ devemos criar uma nova versão da class SERIALIZERS.py;
2. No VIEWS.PY devemos adicionar na ´class VIEWSETS´  um condicional para acessar versão correta do SERIALIZERS.py;
        
        class AlunosViewSet(viewsets.ModelViewSet):
            queryset = 
            authentication_classes = 
            permission_classes =
            def get_serializer_class(self):
                if self.request.version == 'v2':
                    return AlunoSerializerV2
                else:
                    return AlunoSerializer

3. No SETTINGS.PY devemos adicionar um novo parâmetro: [DOCUMENTAÇÃO]('https://www.django-rest-framework.org/api-guide/versioning/')

        REST_FRAMEWORK = {
            'DEFAULT_VERSIONING_CLASS': 'rest_framework.versioning.QueryParameterVersioning'
        }

---

[00:00] Vamos criar na prática o QueryParameterVersioning na nossa API? Como ele funciona? Nós vamos colocar “?version=” e vamos escolher a versão que estamos utilizando na nossa API.

[00:12] Para deixar esse exemplo mais prático, eu quero criar uma versão 2 da nossa API onde eu tenho mais um campo. Além desses campos que eu tenho aqui, eu quero ter o campo celular, porque um determinado cliente, outro sistema precisa dessa nova funcionalidade aqui nos recursos que nós disponibilizamos de alunos.

[00:31] O que eu vou fazer? Primeira coisa, vamos criar lá no nosso modelo um campo em aluno chamado celular, então vou chamar aqui celular, ele vai ser igual a um models.CharField, eu vou colocar aqui um (max_length=11, e vou colocar um valor default=””) para ele também, como uma string vazia.

[01:00] Criei aqui um novo campo, esse campo celular. Deixa eu tirar ali do lado, só para enxergarmos melhor. Então criei aqui o meu campo celular dentro do meu modelo aluno. O que eu vou fazer agora vai ser abrir o meu terminal, “Command + J”, vou abrir uma nova aba do terminal, deixa eu ativar a minha venv, source venv/bin/activate.

[01:33] No primeiro terminal aqui nós estamos rodando nosso servidor, no segundo eu quero rodar essa migração, eu quero realizar essas mudanças que eu fiz aqui no meu modelo lá no meu banco de dados.

[01:45] Então vou rodar o python manage.py makemigrations e ele vai falar: “Nós adicionamos um novo campo celular no aluno”, é isso que nós queríamos. Agora o que eu quero fazer é de fato incluir essa migração no banco de dados, python manage.py migrate, eu dou um “Enter” e ele aplicou essas migrações.

[02:08] O que eu vou fazer na sequência vai ser, lá no meu serializer eu tenho o meu serializer de aluno e eu vou criar o outro serializer para incluir esse novo recurso, que é o celular. Então eu vou copiar todo esse código, todas essas informações, vou colocar aqui embaixo, eu vou colar essa informação do nosso aluno.

[02:36] Então temos o AlunoSerializer, eu vou colocar aqui AlunoSerializerV2, para lembrarmos que é a versão 2 do nosso serializador de aluno. E depois temos nos campos o ID, o nome, vou colocar uma vírgula aqui, vou colocar o nosso campo novo, celular. Salvei.

[02:56] Agora lá na minhas views, vou dar aqui um “Command + P”, vou digitar “views”, aparece aqui a view de escola, nós temos o AlunosViewSet.

[03:04] E olha que interessante, já temos uma classe serializer específica, nós falamos assim: “A classe serializer para esse nosso ViewSet de aluno é o AlunoSerializer”. Não é o que queremos. Dependendo da versão da API que recebermos lá no nosso parâmetro, nós queremos exibir ou a versão 1, que é sem o celular, ou a versão 2, com o celular.

[03:30] Então o que eu vou fazer? Eu vou colocar esse código para baixo, eu segurei o “Option” para baixo e ele veio aqui. Então eu vou definir essa classe com base na versão que vamos utilizar na nossa API. Eu vou tirar esse código aqui, serializer_class = AlunoSerializer, e vou criar uma função onde eu vou definir o meu serializer.

[03:53] A função que define o serializer é get_serializer_class. E como parâmetro vamos passar a instância que estivermos utilizando, o (self):. E aqui dentro eu vou começar.

[04:08] Eu vou perguntar primeiro, se a requisição dessa instância for igual a V2, então if, requisição que está vindo, self.request.version == ‘v2’, quem queremos utilizar como serializer? O AlunoSerializerV2, então vou colocar aqui um return AlunoSerializerV2, nós precisamos trazê-lo aqui, então temos o AlunoSerializerV2 aqui em cima. Já fiz o import dele.

[04:57] Agora, se eu não passei nenhuma informação, se eu não tenho a versão 2 na requisição, o que eu quero fazer? else:, eu quero retornar o nosso AlunoSerializer que nós já tínhamos antes. Salvei essa informação.

[05:17] A última coisa que vamos precisar fazer agora vai ser indicar para as nossas configurações que a nossa API utiliza o QueryParameterVersioning.

[05:28] Então eu vou abrir os sets da nossa aplicação, venho aqui em cima, à esquerda, fechar a “escola”, “setup > settings.py”. Lá no final eu vou criar, na linha 124, um parâmetro chamado REST_FRAMEWORK =, tudo maiúsculo, e aqui vamos passar as configurações do REST_FRAMEWORK.

[05:58] Se formos lá na documentação e digitarmos “Versioning - Django REST Framework”, teremos na própria documentação da nossa API vários tipos explicando todos aqueles tipos de documentação que utilizamos.

[06:13] E observe que temos aqui um “’DEFAULT_VERSIONING_CLASS’”, que é o que precisamos, passando “’rest_framework.versioning”, só que não estamos utilizando “NamespaceVersioning”, que vimos no nosso primeiro vídeo, estamos utilizando o QueryParameterVersioning.

[06:29] Então vou procurá-lo aqui, vou digitar “QueryParameterVersioning”, que é esse cara aqui. Agora sim, copiei, .QueryParameterVersioning’, fechei. Abrindo o nosso terminal 1 para ver se está tudo certo. Recebemos uma mensagem, vou rodar mais uma vez, manage.py runserver, parece que está tudo ok. Vamos testar isso daqui.

[06:58] Estou no alunos, atualizei. E quando eu atualizei ele colocou essa versão 2, porque eu acho que eu já tinha no cache aqui marcado. Então coloquei “?version=v2”, ele já trouxe para mim o ID, nome e o celular, o celular está vazio, podemos incluir o celular depois nesses alunos. Mas você percebe que já temos esse campo celular.

[07:23] Agora, se eu não passo nenhuma informação e dou só um “/alunos/”, observe que aquele campo celular não está mais presente, nem para eu fazer o meu post.

[07:36] Conseguimos criar duas versões da nossa API, uma versão 2, onde incluímos esses novos recursos e uma versão 1, atendendo os clientes e serviços que já consumiam a nossa API.

### Para saber mais: Tipos de versionamento

No Django Rest, existem algumas formas de versionar uma API. Vejamos a seguir alguns exemplos:

- QueryParameterVersioning \
    - _Transfere a versão através do parâmetro version_

    Exemplo:

        http://exemplo.com/alunos/?version=1
        http://exemplo.com/alunos/?version=2

- HostNameVersioning \
    - _A versão é definida pelo nome de domínio_

    Exemplo:

        http://v1.exemplo.com/alunos/
        http://v2.exemplo.com/alunos/

- NamespaceVersioning \
    - _A versão é fornecida através do namespace da url_

    Exemplo:

        urlpatterns = [
            url(r'^v1/alunos/', include(alunos.urls', namespace='v1')),
            url(r'^v2/alunos/', include(alunos.urls', namespace='v2'))
        ]

- URLPathVersioning \
    - _Adiciona a versão no endereço do recurso de uma variável (o caminho é verificado através do parâmetro VERSION_PARAM)_

    Exemplo:

        urlpatterns = [
            url(r'^(?P<version>(v1|v2))/alunos/$', alunos_list
                name='alunos-lista'
            )
        ]

- AcceptHeaderVersioning \
    - Transferência do número da versão através do cabeçalho da requisição

    Exemplo:

        GET /alunos/ HTTP/1.1
        Host: exemplo.com
        Accept: application/json; version=1.0

Não podemos esquecer de incluir o tipo de versionamento na variável de ambiente do REST_FRAMEWORK no arquivo settings.py. Por exemplo:

    REST_FRAMEWORK = {
        'DEFAULT_VERSIONING_CLASS': 'rest_framework.versioning.QueryParameterVersioning',
    }

### Exercício: Vantagens do versionamento

Nesta aula, criamos um novo serializer que inclui o campo celular, conforme ilustra o código abaixo:

    class AlunoSerializerV2(serializers.ModelSerializer):
        class Meta:
            model = Aluno
            fields = ['id', 'nome', 'celular','rg', 'cpf', 'data_nascimento']

Mesmo assim, mantemos o serializer chamado AlunoSerializer que não possui o campo celular:

    class AlunoSerializer(serializers.ModelSerializer):
        class Meta:
            model = Aluno
            fields = ['id', 'nome', 'rg', 'cpf', 'data_nascimento']

Sabendo disso, analise as afirmações abaixo e indique aquela que contém a vantagem de versionar uma API.

a) Ao versionar uma API, a velocidade e desempenho das respostas dela são aumentados significativamente.

b) **Alternativa correta:** Os clientes existentes podem continuar a usar a versão antiga da API compatível com a nova versão.
- _Alternativa correta! Mudanças e novas funcionalidades devem ser implementadas nas novas versões da API, não apenas em uma mesma versão._

c) Ao versionar uma API, a velocidade e desempenho das respostas dela caem significativamente.

### O que aprendemos?

- Carregamos o projeto base local e executamos o arquivo seed.py, para criar alunos e cursos;
- Entendemos que no Django Rest Framework existem várias formas e versionar a API;
- Vimos na prática como versionar a API com Query Parameter Versioning.

## 2. Permissões
### Definindo permissões
Definição padrão do DJANGO ADMIN, adicionamos as permissões conforme necessidade.

---

[00:00] Neste vídeo vamos aprender na prática como funcionam as permissões no Django REST. E para isso vou criar dois tipos de usuários com permissões diferentes.

[00:09] A primeira vai ser a Ana, ela vai ser responsável pelas matrículas da nossa aplicação. Então todo recurso relacionado à matrícula a Ana vai ter permissão de criar novas matrículas, de atualizar, de editar, mas ela não vai poder deletar as matrículas.

[00:25] O mesmo eu quero para o Marcos, só que para outros recursos. Eu quero que o Marcos seja capaz de criar alunos, listar alunos, editar os alunos, criar cursos, editar cursos também, mas ele também não vai ser capaz de deletar os cursos nem os alunos. Vamos ver isso na prática como funciona?

[00:41] A primeira parte que vamos fazer vai ser configurar o admin do Django com essas seguintes permissões para cada usuário. Vamos começar pela Ana.

[00:50] Vou acessar o Django admin, “localhost:8000/admin”, vou colocar aqui o nome do meu super usuário e a minha senha, e eu vou vir em “Usuários” e nós vamos poder visualizar que temos um usuário só, que é o “gui”.

[01:06] Vou adicionar mais um usuário, que vai ser a usuária “Ana”. Vou criar uma senha para a Ana, vou confirmar a senha, vou salvar. Vou dar aqui o primeiro nome, vai ser “Ana”, último nome vai ser “Ana” também, o endereço de e-mail vou deixar sem nada por enquanto.

[01:27] Vou indicar que é um usuário ativo na nossa aplicação. Não vamos criar grupos de permissões, mas poderíamos fazer isso também, não faremos isso agora, eu só quero lidar com as permissões específicas para este usuário.

[01:41] Eu quero que a Ana seja capaz de cuidar dos recursos de matrículas, então vou falar aqui que a Ana vai poder adicionar uma nova matrícula, ela vai poder atualizar, mudar uma matrícula, visualizar uma matrícula, só que ela não vai poder deletar uma matrícula. E essas são as permissões da Ana. Eu venho aqui embaixo, dou um “Salvar” e eu criei a Ana.

[02:06] Vamos criar agora o usuário Marcos, que vai ser capaz de manter os recursos de alunos e cursos. “Adicionar usuário”, “Marcos”, vou criar uma senha para ele, vou salvar. Primeiro nome, “Marcos”, último nome vou deixar “Marcos” também.

[02:36] Scrollando para baixo, quais são as permissões do Marcos? O Marcos vai conseguir criar um aluno, alterar e visualizar um aluno. Ele vai poder adicionar curso, editar um curso, e visualizar um curso também. Vou passar isso aqui para o lado, então ele tem todos esses recursos.

[03:01] Observe que em nenhum momento nós falamos nem para o Marcos e nem para a Ana que eles podem deletar os recursos que eles gerenciam. Vou salvar aqui. Então eu tenho o Marcos e tenho a Ana.

[03:15] Do lado do admin do Django o que temos que fazer é isso. Agora o que vamos precisar fazer? E u vou precisar ir lá nas minhas views e falar que eu preciso desse modelo de permissões aqui do admin na minha aplicação mesmo. E é isso que nós vamos ver no próximo vídeo.

### Testando as permissões

Para que nossa API herde as permissões conforme as permissões do DJANGO-ADMIN, devemos:

1. No VIEWS.PY:

        ...
        from rest_framework.permissions import IsAuthenticated, DjangoModelPermissions

        class AlunosViewSet(viewsets.ModelViewSet):
            ...
            permission_classes = [IsAuthenticated, DjangoModelPermissions]
            ...

---

[00:00] Agora que nós criamos no lado do admin as permissões da Ana para manter os recursos de matrícula e do Marcos para manter recursos de alunos e cursos, como nós pegamos essas modificações que nós fizemos no Django admin e passamos para a nossa API?

[00:16] Então nós queremos que aquelas modificações, aquelas permissões que nós incluímos no admin tenham efeito aqui no lado da nossa API.

[00:23] Primeira coisa que vamos precisar fazer para testar isso é, desse módulo, rest_framework.permissions, vou colocar uma vírgula aqui, nós vamos importar outro módulo para indicar que queremos utilizar o modelo de permissões do Django. Eu vou escrever aqui DjangoModelPermissions, no plural.

[00:48] Trouxe o DjangoModelPermissions, o que eu vou fazer? Observe que temos uma classe de permissões e dentro dessa classe temos uma verificação para analisar se já estamos logados. Além disso, vou colocar uma vírgula e vou passar esse DjangoModelPermissions para esse nosso modelo de permissão de classes também.

[01:09] Isso que fizemos está relacionado com o aluno. O curso, matrícula, lista de matrículas também precisam desse nosso DjangoModelPermissions, dentro dessa nossa variável das classes de permissões.

[01:25] Então o que eu vou fazer? Eu vou copiar essa linha aqui, permission_classes = [IsAutenthicated, DjangoModelPermissions], estamos vendo que o nosso código já está bem duplicado, várias coisas, nós vamos melhorar isso. Mas vou colocar aqui, no lugar do permission_classes só com IsAuthenticated, eu vou alterar, eu vou colocar também o DjangoModelPermissions, os dois. Vou fazer isso para todos.

[01:53] Salvei o meu código, o que eu vou fazer agora? Eu quero testar, vamos testar um por um. Eu vou começar testando a Ana, a responsabilidade dela é manter os recursos de matrículas, então eu vou visualizar.

[02:05] Para isso podemos fazer duas coisas, posso abrir uma aba privada do Chrome para fazer esse teste, posso abrir em outro navegador uma aba privada, aqui, por exemplo, digitar “localhost:8000” e quando eu clico, por exemplo, em “matrículas”, ele vai pedir um username, vou passar “Ana”, vou passar a senha da Ana que eu criei. Quando eu dou um “Sign in” eu consigo visualizar as matrículas.

[02:32] Observe que eu não tenho nenhuma matrícula criada, então vou criar. Vou colocar aqui período matutino, a Isabel Martins, no curso de Python Fundamentos. Vou alterar, vou colocar Python Avançado. Vou dar um “Post” e conseguimos. Parece que está tudo ok.

[02:49] Vamos testar agora algo que ela não pode fazer? Observe que o nosso delete não aparece mais aqui. Se eu acessar, por exemplo, a “/matriculas” aqui, colocar “/1”, e visualizar essa matrícula, temos o “Put”, nós conseguimos atualizar, conseguimos realizar o “Get”, o “Options” dessa requisição, só que não temos o verbo delete.

[03:09] O que eu vou fazer agora? A Ana não pode criar e manter alunos, por quê? Manter e criar alunos são recursos e permissões válidas para o Marcos. Mas vamos testar isso daqui. Vou clicar em “cursos” e observe que quando eu scrollo para baixo em cursos, nem aparece a aba do post. Para nós fez sentido isso daqui.

[03:32] Se eu acesso aqui “matrículas”, ele mostra para mim as matrículas e aqui embaixo eu tenho um HTML e um form, indicando que eu posso aqui executar um post e criar um novo recurso.

[03:42] Agora, se eu coloco, por exemplo, em “alunos”, eu vou listar todos os alunos e quando acabar essa lista de alunos eu não consigo fazer nada, ou seja, o get eu consigo visualizar, da Ana, dos recursos de aluno, cursos, mas eu não tenho ação nenhuma, a Ana não tem permissões de manipular esses recursos.

[04:02] Para testar o Marcos eu vou utilizar o Postman, mas se você não quiser utilizar o Postman, se você quiser utilizar aqui mesmo, abrir outra aba anônima e fazer o teste, você pode. Então vou fechar isso daqui, vou lá no Postman e vamos só relembrar o que o Marcos pode fazer.

[04:20] O Marcos é responsável por criar alunos e cursos, mantendo esses recursos. O que eu vou fazer? Vou pegar esse aluno, de cópia, só para ganharmos tempo, vou vir no Postman e vou dar um post nesse endpoint, deixa eu copiar o código, colocar aqui no “Body”. O nosso código não é XML, é JSON. Não tem o ID, eu já vou alterar esses dados para conseguirmos visualizar melhor.

[04:58] O que eu vou fazer agora? Vou pegar esse nosso end-point, “localhost:8000/alunos/”, eu quero dar um post, e vou colocar aqui no nome “teste do Postman”. O RG vai ser esse RG, deixa eu mudar só um número para ele não ficar igual, vou colocar aqui na frente “2”, aqui no CPF vou colocar “2” também e a data de nascimento eu vou deixar essa mesmo.

[05:26] O que eu preciso fazer? Eu preciso ter uma autorização. Então venho em “Authorization”, vou colocar que é um “Basic Auth” de authorization e vou colocar o Marcos com a senha dele.

[05:39] Aqui no “Body” eu vou dar um “Send”, vamos visualizar, e parece que foi criado, o ID 203. Vamos ver lá do lado da nossa API? Em “/alunos”, se eu colocar “/203/”, eu tenho aqui o teste do Postman. Maravilha, fez sentido.

[05:54] Só que observa que do Marcos, quando eu estou visualizando, eu estou logado com o meu admin, então eu vejo o delete. Será que o Marcos consegue deletar esse aluno? Vamos testar?

[06:07] Selecionei esse end-point, se eu dou um get nesse end-point, “http://localhost:8000/alunos/203/”, dou um “Send”, ele vai mostrar para nós esse recurso que criamos.

[06:17] Eu não quero dar um get nesse recurso, eu quero deletar, então vou colocar aqui o verbo delete e vou tentar. Quando eu dou um “Send” observe que legal a mensagem que ele já dá: “Você não tem permissão para executar essa ação”. Muito bacana.

[06:32] Mas e se eu quisesse alterar alguma coisa? Então eu vou dar aqui um put, e eu vou mudar o nome, “Postman atualizado”, só para visualizarmos lá. Se eu dou um “Send”, temos “Postman atualizado”. Será que alterou aqui para nós também? Clicando aqui em atualizar, alterou, “Postman atualizado”.

[06:58] Olha que bacana, quando criamos usuários e determinamos as permissões desses usuários do lado do Django admin, para trazermos essas informações para cá, nós utilizamos a classe DjangoModelPermissions e passamos para o nosso ViewSet, lá no permission_classes esse módulo que importamos também.

[07:18] Isso ficou bem legal, só que tem um ponto que está um pouco estranho no nosso código, observe a quantidade de código duplicado que temos, principalmente para essa parte de autenticação e permissão. Será que nós conseguimos melhorar o nosso código removendo essa quantidade de código duplicado? É isso que vamos ver no próximo vídeo.

### Refatorando o código

Podemos criar uma função para permission_classes e authenticated_classes. 

1. No SETTINGS.PY podemos adicionar uma outra permissões

        REST_FRAMEWORK = {
            'DEFAULT_VERSIONING_CLASS': 'rest_framework.versioning.QueryParameterVersioning',
            'DEFAULT_PERMISSION_CLASSES': [
                'rest_framework.permissions.IsAuthenticated',
                'rest_framework.permissions.DjangoModelPermissions'
            ],
            'DEFAULT_AUTHENTICATION_CLASSES': [
                'rest_framework.authentication.BasicAuthentication',
            ]
        }

2. NO VIEWS.PY podemos remover:

        authentication_classes = 
        permission_classes = 

---

[00:00] Conseguimos incluir as permissões que queríamos na nossa aplicação, porém se observarmos o nosso código da views, temos várias linhas repetidas.

[00:08] Por exemplo, o authentication_classes e o permission_classes estão iguais em praticamente todos os nossos viewsets, porém, como conseguimos minimizar esse código duplicado? É isso que veremos nesse vídeo. Vamos melhorar o nosso código, deixá-lo mais legível, sem tanta repetição e sem alterar o comportamento da nossa aplicação.

[00:27] Para isso vamos acessar os settings da nossa aplicação, aqui, “setup > settings.py”, e dentro desse REST_FRAMEWORK podemos indicar outras configurações padrões, por exemplo, eu quero indicar o authentication_classes.

[00:44] Da mesma forma que temos aqui um DEFAULT_VERSIONING_CLASS, indicando o QueryParameter, eu vou colocar aqui uma vírgula e vou colocar outro tipo de verificação, vai ser o DEFAULT_PERMISSION_CLASSES, no plural. Então as permissões das nossas classes, as permissões padrões. Dois pontos, entre colchetes, aqui dentro eu vou passar quais são essas permissões. E temos duas.

[01:21] Lá do nosso rest_framework.permissions – vou copiar esse código, vou colocá-lo aqui, entre aspas também – temos duas permissões, a primeira, IsAuthenticated, para saber se ele está autenticado, vou copiá-lo aqui, .Isauthenticated’,.

[01:40] Aqui embaixo eu tenho esse mesmo código, ’rest_framework.permissions.IsAuthenticated’, vou dar aqui um “Enter”, só que no lugar do IsAuthenticated nós vamos utilizar o DjangoModelPermissions, vou colocá-lo aqui. Nós passamos então para cá.

[01:56] O que eu já poderia fazer? Todas essas linhas de classes de permissões eu já posso tirar daqui, porque eu coloquei-a lá no setup da nossa aplicação. Então nós dizemos que por default essas são as nossas autenticações. Então todas essas linhas nós vamos tirar, permission.

[02:16] O que podemos fazer também é para a parte de autenticação. Temos aqui do rest_framework.authentication, vou criar o default dele, vou colocar aqui uma vírgula, porque nós fechamos esse permission, DEFAULT_PERMISSION_CLASSES, entre aspas vou colocar ’DEFAULT_AUTHENTICATION_CLASSES’:, no plural, entre colchetes vou passar o meu valor.

[02:48] Então temos, lá do Django Rest Authentication, entre aspas ’rest_framework.authentication.’, queremos verificar que a pessoa está autenticada, e nós utilizamos o BasicAuthentication, então vou passar aqui .BasicAuthentication’.

[03:09] Salvei, o que eu posso fazer? Vou remover essa linha de autenticação, essas linhas também, authentication_classes = [BasicAuthentication]. Salvei esse aqui, posso remover essa linha, from rest_framework.authentication import BasicAuthentication, não estou utilizando.

[03:29] Então nosso código já ficou bem mais fácil de entendermos. E nós vamos continuar com o mesmo comportamento. Vou colocar aqui uma vírgula, só para o nosso terminal não parar. Vamos testar para ver se tudo está funcionando bem?

[03:45] O que eu vou fazer? Aqui eu estou no “alunos” com autorização do Marcos, o Marcos pode fazer as atualizações de alunos, então vou colocar “Postman atualizado 2.0”, algo desse tipo, vou dar um “Send” e temos o “Postman atualizado 2.0”.

[04:03] Vou tentar deletar esse aluno 203, e nós recebemos que não temos a permissão, ou seja, nossas permissões continuam funcionando, então o nosso código continua igual e nós melhoramos bastante a questão das nossas views, deixamos muito melhor.

[04:22] Outro ponto que podemos melhorar na nossa aplicação é a navegação. Se observarmos no nosso código, quando eu clico aqui, “alunos”, ele vai pedir autenticação, vou logar como o usuário admin, que eu quero mostrar outro ponto que podemos melhorar, e observe que aqui temos o “localhost:8000/alunos/”. Se eu coloco aqui, por exemplo, o aluno 2, temos os detalhes do aluno 2 e assim por diante.

[04:45] Se eu quiser visualizar todas as matrículas desse aluno, o que eu tenho que fazer? Vamos visualizar lá em “setup” as nossas URLs.

[04:53] Na nossa URL eu tenho aluno, no singular, o ID desse aluno, barra matrículas. Então eu teria que tirar esse S, “localhost:8000/aluno/2/matriculas/”. Quando eu dou um “Enter” ele não tem nenhuma matrícula, eu acho que fizemos a matrícula para o aluno 1. Deixa eu voltar aqui. Isso, para a aluna 1. Então temos aqui as matrículas da aluna 1.

[05:17] Só que observe que faz mais sentido pensarmos na nossa API como uma navegação entre pastas. Se eu mantenho tudo no plural, vai ficar muito mais fácil eu conseguir manipular os dados, melhorar os meus end-points.

[05:30] Por exemplo, se eu coloco “localhost:8000/alunos/1/”, temos detalhes do ID 1. Se eu quiser visualizar as matrículas, faria mais sentido se eu tivesse aqui “localhost:8000/alunos/1/matriculas”, dou um “Enter” e visualizo as matrículas desse aluno.

[05:43] Ou seja, posso padronizar os meus end-points, como? Tudo no singular ou tudo no plural, para ficar mais fácil essa navegação. Vamos alterar isso então?

[05:52] Vou deixar “alunos”, vou deixar “cursos”, então temos end-point de alunos, end-point de cursos e de matrículas. Se eu quero visualizar, por exemplo, as matrículas de um determinado aluno, eu vou utilizar no plural por conta da navegação da minha aplicação também. Então se eu atualizo aqui, deu um erro. Vou atualizar mais uma vez, ele conseguiu trazer.

[06:16] Se eu coloco, por exemplo, as matrículas do aluno 2, ele vai mostrar que esse aluno não tem nenhuma matrícula. O mesmo acontece para os nossos cursos. Eu tenho um curso, eu passo o ID desse curso, barra, e quero ver todas as matrículas que esse curso possui, vai ficar muito mais fácil a nossa navegação.

[06:33] E de onde nós tiramos essa ideia? Vamos pensar bem nos nossos end-points como uma navegação entre pastas. É uma analogia muito simples, mas que vai fazer sentido e vai ficar muito mais fácil conseguirmos navegar nos nossos end-points.

[06:50] O que nós fizemos? Colocamos lá nos settings da nossa aplicação as propriedades default das nossas classes, tanto os de permissões como os de autenticação, e nós melhoramos os nossos end-points padronizando tudo no plural, para ficar mais fácil essa navegação.

### Exercício: Django Admin e API

Nesta aula, criamos 2 tipos de usuários utilizando o Django Admin com permissões diferentes, em que cada um é responsável por um recurso.

Sabendo disso, analise as afirmações abaixo e marque a que está correta em relação ao Django Admin.

a) **Alternativa correta:** As alterações feitas no Django Admin podem ser aplicadas na API Rest, respeitando as boas práticas de programação.
- _Alternativa correta! Podemos incluir as configurações em cada viewset ou apenas uma única vez no settings.py do projeto._

b) As alterações feitas no Django Admin não podem ser aplicadas na API Rest.

c) As alterações feitas no Django Admin podem ser aplicadas na API Rest. Porém, uma série de códigos duplicados será necessária para o funcionamento.

### O que aprendemos?

- No Django Admin, criamos a usuária Ana, com permissão de manter os recursos de Matrículas, como criar, ler e atualizar; e o usuário Marco, com permissão para manter os recursos de Alunos, podendo criar, ler e atualizar;
- Configuramos o Django Rest para utilizar as permissões do Django Admin e testamos as permissões no Postman;
- Melhoramos a qualidade do nosso código removendo o código duplicado das views.

## 3. Viewset e permissões
### Métodos HTTP

Na API podemos definir na VIEWS.PY qual o método disponível para a VIEWSET.

    class CursosViewSet(viewsets.ModelViewSet):
        ...
        http_method_names = ['get','post','put','path','delete']

---

[00:00] Agora que refatoramos o nosso código e melhoramos para caramba a qualidade do nosso arquivo de views, tiramos todo aquele código duplicado, existe um ponto interessante que eu quero mostrar para vocês também.

[00:12] Criamos aqui as classes AlunosViewSet, CursosViewSet e MatriculaViewSet. Isso significa que quando vamos para a nossa API e eu clico em “alunos”, observe que eu tenho esses verbos aqui, get, post, head e options, essas ações permitidas para esse recurso de alunos.

[00:26] Então eu posso buscar uma informação de um aluno, colocar aqui o post para criar um novo aluno, o head e o options, outros verbos que eu tenho também.

[00:34] E se eu coloco aqui, por exemplo, “localhost:8000/alunos/1”, observe que eu tenho o put e o patch para eu atualizar determinado aluno também. Então ele me mostra todas essas ações. Isso é padrão, tanto para alunos como para cursos também, temos todas essas ações. E se eu seleciono um determinado curso, podemos ver que o put e o patch aparecem aqui também.

[00:54] E o mesmo para as matrículas, deixa eu mostrar para vocês, “matriculas”, eu tenho aqui options, o get no formato JSON e API, e aqui embaixo o post, para eu criar uma nova matrícula, e se eu seleciono uma determinada matrícula com esse ID, temos aqui o put e o patch.

[01:14] “Beleza, Guilherme, o que você quer dizer?”. Vamos supor que eu quero criar um determinado recurso, mas eu não quero permitir todas as ações. Eu não quero permitir, por exemplo, o delete.

[01:24] Observe que quando eu coloco aqui “/matriculas/1”, aparece por padrão o delete. Em nenhum momento do nosso código, em nenhum viewset nosso nós falamos: “Esses são os verbos permitidos”, não. Por padrão, quando criamos um viewset, ele nos gera recursos para atender todas as ações.

[01:45] O que eu quero fazer? Vamos supor que a matrícula eu não quero permitir o delete, em hipótese alguma, nenhum usuário, nem admin, nunca. Não quero permitir aqui o delete na minha API, como eu faço isso?

[01:57] Existe uma forma de limitarmos esse delete indicando quais são os verbos que eu quero permitir para esse viewset. Para isso eu vou colocar aqui http, ele já até aparece ali, _method_names, no plural. E eu coloco aqui um igual, entre colchetes eu vou falar que eu quero o get, por exemplo, e o post, só para visualizarmos esse exemplo.

[02:21] O que eu posso permitir dessa forma? Vou salvar. Quando eu coloco http_method_names = [‘get’, ‘post’], significa que eu vou conseguir recuperar uma determinada matrícula e criar uma matrícula nova. Outros verbos, o delete, o put e o patch vão desaparecer.

[02:37] Vou atualizar essa página e observe que temos aqui um get. Todo aquele contexto que tínhamos aqui embaixo, de atualizar uma matrícula, já desapareceu, ele não está mais visível.

[02:47] E se eu for lá para a página de matrícula, observe que temos o get e o post, eu consigo criar uma nova matrícula, por exemplo, eu vou criar aqui, no período vespertino, para o Renan e o curso vai ser o Python/React. Quando dou aqui um “Post” ele mostra para nós, se eu for lá na tabela de matrícula, temos duas matrículas.

[03:05] Só que por mais que eu acesse a matrícula 2, eu não consigo atualizar. Mas eu quero atualizar essa matrícula, então vamos especificar esses verbos.

[03:12] Vou colocar aqui, para eu atualizar eu tenho o ’put’, e tenho também o ’path’. Vou deixar os dois, para entendermos. Estou aqui no “localhost:8000/matriculas/2/”, quando eu atualizo aparece para nós o put e nós conseguimos atualizar também esse nosso recurso.

[03:33] Por exemplo, vou falar, ele mudou, o período agora dele é noturno. Quando eu dou aqui um “Put” ele muda para nós para o período noturno também.

[03:41] Então essa é uma forma que temos para limitar as ações que queremos dentro de um viewset. Quero criar um viewset, quero usar todos os recursos possíveis que o Django REST nos proporciona.

[03:53] Observe que em nenhum momento estamos criando na mão, se for o método get verificando eu quero essas ações, não. Estamos deixando tudo isso por conta do Django REST, e estamos especificando que queremos para o nosso recurso de matrícula esses métodos, o get, o post, o put e o path.

[04:12] Vamos supor que eu quero o método delete também, eu posso colocar aqui o delete. Quando eu volto lá e atualizo, o método delete vai aparecer para nós também. Então vou tirar aqui o método delete, eu não quero, vou deixá-lo apenas com esses métodos aqui, para lembrarmos.

[04:28] Então não coloquei nada, não especifiquei nenhum http name, aqui em cursos ou aluno ele vai permitir todos os verbos possíveis, o get, o post, o put, o path, o options e todos os outros verbos também. E o mesmo acontece para curso.

[04:46] Mas eu quero especificar, eu tenho esse recurso, mas eu não quero todos os verbos, então eu posso criar essa nossa variável, http_method_names e indicar quais são os verbos que eu quero utilizar.

### Limitando requisições

Podemos limitar o acesso a nosssa API por requisições por usuário. Com funcionalidade DJANGO-REST THROTTLING. [DOCUMENTAÇÃO]('https://www.django-rest-framework.org/api-guide/throttling/')

No SETTINGS.PY adicionamos:

    REST_FRAMEWORK = {
        'DEFAULT_THROTTLE_CLASSES': [
            'rest_framework.throttling.AnonRateThrottle',
            'rest_framework.throttling.UserRateThrottle'
        ],
        'DEFAULT_THROTTLE_RATES': {
            'anon': '100/day',
            'user': '1000/day'
        }
    }

---

[00:00] Na nossa API nós incluímos permissões e criamos a Ana e o Marcos para controlar e manter determinados recursos.

[00:07] Porém, essa não é a única forma que temos no Django REST de criar permissões ou limitar o acesso aos recursos que a nossa API disponibiliza. Podemos inserir outra forma de permissões do consumo da nossa API.

[00:23] Por exemplo, eu posso criar uma forma de limitar a quantidade de requisições. Então vou falar, por exemplo: “Esse usuário pode fazer x requisições” ou “Se o usuário for anônimo, ele vai poder fazer tantas requisições”, e é isso que eu quero mostrar para vocês agora.

[00:38] Vamos acessar a documentação do Django REST, aqui “Django REST framework: Home”. Aqui em cima, em “API Guide”, temos essa palavra “Throttling”, vou clicar nela. Podemos entendê-la como um limite. Tem uma explicação bem legal sobre ela e aqui temos como utilizamos essa política de limitação.

[01:02] O que acontece? Nós conseguimos criar uma limitação para um usuário que for anônimo, então aqui eu falo, se o usuário for anônimo, ele pode fazer 100 requisições por dia, ou se for um determinado usuário, ele pode fazer mil requisições por dia.

[01:17] Vamos copiar essa configuração, passar lá para o nosso arquivo de setup, do settings. Só para lembrarmos, vou minimizar a nossa “escola”, então em “setup > settings.py”, eu coloquei uma vírgula ali e vou colocar essa nossa classe de throttle classes, palavra difícil em inglês.

[01:44] Primeira coisa, eu vou tirar – só para conseguirmos testar certo – essa limitação de permissão das classes. Selecionei tudo, dei um “Command + /”, para ele colocar essa linha como comentário, e aqui vamos manter o BasicAuthentication.

[02:04] Já que criamos os usuários e falamos: “Esse usuário pode manter, criar, atualizar determinado recurso”, eu vou fazer só com o usuário anônimo. O que é um usuário anônimo? Uma pessoa que não está logada e fez um get na nossa API ou tentou fazer alguma coisa na nossa API.

[02:23] Eu vou remover essa linha de baixo, ’rest_framework.throttling.UserRateThrottle’, vou deixar só essa linha, ’rest_framework.throttling.AnonRateThrottle’. Vou tirar também essa, ’user’ : ‘1000/day’. 100 requisições por dia é um número talvez aceitável, dependendo da situação que é disponibilizada a sua API.

[02:46] Como estamos no vídeo, para eu fazer as 100 requisições e mostrar no vídeo, vai ficar impossível, vai ficar um vídeo muito comprido. Vou deixar 5 requisições por dia, só para vermos isso funcionando.

[02:56] Eu indiquei que vai existir um rate, um limite de requisições para um usuário anônimo. E a quantidade do usuário anônimo é de cinco requisições por dia.

[03:10] O que eu vou fazer? Eu poderia testar isso lá na minha API mesmo, deslogar o Gui aqui como admin e fazer esse teste. Mas para ficar mais fácil para entendermos e para irmos contando para ver se está certo esse número, eu vou fazer esse teste no Postman.

[03:26] Não se preocupe se você não está com o Postman instalado, eu mostro aqui no vídeo, depois você pode fazer esse teste na sua casa também.

[03:33] Eu estou utilizando aqui o “Basic Auth”, vou remover, vou colocar aqui “No Auth”, eu sou um usuário anônimo, e vou dar aqui um “Send” em cursos. E ele mostrou, apareceu aqui um, dois, três, estou vendo todos os cursos, quatro, cinco.

[03:52] Na sexta vez aparece algo diferente, “Pedido foi limitado”, e ele dá aqui um valor em segundos e eu preciso esperar até o outro dia. Olha que bacana.

[04:04] Além das permissões que criamos lá no nosso admin e depois lá na nossa view – deixa eu abrir nossa view – nós falamos que determinados usuários vão poder utilizar tais recursos, vão manter alguns recursos, quando fazemos isso estamos bem especificando, estamos falando assim: “Esses usuários podem fazer, alterar e manter esses recursos”.

[04:32] Quando utilizamos esse cenário, por exemplo, a minha API está aberta e eu consigo limitar o uso da minha API. No Postman eu só utilizei o get como exemplo para ficar mais fácil, mas depois você pode testar os outros verbos também, o get, o post.

[04:47] Então para esse usuário anônimo nós colocamos cinco requisições por dia de limite, mas é um número com base naquilo que o seu sistema ou aquilo que você está criando faz sentido você colocar. Essa é outra ideia.

[05:04] Temos dois níveis de permissões aqui, temos esse nível de permissão que eu vou comentar aqui, que é o nível que vimos nesse vídeo, que vamos limitar uma determinada quantidade de requisições da nossa API, seja um usuário anônimo ou seja um usuário da nossa API.

[05:20] Ou temos aqui uma possibilidade de falar: “Lá no nosso Django admin nós criamos alguns usuários com determinadas permissões, então eu quero que essas permissões sejam refletidas também na minha API”, então nós colocamos esse PERMISSION_CLASSES e indicamos que queremos aqueles usuários com aquelas determinadas requisições. São duas formas que podemos disponibilizar os recursos da nossa API.

### Exercício: Tipos de Views

Uma pessoa estava trabalhando no desenvolvimento de uma API que tinha o seguinte desafio: criar um recurso capaz de atender apenas requisições GET e DELETE.

Ao pesquisar a documentação, ela decidiu utilizar o RetrieveDestroyAPIView.

Analise a história acima alinhando-a ao conteúdo aprendido e assinale as alternativas que correspondem melhor ao que podemos esperar do RetrieveDestroyAPIView.

a) **Alternativa correta:** O uso do RetrieveDestroyAPIView vai atender a necessidade da pessoa.
- _Alternativa correta! Conforme a documentação, o uso deste método permitirá apenas ações como GET e DELETE._

b) O uso do RetrieveDestroyAPIView não vai atender a necessidade da pessoa, pois, o Django Rest só funciona com ViewSet.

c) **Alternativa correta:** A pessoa pode usar o método RetrieveDestroyAPIView ou um ViewSet, limitando as ações do recurso.
- _Alternativa correta! Podemos configurar as ações do ViewSet através de http_method_names = ['get', 'delete'], por exemplo._

### O que aprendemos?

- Vimos como limitar as ações de um ViewSet;
- Aprendemos como limitar a quantidade de requisições de um usuário anônimo.

## 4. Modelo de maturidade e Location
### Modelo de maturidade

- A lama do XML
    - _HTTP como um sistema de transporte para interações remotas, mas sem a utilização de qualquer um dos mecanismos da web._
- Recursos
    - _Introdução de recursos. No lugar de fazer todos os nossos pedidos a um simples endpoint, trabalhamos com recursos individuais._
- Verbos HTTP
    - _Introduz um conjunto padrão de verbos para que possamos lidar com situações semelhantes, da mesma forma._
- Controle de Hipermídia
    - _Busca uma forma de fazer um protocolo auto-documentado._

---

[00:00] Nesse vídeo vamos conversar um pouco sobre modelos de maturidade com base na glória do REST de Richardson, que é um artigo muito bacana onde ele descreve os passos em direção a glória do REST.

[00:13] O que acontece? Nós criamos a nossa API, ela tem várias funcionalidades bacanas, versionamento, relacionamento entre modelos, padronizamos os nossos end-points, fizemos bastante coisa legal. Mas é possível subirmos ainda um nível de maturidade na nossa API, com base nesse artigo.

[00:32] Vou deixar esse link na descrição desse vídeo para você conseguir ler depois, ele está em inglês, mas você pode usar o Google Translate para conseguir entender depois esse artigo em português também. E vamos falar um pouco sobre a glória do REST, com base no Richardson.

[00:49] Eu fiz aqui um pequeno resumo para entendermos esse caminho para a glória do REST. Ele divide esse modelo de maturidade em alguns níveis, e o primeiro nível que temos ele dá um nome de lama do XML, algo desse tipo. O que é a lama do XML? É utilizarmos o protocolo do http sem qualquer um dos mecanismos da web.

[01:14] Por exemplo, eu tenho lá na nossa API o recurso chamado alunos, e quando queremos criar um determinado aluno, o que nós fazemos? Vamos no end-point desse determinado recurso, utilizamos o verbo do http post para que criemos, de fato, um determinado aluno ou aluna na nossa aplicação.

[01:36] Isso é interessante, porém nesse nível 0 nós não teríamos isso, teríamos um end-point cadastrar aluno e passaríamos nesse end-point todas as outras informações. Repara que na lama do XML nós não temos essa divisão dos recursos, nós não utilizamos todos os mecanismos da web para que consigamos criar os nossos recursos.

[02:05] O nível 1 já pensa em introduzir recursos na nossa API. No lugar de termos um simples end-point que vai fazer um monte de coisa mágica, nós não queremos, vamos começar a dividir e trabalhar com recursos individuais, como fizemos na nossa API.

[02:21] Criamos alunos e mantivemos os recursos de alunos, criamos cursos e mantivemos o recursos relacionados aos cursos da nossa API, e matrículas também. Então nós começamos a dividir a nossa aplicação em recursos diferentes. E isso é uma coisa legal. E ele fala que esse é o nível 1 de modelo de maturidade da glória do REST.

[02:43] O nível 2 nós começamos a introduzir um conjunto de padrões e verbos para que possamos lidar com situações semelhantes. Se eu quero criar um determinado recurso, se eu quero atualizar ou se eu quero recuperar uma determinada informação, vamos começar a utilizar o conjunto de padrões dos verbos do http.

[03:06] E para finalizar, o último nível é o controle de hipermídia, onde buscamos uma forma de fazer o nosso protocolo ser auto-documentado. O que isso significa? Significa que a minha própria documentação, eu vou utilizar o protocolo para que as pessoas e sistemas que utilizam e consomem recursos da minha API estejam cientes do que está acontecendo. Então vamos utilizar o protocolo para auto-documentar a nossa API.

[03:35] Só para fazer um resumo aqui do modelo de maturidade, seguindo os passos para a glória do REST com base no Richardson, temos o nível 0, onde não utilizamos os recursos do http e os end-points cadastrar aluno ou algo muito mágico fazendo e não tem a divisão dos recursos.

[03:57] No nível 1 já temos essa divisão dos recursos, eu trabalho só com alunos ou nesse momento estou trabalhando só com matrículas, trazendo um pouco para o nosso contexto, então nós dividimos os recursos da nossa API.

[04:09] Depois temos a inserção dos padrões, dos verbos para situações semelhantes na nossa API e por último, controle de hipermídia, onde vamos buscar uma forma de auto-documentar as informações na nossa API. Esse é o modelo de maturidade de Richardson.

[04:33] O que vamos fazer na sequência? Vamos pensar nesse nível 3, em controle de hipermídia. Como podemos documentar melhor uma determinada situação ou um determinado recurso ou uma determinada ação na nossa API, para que aqueles que estão consumindo nossa API, fique mais claro o que está acontecendo. Vamos fazer isso a seguir.

### Cabeçalho Location

O cabeçalho Location retorna para ou usuário da API o endereço do elemento criado por ele.

No VIEWS.PY:

    ...
    from rest_framework.response import Response

    class CursosViewSet(viewsets.ModelViewSet):
        ...

        def create(self,request):
            serializer = self.serializer_class(data=request.data)
            if serializer.is_valid():
                serializer.save()
                response = Response(serializer.data, status=status.HTTP_201_CREATED)
                id = str(serializer.data['id'])
                response['Location'] = request.build_absolute_uri() + id
                return response

---

[00:00] Vamos subir um nível de maturidade da nossa API REST? Eu quero mostrar algo interessante para vocês. Eu vou clicar com o botão direito, vou escolher a opção inspecionar, “Inspect”, e vou selecionar a opção “Network”.

[00:14] Eu vou clicar aqui em “cursos”, aqui temos todas as propriedades do curso, todas as informações e eu vou acessar o curso com o ID 1, dou um “Enter” no “localhost:8000/cursos/1” e aqui eu tenho duas pastas. Eu tenho aqui o ID 1, localhost 1, e esse “1/”.

[00:30] Vou clicar nessa primeira opção, “1”, e vou scrollar. Observe que quando scrollamos essa parte, nesse “Response Headers”, existe uma propriedade chamada “Location”, o que isso significa?

[00:43] Esse location serve para auto-documentar a nossa API utilizando os recursos da web. Só que esse location é exibido no Django quando acessamos determinado ID, porém quando criamos um novo curso, eu vou fazer isso aqui, vou chamar curso de Java básico, por exemplo, vou chamar “Curso de Java”, deixar nível básico. Vou limpar aqui, vou dar um “Clear”.

[01:13] Quando eu dou um “Post”, observe que ele criou aqui o “cursos/”, só que quando nós scrollamos o “Response Headers” nós não temos o location. Nativamente o Django REST não nos traz o location.

[01:26] Como eu crio o location para tornar minha API auto-documentada? Eu quero que todas as vezes que eu crio um elemento novo, apareça aqui na propriedade do “Response Headers” a aba location com o ID desse curso que eu acabei de criar, que é o curso com o ID 11, então vou colocar aqui “localhost:8000/cursos/11/”.

[01:44] Eu queria que o meu location tivesse esse end-point, indicando para quem está consumindo a nossa API: “Esse aqui é o link do recurso que você acabou de criar”. Vamos fazer isso? Primeira coisa, vou abrir meu app de “escola”, vou lá nas minhas views. Vou acessar aqui cursos, deixa eu dar um “Enter” só para ficarmos com essa aba de cursos na nossa tela.

[02:12] Para que consigamos acessar o nosso curso, vamos precisar fazer um import de dois módulos. O primeiro módulo é do rest_framework mesmo, .response import Response, é esse. Conforme formos escrevendo o nosso código, eu vou fazer o import dos outros também.

[02:40] O que eu quero fazer? Quando eu crio um elemento novo, eu quero incluir o response location. Então quando nós criamos, significa que vamos precisar reescrever o nosso método create. Vou reescrever o create():.

[02:55] Para eu reescrever o create dois argumentos são necessários, primeiro, a instância que estivermos trabalhando, (self, e a requisição, request):.

[03:05] Primeira coisa que eu vou fazer vai ser buscar todos os dados dessa minha requisição, eu vou chamar de serializer, no singular, vou falar que ele vai ser igual a instância que estivermos utilizando, = self.serializer_class, entre parênteses, para eu buscar todas as informações, eu vou utilizar a propriedade (data=request.data).

[03:31] E aqui o que nós vamos fazer? Vamos verificar se as informações que passamos para o nosso serializer são válidas. Para isso, if serializer.is_valid():, se ele for válido o que eu quero fazer? Eu quero salvar os dados no meu serializer, eu quero pegar aquela informação post que eu enviei e salvar na minha base de dados, serializer.save().

[03:56] O que acontece agora? Vamos pensar no lado do location. Primeira coisa, se um dado foi salvo, ele foi criado, eu preciso falar qual é o dado criado, precisamos devolver essa resposta para o nosso servidor.

[04:09] Então vou criar uma variável chamada response = e vou falar que ela vai ser igual a classe Response que acabamos de importar, passando o (serializer.data, com as informações que criamos na nossa base de dados e o status code, que vai ser status=status., existe uma propriedade chamada status.

[04:34] Como vamos criar um elemento, já temos aqui HTTP_201_CREATED). Vou selecionar essa opção. Temos então a resposta dessa requisição.

[04:46] O que eu vou precisar fazer agora vai ser buscar o ID dessa requisição, para eu criar a minha URL location inteira. Vou criar uma variável chamada id = e para eu conseguir recuperar a informação desse ID eu vou utilizar a propriedade serializer.data[‘id’].

[05:06] Se eu executar da forma que está aqui, vamos receber um erro mostrando que o ID é do tipo inteiro e precisamos na concatenação, para criar a nossa string, de um tipo string. Então eu vou converter aqui já, str e vou colocar entre parênteses, encapsulando esse serializer data.

[05:25] Agora o que eu posso fazer é criar o meu response location. Então response [‘Location’] =, eu preciso do endereço daquele “localhost:8000/cursos/” mais o ID, para eu pegar todo esse endereço eu vou pegar lá da request.build_absolute_uri(). É uma função, ela vai pegar o endereço completo e eu quero concatenar com o ID do recurso que salvamos.

[06:12] Para finalizar, o que eu vou fazer? Dar um return response. Salvei, abri o terminal, vou ver se tem algum erro aqui. Salvando de novo. Acho que eu escrevi response em algum lugar errado, deixa eu ver. Aqui em cima tem um response também minúsculo, eu vou tirar, vou deixar só o maiúsculo. Era isso.

[06:44] Ele acabou importando um response que não vamos precisar usar, esse response aqui é referente aos dados e o status code da nossa aplicação, então não tem eles, nós só vamos precisar de dois imports, o response com R maiúsculo, que fizemos no início, e o rest framework status, para devolvermos aqui o status code 201 de criado.

[07:07] Vamos testar isso agora. Vou vir aqui em “Cursos List”, tenho alguns cursos. Eu vou criar, por exemplo, curso de Docker, então vou colocar “Curso de Docker”, básico, vou limpar, dar um “Clear” para visualizarmos o nosso location, dou um “Post” e foi criado, tem o ID.

[07:36] Vamos navegar, acessando aqui a barra “cursos/”, scrollando um pouco para baixo, temos aqui um “Location: http//localhost:8000/cursos/12”, que é o curso do ID que acabamos de criar.

[07:50] Dessa forma nós conseguimos auto-documentar a nossa API. Todas as vezes que criarmos um curso, mandamos no response headers uma propriedade chamada location.

[08:03] Isso nós podemos pensar em extrair para outra função e passar para todos os outros módulos que temos também. Deixa eu só tirar a quantidade de espaços aqui, só para ficarmos com o nosso código certo.

[08:17] Fizemos isso para o nosso curso, mas poderíamos fazer isso para os outros viewsets que temos aqui também e padronizar o nosso projeto. Esse foi só um exemplo demonstrativo de como podemos tornar nossa API mais auto-documentável.

### Exercício: A glória do REST

Aprendemos que segundo o artigo [Modelo de maturidade de Richardson]('https://martinfowler.com/articles/richardsonMaturityModel.html'), existem níveis para a glória do Rest.

Sabendo disso, analise as afirmações abaixo e marque aquelas que trazem corretamente o nível de maturidade e sua devida função.

a) **Alternativa correta:** O nível 0 aborda a questão de lidar com a complexidade usando “dividir e conquistar”, quebrando um grande endpoint de serviço em vários recursos.

b) **Alternativa correta:** O nível 2 introduz um conjunto padrão de verbos para que possamos lidar com situações semelhantes da mesma forma.
- _Alternativa correta! No lugar de usar um endpoint cria-curso ou deleta-curso, por exemplo, usamos os verbos HTTP POST ou DELETE no endpoint de cursos._

c) **Alternativa correta:** O nível 3 fornece uma maneira de fazer um protocolo auto-documentado.
- _Alternativa correta! Vimos como incluir o cabeçalho Location sempre que um recurso é criado para auto-documentar a API._

### O que aprendemos?

- Aprendemos o que é o modelo de maturidade de Richardson e seus níveis;
- Incluímos o cabeçalho Location quando criamos um novo curso.

## 5. Teste de unidade na view e model
### Preparando o ambiente

No próximo vídeo, vamos integrar uma aplicação front-end desenvolvida em React para consumir nossa API. Para isso, clique [neste link]('https://github.com/guilhermeonrails/escola_react_api_3/archive/master.zip') para realizar o download do projeto React e siga os passos abaixo:
- Após o download, verifique se Nodejs está instalado em sua máquina, executando o seguinte comando em terminal:

        node --version

Se sua versão aparecer na tela, pode passar para o próximo passo. Caso a versão do React não apareça na tela, realize por gentileza o download do React em sua máquina, de acordo com seu sistema operacional.
- Agora abra um terminal na pasta do projeto e digite o seguinte comando para instalar as dependências do React:
        
        npm install

Atualize as dependências do npm com o seguinte comando:

        npm update

Para finalizar, ainda no terminal digite o comando abaixo para subir o servidor do React e aguarde:

        npm start

Após o carregamento, será exibida a seguinte página:

<center>
    <img src="https://caelum-online-public.s3.amazonaws.com/1996-api-django-3-versionamento-cabecalhos-cors/05/aula-5-p%C3%A1gina.png">
</center>


Chegou aqui? Você está pronto para descobrir o que é CORS na próxima atividade. Algo deu errado? Não hesite em pedir ajuda no fórum!

### O que é CORS?

[SAME ORIGIN POLICY]('https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy')

Compartilhamento entre recursos. 

---

[00:00] Na atividade anterior fizemos algo super legal, disponibilizamos uma API feita em React para consumir a nossa API feita em Django REST. E quando eu executo a minha API, eu subo o meu servidor no React, na porta 3000 e vou lá no meu console, acontece algo interessante.

[00:22] O que eu quero fazer com essa aplicação em React? Eu quero exibir a descrição dos cursos aqui, Python Fundamentos, Python/React, Python para Data Science, Python Avançado e mostrar aqui a lista de cursos criados numa outra linguagem, numa outra aplicação, então eu tenho o back-end e o front-end.

[00:38] Só que eu tenho uma mensagem no front-end indicando que fomos bloqueados por conta da política do CORS, que é o Acess-Control-Allow-Origin, que é o acesso de recursos compartilhados. Então o que é política de mesma origem?

[00:57] Política de mesma origem é um mecanismo de segurança crítico que restringe como um documento ou um script carregado de outra origem pode interagir com o recurso, entre eles, como eles podem conversar. Isso ajuda a isolar documentos maliciosos, reduzir ataques entre as aplicações também.

[01:22] Existe um local onde podemos ter mais informações sobre esse tipo de erro. Se eu digitar na barra de navegação “same origin policy”, por exemplo, eu tenho aqui alguns links explicando. Vou clicar no link do Mozilla para abrir e vou clicar no link do Wikipédia também.

[01:40] No Wikipédia temos uma descrição em português sobre esse tipo de segurança que temos na web, você pode dar uma lida depois nele. Eu vou pegar o exemplo do Mozilla. Ele fala que o compartilhamento entre recursos ou o CORS foi criado para ajudar a resolver problemas de segurança.

[02:02] Antes do CORS os desenvolvedores tinham que se esforçar muito para garantir quais APIs podiam consumir, quais APIs podiam ser compartilhadas por outras aplicações, por outros domínios, por outros clientes também dentro do navegador JavaScript. E hoje temos o CORS. O que o CORS faz? O CORS permite que solicitações de origem cruzada sejam compartilhadas de maneira segura.

[02:33] Pensando da perspectiva do React, o CORS é muito bom, porque o React vai falar: “Preciso consumir essas APIs” ou outra aplicação em front-end, “Preciso consumir esses determinados recursos com esses end-points, com esses caminhos, outras aplicações”.

[02:50] E essas outras aplicações vão precisar fazer configurações dizendo que: “Essa aplicação em React você pode confiar e nós vamos liberar os recursos e todas as outras informações também”.

[03:04] Mas quando eu sei o que são origens diferentes e o que são de mesma origem? Se observarmos na nossa aplicação, o que eu vou fazer aqui? Vou abrir o inspecionar, vou selecionar aqui “Network”, vou atualizar essa página. Eu atualizei, ele trouxe todas as informações para mim.

[03:28] Se eu vier em “cursos/”, aqui no “General” eu tenho política de referência same-origin. Então eu estou consumindo recursos utilizando a mesma origem do meu servidor, então não vou ter problema em relação a isso.

[03:47] Porém, lá no site do Mozilla, ele dá um exemplo assim, aqui temos um “http://store.company.com/dir/page.html”, e ele dá um exemplo do que é mesma origem e do que são origens diferentes também.

[04:02] Para entendermos um pouco, ele entende como mesma origem mesmo quando temos paths diferentes. Observe que aqui temos o “dir” e no outro temos o “dir2”. Esse “dir2”, por mais que ele seja um path diferente, se observarmos, o host aqui é o mesmo, e provavelmente a porta que ele está utilizando é a mesma também, mesmo que seja outra página. Nesse caso ele vai permitir.

[04:29] Outro exemplo de mesma origem também é quando eu tenho paths diferentes. Eu tenho aqui “store.company.com/dir/inner”, então aqui já mudou, “/dir/page.html”, ele foi para outra página dessa aplicação desse exemplo. Isso ele considera como mesma origem, pode liberar as informações, os recursos.

[04:55] O que acontece quando temos protocolos diferente? Ele entende como origens diferentes. Então por mais que eu tenha aqui um “http://store.company.com/dir/page.html”, aqui eu tenho “https”, ele já vai entender que é um protocolo diferente.

[05:11] Ou se eu estiver utilizando uma porta diferente, uma está utilizando http na porta 80 por default e essa aqui eu estou utilizando na porta 81, por exemplo, ele vai entender, isso pode ser outra aplicação, não libera, isso vai violar as políticas de mesma origem.

[05:30] Ou quando eu tenho host diferente. Observe que eu tenho “news.company.com/dir/page.html”, esse “news.company.com” já garantiu um host diferente, então eu não vou conseguir acessar.

[05:42] Olha que interessante, temos uma aplicação React feita para consumir os cursos da nossa aplicação em Django, só que nós não conseguimos consumir, porque existe essa política de mesma origem. Então é um erro que acontece do lado do front-end, mas quem deve resolver é o pessoal do back-end.

[06:04] O que nós desenvolvedores back-end, que criamos a nossa API em Django REST, precisamos fazer? Precisamos informar para a nossa API que vamos utilizar compartilhamento cruzado na nossa API, que vamos utilizar o CORS, e identificar quais são as origens que vamos permitir esse compartilhamento cruzado.

[06:26] Eu vou falar assim: “O localhost:3000 é um local que você pode confiar, pode liberar o acesso. Qualquer outra aplicação diferente disso eu não quero liberar o acesso da minha API”.

[06:40] O que nós vamos fazer na sequência? Vamos configurar a nossa API do lado do Django para conseguir atender o projeto feito em React.

### CORS no Django

[DOCUMENTAÇÃO]('https://pypi.org/project/django-cors-headers/')

Para funcionar nosso projeto de REAACT precisamos instalar DJANGO-CORS-HEADERS

    pip install django-cors-headers

No SETTINGS.PY:

    INSTALLED_APPS = [
        ...
        'corsheaders',
        ...
    ]

    MIDDLEWARE = [
        ...
        'corsheaders.middleware.CorsMiddleware',
        'django-middleware.common.CommonMiddleware',
        ...
    ]

    CORS_ALLOWED_ORIGINS = [
        "http://localhost:3000",
    ]

---

[00:00] Vamos configurar a nossa API Django para que o compartilhamento de recursos entre origens diferentes seja permitido.

[00:09] Existe uma biblioteca chamada django-cors-headers, ela vai ser responsável por fazer esse meio de campo para nós, não vamos precisar realizar toda essa verificação na mão, já existe uma biblioteca específica para isso, que é essa django-cors-headers. Vou copiá-la e vou seguir a documentação para conseguirmos instalá-la.

[00:30] Primeiro passo, pip install django-cors-headers, vou colar aqui. Deixa eu minimizar ali do lado, só para conseguirmos ver melhor. Dou um “Enter”, vai instalar super rápido, já instalou.

[00:44] O que eu vou fazer agora vai ser seguir o que está escrito na documentação, depois o que vamos precisar fazer é colocá-lo na configuração dos nossos apps instalados. Então abrindo aqui, vamos no “setup > settings.py”.

[01:00] Aqui nos apps instalados, se scrollarmos, no meu está na linha 32, temos todos esses apps, que são os apps desse projeto Django, eu vou copiar e vou colocar, ’corsheaders’,, aqui dentro. Já instalamos, já colocamos nos apps instalados, vamos precisar colocar no Middleware também.

[01:17] E aqui ele tem uma informação interessante, esse “CorsMiddleware” é importante gerá-lo o mais alto possível, antes mesmo desse “CommonMiddleware” ou do “WhiteNoise”.

[01:35] Por quê? Porque a ordem do Middleware que nós vamos colocar na nossa aplicação vai fazer diferença no nosso funcionamento também, então antes desse “CommonMiddleware” nós vamos colocar a configuração do Django CORS, que é essa aqui, ’corsheaders.middleware.CorsMiddleware’,. Vou colocá-la aqui. Salvei.

[01:58] E agora faremos o quê? Temos tipos de configurações diferentes, então aqui ele vai especificar, vai dizer quais são os domínios onde vamos permitir que a nossa aplicação possa ser compartilhada.

[02:19] Eu vou copiar toda essa linha do CORS_ALLOWED_ORIGINS = [, vou lá para o final da página mesmo e vou colocá-la aqui embaixo. Eu vou tirar essa aqui, ”http://127.0.0.1:9000”, vou deixar só a que está com “localhost”, para fazermos a nossa alteração.

[02:33] Se observarmos, a nossa aplicação React roda na porta 3000, então vou colocar aqui na porta 3000. E observe algo muito interessante, se eu copiar e colar e deixar o 3000 com uma barra, teremos um erro aqui, não podemos passar a barra no final do CORS_ALLOWED_ORIGINS, as origens que queremos permitir esse compartilhamento cruzado.

[03:00] Então tirei a barra, não tem a barra aqui no final. O que eu vou fazer vai ser subir o meu servidor, python manage.py runserver, volto na minha aplicação React, atualizo e nós recebemos um erro.

[03:16] Por que estamos recebendo esse erro? Esse erro não é por conta do React, mas sim por conta das permissões que temos na nossa aplicação. O lado do React não tem uma classe para fazer a verificação, para saber se eu sou um usuário que pode acessar ou não. Então o que vamos fazer? Eu vou alterar.

[03:34] Lembra que temos uma permissão aqui que vai verificar quantas vezes um usuário anônimo pode fazer requisições na nossa aplicação? Eu vou usá-la. Vou comentar essas linhas do ’DEFAULT_PERMISSION_CLASSES’ até o ’DEFAULT_AUTHENTICATION_CLASSES’, eu não vou apagar, só vou comentar e vou ativar ‘DEFAULT_THROTTLE_CLASSES’ E ‘DEFAULT_THROTTLE_RATES’ que vou tirar aqui o comentário daquela nossa classe de permissões anônimas, e vou aumentar, vou deixar com 100 permissões por dia ‘anon’: ‘100/day’

[Aula5_video2_imagem4]

[04:05] Se eu tiro essa parte de permissões, a minha aplicação vai estar sempre disponível para qualquer pessoa, mas eu quero colocar aqui um limite, só para termos um pouco o controle para onde estamos liberando a nossa API. Fique à vontade se você quiser tirar essa parte do Rates de requisições anônimas também na sua aplicação.

[04:27] Alterei aqui para 100, vou atualizar a parte do React e está lá, temos Python Fundamentos, Python/React, as descrições de todos os cursos que temos na nossa API também.

[04:40] Para conseguirmos disponibilizar esse compartilhamento cruzado, é necessário instalarmos o django-cors-headers, façamos toda essa configuração e digamos: “Eu tenho a minha API, ela está funcionando, está tudo certo e eu posso compartilhar recursos da minha API com essas aplicações”.

[05:02] Então se você está criando mais de uma aplicação ou se você está dividindo a sua aplicação em back-end, front-end e está ficando bem legal, você pode usar esse sistema de segurança.

[05:14] A minha API roda numa porta diferente, então nós já estaríamos com outra política mesmo, não estamos na política de mesma origem, estamos com uma origem diferente. Mesmo assim conseguimos consumir, porque nós permitimos, falamos dentro das nossas configurações, do lado do Django REST: “Pode confiar nessas outras aplicações”. E aqui temos uma aplicação front-end super simples consumindo os dados do Django REST Framework.

### Permitindo compartilhamento

Uma equipe desenvolveu uma API com Django Rest que seria usada por 3 sistemas front-end diferentes. Pensando nisso, realizaram toda a configuração do CORS no Django. Porém, no lugar de configurar cada sistema conforme ilustra o código abaixo:

código 1

    CORS_ALLOWED_ORIGINS = [
        "http://sistema1:3000",
        "http://sistema2:9000",
        "http://sistema3:5000",
    ]

Eles optaram por configurar usando o seguinte código:

código 2

    CORS_ORIGIN_ALLOW_ALL = True

Analisando as linhas de código acima, escolha as alternativas que apresentam os possíveis resultados.

a) A forma usada pela equipe permitirá o compartilhamento de recursos apenas para as 3 aplicações front-end.

b) **Alternativa correta:** A forma usada pela equipe permitirá o compartilhamento de recursos para qualquer aplicação.
- _Alternativa correta! Com esse comando, o compartilhamento de recursos cruzados estará disponível à qualquer aplicação._

c) **Alternativa correta:** Tanto o código 1 como o código 2, atenderão às 3 aplicações front-end.
- _Alternativa correta! Certo! As aplicações front-end usarão a API com o código 1 ou 2._

### O que aprendemos?

- Entendemos a importância da política de mesma origem e como compartilhar recursos de origens diferentes configurando o CORS;
- Configuramos o CORS do Django Rest e integramos a API Django Rest com uma aplicação React.
