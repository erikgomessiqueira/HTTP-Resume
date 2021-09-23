# HTTP

## Entendendo

HTTP significa HyperText Transfer Protocol que traduzindo significa Protocolo de Transferência de HyperTexto.

### Visão Geral

- Permite a troca de informações e dados na internet.
- Uma troca de mensagens.
- Requisita e envia os recursos(HTML, CSS, Scripts, Imagens, Vídeos, ...).
- Uma chamada para cada uma desse recursos.

### Visualizando a comunicação

A "conversa" entre Browser(Navegador/Cliente) e o Servidor ocorre da seguinte forma:

1. O Browser faz um pedido (**Request**) ao Servidor.
2. O Servidor entrega uma resposta (**Response**) ao Browser.

De forma simples é como se fosse uma troca de mensagens, mas o que é importante é a mensagem (**Message**) trocada entre os dois, vamos ver mais sobre ela.

#### Message 

Existem alguns tipos de mensagem (Message) que iremos abordar.

##### Pedido/Request

É composto por três divisões:

- ***Methods***/Métodos => ele vai definir o tipo do meu pedido, ou seja, qual ação eu quero fazer no servidor. Vamos mostrar dois tipos de métodos:
  - **GET** => Pegar um recurso.(get seria o verbo pegar em português)
  - **POST** => Criar um recurso.(post traduzido seria postar/enviar, mas nesse caso criar)
- **Header** => veremos a seguir.
- **Body** => veremos a seguir.

##### Resposta/Response

É composto por três divisões:

- ***Status Code*** => é a resposta do servidor sobre o estado do pedido, se deu certo, errado ou outro caso. Vamos mostrar alguns tipos de status:
  - **200** => Tudo certo (OK).
  - **301** =>  Redirecionado.
  - **404** => Not found. (Não encontrado)
  - **500** => Erro interno do servidor.
- **Header** => veremos a seguir.
- **Body** => veremos a seguir.

##### Request/Response

As opções Body e Header são opcionais. Podem receber parâmetros ou não dependendo co caso.

###### Header

São campos informativos que recebem parâmetros do tipo **propriedade: valor**.

```json
Content-Type: application/js /*Tipo de conteudo*/
	//ou
User-Agent: Chrome /*Cliente*/
	//ou
Request URL: www.google.com /*URL do pedido*/
```



###### Body

São campos recebem ou enviam conteúdo.

- HTML
- Conteúdo
- JSON

### Visualizando com DevTools

O DevTools é uma ferramenta nos navegadores para desenvolvedores no Chrome e derivados essa ferramenta é acessada pelo atalho **F12**. Para visualizarmos o que qeuremos vamos na aba network e acessar o site novamente ou reiniciar a página(F5), isso ativará as conexões e podemos velas acontecendo em tempo real.

Escolhendo um e clicando sobre ele é possível ver as abas com as opções como Header, Preview, Response ..., com isso podemos ver o que foi requerido e a resposta  obtida.

### Visualizando com cURL

É uma ferramenta que já é instalada por padrão em sistemas Unix, se estiver usando o Windows baixe o Git Bash. Ele é uma ferramenta para transferir dados de ou para um servidor, usando um dos protocolos suportados:

- DICT
- FILE
- FTP
- FTPS
- GOPHER
- HTTP
- HTTPS
- IMAP
- IMAPS
- LDAP
- LDAPS
- POP3
- POP3S
- RTMP
- TSP
- SCP
- SFTP
- SMB
- SMBS
- SMTP
- SMTPS
- TELNET
- TFTP

É um comando usado para trabalhar sem a interação com o usuário.

Para saber mais use o comando:

```bash
man curl 
```

 Para  usá-lo fazemos da seguinte forma:

```bash
# comando protocolo://dominio
curl https://www.google.com.br
```

E assim também podemos observar que ele consegue pegar detalhes que o próprio DevTools não consegue.

Para obtermos os Headers e o Body usamos:

```bash
curl -i https://www.google.com.br
```

Para obtermos todas as informações dos Headers ao mesmo tempo e o Body usamos:

```bash
curl -v https://www.google.com.br
```

Para obtermos somente os Headers de resposta/response:

```bash
curl -I https://www.google.com.br
```

Para escolhemos o método HTTP:

```bash
#comando parametro(-X) metodo URL
curl -X GET https://www.google.com.br

#retorna o cabecalho
curl -X GET https://www.google.com.br -i
```



## Conceitos 

#### Simples

Deve ser legível por qualquer pessoa.

####  Cliente e servidor

Você faz uma requisição(request/pedido) e recebe uma resposta(response) do servidor.

####  Statelees

Statelees significa não guarda um estado, ou seja, **não guarda informações**. Não existe relações entre conexões, uma não depende da outra, cada uma ocorre separadamente e **são independentes**.

####  Sessões

É uma forma de guardar informações para a próxima conexão, isso pode ser feito atravez de Cookies ou Storages. Por exemplo informações de login não podem ser requisitadas toda vez que uma nova pagina é acessada, as sessões aramzenam esses tipo de dados e solucionam esse problema.

#### Extensível

Atravé do cabeçalho podemos fazer diversas trocas de informações entre o cliente e servidor, de acordo com a necessidade. E podemos receber e enviar dados com o Body na requisições.

### Cliente

O cliente é o User Agent, ou seja, a entidade que da inicio a comunicação(faz o pedido/requisição/request), ele pode ser o Browser(Navegador) ou cURL  ou vários outro que iniciam a comunicação.

Esses pedidos são feitos atravéz das ações dos clientes, ou seja os métodos de requisição:

- GET
- POST
- PUT
- DELETE

### Serividor 

Se apresenta como uma maquina no mundo que está preparada para receber e a requisição e processar uma resposta. Lembrando que também existe a possibilidade de varios servidores se apresentarem como apenas uma máquina, pois voê pode fazer a requisição a um servidor mas o processo de retornar a resposta depende de varios outros servidores. 

A **resposta** pode ser **enviada** pelo **header** atravéz de um Status Code (404, 500, etc..), ou pelo **body**.

### Proxies

São representantes que ficam entre o cliente e servidor e ajudam a fazer o transporte de dados.

Ele possui diversas funções:

- Cache => ele define um parâmetro que ao invéz de fazer todo o fluxo de transferência, ele verifica se algum proxy tem essa informação e retorna ela mais rápido.
- Filtro => faz um filtro do que pode ser acessado(requisitado) ou não, essa função pode ser usada em antivírus e controle parental, inpedindo o usuário de acessar/requisitar um site.
- Load balancing(distribuição de carga) => quando fazemos a requisição e a resposta é gerenciada/distribuída pelos proxies para que chegue mais rápida.
- Autenticação
- Autorização

## URI

**URI** é a sigla para **U**niform **R**esource **I**dentifier(Identificador de Recurso Uniforme ou Unico).

Para identificar esse recurso podemos usar o seu **Nome** ou **Localização**.

### Resource/Recurso

É o alvo do pedido HTTP, ele pode ser qualquer coisa identificável e tambem podemos chamá-lo de Entidade. Vamos ver alguns de seus tipos e exemplos:

- **Digital** => **Email** => acessado por **mailto:email@dominio.com**. (Existe na forma digital)
- **Abstrata** => Uma **Sessão** ou **Autenticação**. (Exsite um caminho abstrato que leva até esse recurso/resource)
- **Físicos** => **Produtos** ou **Usuários**.(Exeistem na forma física/real)

E podemos nomear, identificar, endereçar ou manipular, estamos falando de um recurso.

### URL

**URL** é a sigla para **U**niform **R**esource **L**ocator (Localizador de Recurso Uniforme ou Unico), ele localiza o recurso atravéz de seu **_endereço_**. Essa URL deve ser composta por alguns componentes.

***Obrigatórios***:

- **Protocolo** => HTTP, HTTPS, ...
- **Domínio** => google.com, youtube.com, ...

> protocolo://dominio

> **https** ://www. **google.com.br**

 ***Opcionais***:

- **Subdomínio** =>  vem antes do domínio => www.

  > https:// **www** .google.com.br

- **Path** => Caminho de um recurso específico.

- **Parâmetros** => de forma simples são variaveis que usamos na URL. Elas vem após um ponto de interrogação( **?** ), passando uma chave(ex:' **v** ') recebendo(' **=** ') um valor('**OlaMundo**')

  > **?v=OlaMundo**

- **Porta** => Em domínios escritos em IP as portas são identificadas após os dois pontos( **:** ), essa porta pode estar aberta ou fechada, sendo que fechada não é possivel acessar o recurso. Usando o HTTP e o HTTPS temos algumas portas definidas por padrão que serão usadas caso uma porta específica não for informada:

  - HTTP => :80
  - HTTPS => :443

  > **http**:// 192.168.0.1:8845
  >
  > **https**:// 192.168.0.1:8888
  >
  > **http**:// 192.168.0.1 => http:// 192.168.0.1:80
  >
  > **https**:// 192.168.0.1 => https:// 192.168.0.1:443

- Âncora => Direciona para uma parte específica dentro do site, ou recurso que foi pedido. Ela composta por um "Jogo da Velha"( **#** ) e um identificador.

  > #IdDiv02

Exemplo geral:

|   https   |    www     | youtube.com | /watch | ?v=IhV5q3mu6fo |
| :-------: | :--------: | :---------: | :----: | :------------: |
| Protocolo | Subdomínio |   Domínio   |  Path  |   Parâmetros   |

------



|   http    | 192.168.0.1 | :8845 |     /      | index.html | #IdDiv02 |
| :-------: | :---------: | ----- | :--------: | :--------: | :------: |
| Protocolo |     IP      | Porta | Path(Root) |  Arquivo   |  Âncora  |



### URN

**URN** é a sigla para **U**niform **R**esource **N**ame(Nome do Recurso Uniforme ou Unico), ele localiza o recurso atravéz de seu **_Nome_**. Não vamos usar muito, então caso precise procure.

## Messages

São mensagens enviadas do servidor, podendo ser um request ou respose, o seu uso começou no HTTP/1.1 que era em formato de texto e bem legível, já no HTTP/2 que é mais moderno usamos uma estrutura binária o que deixa a estrutura menos legível mas é melhor para a optimizações, porém no final ela funciona da mesma maneira da da versão HTTP/1.1.

### Request

É o pedido/requisição que fazemos ao servidor. É composto por: request line, body, headers.

#### Request Line

Ele é composto por:

* Método(Method[GET, POST, ...])
* Protocol version(Versão do protocolo)
* URI

#### Body

Depende do tipo de requisição feita.

#### Headers

Os headers da requisição é preenchido automaticamente pelo **browser**. 

Todas essas informações podem ser obtidas utilizando o comando:

```bash
curl -v https://www.google.com.br

#Trecho que queremos

> GET / HTTP/2
> Host: www.google.com.br
> user-agent: curl/7.68.0
> accept: */*

```

### Response

É a resposta enviada pelo servidor, mesmo se a requisição dar certo ou não. Ela é composta por: Protocol Version, Status Code, Headers, Status message.

#### Protocol Version

Versão do protocolo

#### Status Code

Código de status que diz o que aconteceu com a requisição, se deu certo, errado, deu certo mas a página não foi encontrada, e etc... 

#### Status message

Corpo da resposta que acompanha o status code, ou seja, é o próprio Body da resposta e é enviado pelo servidor.

#### Headers

Os headers da resposta/response é preenchido automaticamente pelo **servidor**. 

## Methods

### HTTP Methods

Define um conjunto de **métodos HTTP**, métodos/methods **indicam a ação** que o cliente deseja fazer. Também podem ser chamados de **Verbos HTTP**, pois o nome dos métodos/methods mais usados são verbos da língua inglesa(mas alguns não) e cada um tem a sua semântica/significado. Vamos ver algumas características:

#### Seguro

* Não altera o estado no servidor, ou seja, o documento é de somente leitura, onde o original não é alterado.
* O cliente não pede alterações, ele pede uma página e não há uma carga extra para o servidor.
* O servidor é o responsável por manter os métodos/methods seguros.
* Esses métodos são:
  * **GET** => GET/search.html HTTP/1.1
  * **HEAD** 
  * **OPTIONS**

#### Idempotente

* Ao executar o método a resposta é sempre a mesma.

* Esse métodos/methods são:

  * Todos os métodos **Seguros**(GET, HEAD e OPTIONS)
  * **PUT** => não é seguro pois ele **atualiza** algum recurso e muda o estado no servidor.
  * **DELETE** => não é seguro pois ele **deleta** algum recurso e muda o estado no servidor.

* O status code poderá ser diferente.

* O servidor deve retornar os dados da mesma maneira.

* Essa especificação não é garantia que todos os servidores aplicarão o conceito de forma correta, mas deveriam.

* **IDEMPOTENCE**

  | HTTP METHOD | IDEMPOTENCE | SAFETY/SEGURO |
  | :---------: | :---------: | :-----------: |
  |     GET     |     YES     |      YES      |
  |    HEAD     |     YES     |      YES      |
  |     PUT     |     YES     |      NO       |
  |   DELETE    |     YES     |      NO       |
  |    POST     |     NO      |      NO       |
  |    PATCH    |     NO      |      NO       |

  

### Instalando o JSON Server

Link para o [repositório](https://github.com/typicode/json-server).

Agora falaremos sobre os Methods ou Verbos HTTP.

### OPTIONS

Ele nos informa sobre a disponibilidade dos métodos da requisição, ou seja, quais métodos/methods podem ser usados naquela URI.

#### Características

* É seguro.
* É idempotente.
* Não recebe(response) ou envia(request) um Body.
* Não é usado em formulários HTML.
* Não é cacheable, ou seja, não guarda cache(dados pré-definidos na memória).

#### Escrita

* OPTIONS /index.html HTTP/1.1
* OPTIONS * HTTP/1.1

#### Comando

Use o comando para obter os dados:

```bash
curl -X OPTIONS http://localhost:3000/posts -i

#Retorno

HTTP/1.1 204 No Content
X-Powered-By: Express
Vary: Origin, Access-Control-Request-Headers
Access-Control-Allow-Credentials: true
##############################################################
Access-Control-Allow-Methods: GET,HEAD,PUT,PATCH,POST,DELETE
##############################################################
Content-Length: 0
Date: Thu, 23 Sep 2021 17:12:30 GMT
Connection: keep-alive
Keep-Alive: timeout=5

```



### GET

Serve para pegar(get) um recurso, ele apenas recebe dados.

#### Características

* É seguro.
* É idempotente.
* Não envia um Body, mas recebe no response.
* É usado em formulários HTML.
* É cacheable, ou seja, guarda cache.

#### Escrita

* OPTIONS /index.html HTTP/1.1
* OPTIONS * HTTP/1.1

#### Comando

Use o comando para obter os dados:

```bash
# O método GET é o padrão no curl então não precisamos adicionar.

curl -v http://localhost:3000/posts    

#Headers
*   Trying ::1:3000...
* TCP_NODELAY set
* connect to ::1 port 3000 failed: Conexão recusada
*   Trying 127.0.0.1:3000...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 3000 (#0)
#################################################################
> GET /posts HTTP/1.1
#################################################################
> Host: localhost:3000
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< X-Powered-By: Express
< Vary: Origin, Accept-Encoding
< Access-Control-Allow-Credentials: true
< Cache-Control: no-cache
< Pragma: no-cache
< Expires: -1
< X-Content-Type-Options: nosniff
< Content-Type: application/json; charset=utf-8
< Content-Length: 77
< ETag: W/"4d-49G7XbVRP2NKipc5uj9Z4hcUq3Y"
< Date: Thu, 23 Sep 2021 17:14:41 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
< 

#Response>>Body
[
  {
    "id": 1,
    "title": "json-server",
    "author": "typicode"
  }
* Connection #0 to host localhost left intact
]

```

### HEAD

É parecido com o método GET porém recebemos apenas o Header(Cabeçalho).

#### Características

* É seguro.
* É idempotente.
* Não envia e não recebe Body.
* Não é usado em formulários HTML.
* É cacheable, ou seja, guarda cache.

#### Escrita

* OPTIONS /posts

#### Comando

Use o comando para obter os dados:

```bash
# O parâmetro -I retorna apenas o cabeçalho como o método HEAD 

curl -I http://localhost:3000/posts

#Headers
HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 77
ETag: W/"4d-49G7XbVRP2NKipc5uj9Z4hcUq3Y"
Date: Thu, 23 Sep 2021 17:33:49 GMT
Connection: keep-alive
Keep-Alive: timeout=5

```

### POST

Publica/Cadastra um recurso.

#### Características

* Não é seguro.
* Não é idempotente.
* Envia Body no request e pode ou não receber um Body no response.
* É usado em formulários HTML.
* Pode ser cacheable ou não, depende do header.

#### Comando

Use o comando para obter os dados:

```bash
curl -d ' { "id": 2, "title": "json-server-2", "author": "Erik" }' -H "Content-type:application/json" -X POST http://localhost:3000/posts

#Response
{
  "id": 2,
  "title": "json-server-2",
  "author": "Erik"
}

# O parâmetro -H é para configurar os Headers.
# O parâmetro -d é para enviar o Body/dados.
# O parâmetro -X é para definir o Método.

```

### PUT

Cria novo recurso ou atualiza um recurso existente. Se diferencia do POST por ser idempotente. É visto que o método PUT é mais usado para atualizar do que criar um recurso, o POST é mais usado para criação, mas caso use ele o Status Code para sucesso na criação do recurso é 201 e para atualização o Status Code será 200 ou 204.

#### Características

* Não é seguro.
* É idempotente.
* Envia Body no request, mas não recebe um Body no response.
* Não é usado em formulários HTML.
* Não é cacheable.

#### Escrita

* PUT /profile HTTP/1.1

#### Comando

Use o comando para obter os dados:

```bash
curl -d ' { "name":"Erik"}' -H "Content-type:application/json" -X PUT http://localhost:3000/profile -i

#Headers
#################################################################
HTTP/1.1 200 OK
#################################################################
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 20
ETag: W/"14-tX+isMZyD28UhAlPCGneR38K9mg"
Date: Thu, 23 Sep 2021 18:25:01 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{
  "name": "Erik"
}                 

#Caso use o curl ele retorna um body(Como no exemplo acima) no response, mas a documentação diz que não a Body na resposta, porém varia com a implementação de cada um.

# O parâmetro -H é para configurar os Headers.
# O parâmetro -d é para enviar o Body/dados.
# O parâmetro -X é para definir o Método.

```

### PATCH

Modifica parcialmente um recurso. Sua diferença para o PUT é que o PATCH modifica algumas propriedades do recurso e o PUT faz uma atualização, ou seja, todas as propriedades do recurso.

#### Características

* Não é seguro.
* Não é idempotente.
* Envia Body no request e recebo um Body no response.
* Não é usado em formulários HTML.
* Não é cacheable.

#### Escrita

* PATCH /posts HTTP/1.1

#### Comando

Use o comando para obter os dados:

```bash
curl -d ' { "title":"my-json-title"}' -H "Content-type:application/json" -X PATCH http://localhost:3000/posts/1

# O no final /1 indica qual a posição do objeto que será modificado no array

#Response
{
  "title": "my-json-title",
  "id": 1,
  "author": "typicode"
}

```

### DELETE

Remove um recurso. Ele responde os seguintes Status Code:

* 202 => Accepted(Aceito).
* 204 => No content(Sem conteúdo de resposta).
* 200 => OK

#### Características

* Não é seguro.
* É idempotente.
* Pode ser que precise enviar um Body no request e pode ser que você receba um Body no response.
* Não é usado em formulários HTML.
* Não é cacheable.

#### Escrita

* DELETE /posts HTTP/1.1

#### Comando

Use o comando para obter os dados:

```bash
curl -X DELETE http://localhost:3000/posts/2 -i

#Headers
HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 2
ETag: W/"2-vyGp6PvFo4RvsFtPoIWeCReyIC8"
Date: Thu, 23 Sep 2021 19:23:34 GMT
Connection: keep-alive
Keep-Alive: timeout=5

```

## Headers

Headers ou cabeçalhos na tradução, são informações adicionais para o pedido ou resposta. É um tipo de dado propriedade valor, veja o exemplo:

* propriedade:valor
* content-type:application/json
* Content-Type: text/html

### Headers por contextos

Vamos dividir os Headers em três categorias.

#### General

É um agrupamento geral de headers que servem tanto para o request quanto para o response. Nele geralmente temos:

* **Request URL**: https://www.google.com.br/ (URL do pedido)

* **Request Method**: GET (Método HTTP)

* **Status Code**: 200 (Código de Status)

* **Remote Address**: [2800:3f0:4001:834::2003]: 443 (Endereço remoto)

* **Referrer Policy**: strict-origin-when-cross-origin (Referência onde passa os dados, com esse valor não se pede detalhes, somente quem está enviando)

#### Request headers

São os headers somente do request/requisição. Vamos ver alguns:

* **:authority**: www.google.com.br(Autoridade do pedido, servidor do pedido)
* **:method**: GET (Método HTTP)
* **:path**: / (Caminho, nesse caso /)
* **:scheme**: https (Protocolo)
* **accept**:text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9(Tipo de pedidos que podem ser feitos a essa URL)
* **accept-encoding**: gzip, deflate, br(Pede a resposta de forma compactada, para enviar de uma forma mais rápida)
* **cookie**: HSID=ADX6xdKWnHAHDYhbc; SSID=Ao74cAtkNLh48CGGb;(São dados armazenados que serviram para outras operações acontecerem)

#### Response Headers

São os headers somente do response/resposta. Vamos ver alguns:

* **cache-control**: private, max-age=0(O controle de cache é privado e tem uma idade máxima de 0 segundos)
* **content-length**: 41293(O tamanho do conteúdo é de 41293 bytes)
* **content-type**: text/html; charset=UTF-8(Tipo da reposta enviada)
* **content-encoding**: br(A códificação do conteúdo da resposta é português brasileiro)
* **date**: Thu, 23 Sep 2021 22:27:58 GMT(data que a resposta foi feita)
* **set-cookie**: 1P_JAR=2021-09-23-22; expires=Sat, 23-Oct-2021 22:27:58 GMT;(Sete esse cookie no navegador)

### Dev Docs

Usamos o Dev Docs para checar varias documentações ao mesmo tempo.

#### [Site](https://devdocs.io/)

#### [Aplicativo Desktop](https://www.electronjs.org/apps/devdocs-app)

## Status Code

Vamos ver alguns tipos de status code:

### 100

* 100: Continue

### 200

* 200: OK(GET, POST)

* 201: Created (PUT)

* 204: No Content (DELTE, PUT)

### 300

* 301: Moved Permanently

* 308: Permanent Redirect

* 302: Found

* 307: Temporary Redirect

### 400

* 400: Bad Request
* 401: Unauthorizad
* 403: Forbidden
* 404: Not Found
* 405: Method Not Allowed
* 429: Too Many Requests

### 500

* 500: Internal Server Error
* 503: Service Unaviable





















