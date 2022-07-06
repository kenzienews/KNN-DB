# KNN-DB
# Bem vindo KNN!

Este é o backend da aplicação Kenzie News Network - site de noticias que visa facilitar o contato entre novos jornalistas e empresas.


# Endpoints

A API tem um total de 9 endpoints, sendo em volta principalmente dos artigos - podendo cadastrar seu perfil como user jornalista, empresa e leitor.  
O JSON para utilizar no Insomnia pode ser baixado aqui ->  [https://drive.google.com/file/d/1g6OP43uklOUQK3iciI3_yCCjytXJ3_6k/view?usp=sharing](https://drive.google.com/file/d/1g6OP43uklOUQK3iciI3_yCCjytXJ3_6k/view?usp=sharing)  Para importar o JSON no Insomnia é só clicar na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > Import from File > e escolher o local onde foi salvo o arquivo"  ✌️

O url base da API é  [https://knn-db.herokuapp.com/](https://knn-db.herokuapp.com/)

## Rotas que não precisam de autenticação

**Criação de usuário**

POST -> baseURL/register

Os dados solicitados pela API são:

    {
    	"email": "email@asdf",
    	"password": "123456"
    }

Em caso de sucesso na criação de usuário, é retornado a seguinte resposta:

    {
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsQGFzZGYiLCJpYXQiOjE2NTcwNDg4MDQsImV4cCI6MTY1NzA1MjQwNCwic3ViIjoiMyJ9.zCJiKqqSfv9vagbd1TIU96y22JTwa5oLv2wFQ5noGXo",
	"user": {
		"email": "email@asdf",
		"id": 3
	}
}

Response da api não cadastrado com sucesso:

| Situação | Mensagem |
|--|--|
|Caso e-mail já exista na base de dados | "Email already exists" |
|Caso não digita um e-mail ou senha|"Email and password are required"|
|Caso a senha não tenha, no mínimo de 4 dígitos|"Password is too short"|


**Login de usuário**

POST -> baseURL/login

Os dados solicitados pela API são:

    {
    	"email": "email@asdf",
    	"password": "123456"
    }

Em caso de sucesso na criação de usuário, é retornado a seguinte resposta:

    {
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsQGFzZGYiLCJpYXQiOjE2NTcwNDkyMzEsImV4cCI6MTY1NzA1MjgzMSwic3ViIjoiMyJ9.ZKXUxgrSDK1v9kBj1QZJjGtq9QNxD3dGMT1lQNNVq-g",
	"user": {
		"email": "email@asdf",
		"id": 3
	    }
    }

Caso haja necessidade, o "accessToken" pode ser usado para ser armazenado no localStorage.

Response da api caso login não seja efetuado com sucesso:

| Situação | Mensagem |
|--|--|
|Caso esteja faltando e-mail ou senha | "Email and password are required" |
|Caso e-mail errado ou inválido|"Cannot find user"|
|Caso senha errada|"Incorrect password"|
|Caso senha abaixo de 4 caracteres:|"Password is too short"|

**Listar todos os artigos postados**

Nesse endpoint é possível ver todos os artigos postados na api

GET-> baseURL/articles

    [
        {
            "source": {
                "name": "Globo"
            },
            "authorId": 1,
            "title": "Inflação do Brasil está entre as mais altas do mundo, aponta OCDE; veja comparativo - Globo",
            "description": "Na conjunto de países do grupo G20, taxa anual atingiu 8,8% em maio, contra 11,7% no Brasil. Entre as grandes economias, apenas Turquia, Argentina e Rússia também possuem inflação acima de 10% ao ano.",
            "url": "https://g1.globo.com/economia/noticia/2022/07/05/inflacao-do-brasil-esta-entre-as-mais-altas-do-mundo-aponta-ocde-veja-comparativo.ghtml",
            "urlToImage": "https://s2.glbimg.com/c6BZPgFXO1_W6EJwH2GIPxs3Ag8=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/z/0/sDKKB2Q9ir0grLPc3fGA/fta20220618131.jpg",
            "publishedAt": "2022-07-05T15:28:12Z",
            "content": "Novo relatório divulgado pela OCDE (Organização para a Cooperação e Desenvolvimento Econômico) mostra que a inflação do Brasil segue entre as maiores do mundo e bem acima da média das grandes economi… [+2191 chars]",
            "id": 1
        }
    ]

**Listar artigos com paginação**

Nesse endpoint é possível listar todos artigos, com o parametro "_page" criamos uma paginação e com o "_limit" definimos quantos artigos estão dispostos por pagina.

GET-> baseURL/articles?_page=1&_limit=1 

    [
        {
            "source": {
                "name": "Globo"
            },
            "authorId": 1,
            "title": "Inflação do Brasil está entre as mais altas do mundo, aponta OCDE; veja comparativo - Globo",
            "description": "Na conjunto de países do grupo G20, taxa anual atingiu 8,8% em maio, contra 11,7% no Brasil. Entre as grandes economias, apenas Turquia, Argentina e Rússia também possuem inflação acima de 10% ao ano.",
            "url": "https://g1.globo.com/economia/noticia/2022/07/05/inflacao-do-brasil-esta-entre-as-mais-altas-do-mundo-aponta-ocde-veja-comparativo.ghtml",
            "urlToImage": "https://s2.glbimg.com/c6BZPgFXO1_W6EJwH2GIPxs3Ag8=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/z/0/sDKKB2Q9ir0grLPc3fGA/fta20220618131.jpg",
            "publishedAt": "2022-07-05T15:28:12Z",
            "content": "Novo relatório divulgado pela OCDE (Organização para a Cooperação e Desenvolvimento Econômico) mostra que a inflação do Brasil segue entre as maiores do mundo e bem acima da média das grandes economi… [+2191 chars]",
            "id": 1
        }
    ]

**Listar artigos Reportados**

Nesse endpoint é possível listar todos os artigos que foram reportados por usuarios.

GET-> baseURL/reported

	[
		{
			"source": {
				"name": "Globo"
			},
			"authorId": 1,
			"title": "Inflação do Brasil está entre as mais altas do mundo, aponta OCDE; veja comparativo - Globo",
			"description": "Na conjunto de países do grupo G20, taxa anual atingiu 8,8% em maio, contra 11,7% no Brasil. Entre as grandes economias, apenas Turquia, Argentina e Rússia também possuem inflação acima de 10% ao ano.",
			"url": "https://g1.globo.com/economia/noticia/2022/07/05/inflacao-do-brasil-esta-entre-as-mais-altas-do-mundo-aponta-ocde-veja-comparativo.ghtml",
			"urlToImage": "https://s2.glbimg.com/c6BZPgFXO1_W6EJwH2GIPxs3Ag8=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/z/0/sDKKB2Q9ir0grLPc3fGA/fta20220618131.jpg",
			"publishedAt": "2022-07-05T15:28:12Z",
			"content": "Novo relatório divulgado pela OCDE (Organização para a Cooperação e Desenvolvimento Econômico) mostra que a inflação do Brasil segue entre as maiores do mundo e bem acima da média das grandes economi… [+2191 chars]",
			"id": 1,
			"likes": 2,
			"reports": 1
		}
	]
    
## Rotas precisam de autenticação

**Criar novo artigo**

POST -> baseURL/articles

Os dados solicitados pela API são:

    {
        "source": {
            "name": "Globo"
        },
        "authorId": 1,
        "title": "Mario Frias é internado em Brasília e passa por novo cateterismo, após 'infarto agudo do miocárdio' - Globo",
        "description": "Segundo boletim médico, ex-secretário de Cultura do governo federal está na UTI do hospital Santa Lúcia, desde noite de segunda (4). Está é, pelo menos, a terceira vez que ele é internado com quadro similar.",
        "url": "https://g1.globo.com/df/distrito-federal/noticia/2022/07/05/mario-frias-e-internado-em-brasilia-e-passa-por-novo-cateterismo-apos-infarto-agudo-do-miocardio.ghtml",
        "urlToImage": "https://s2.glbimg.com/TxLXAcUoQH5eo-0kKPWcJcLeLzc=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2020/7/h/C23LnQQBOXN2kUWn4hsw/mario-frias.jpg",
        "publishedAt": "2022-07-05T14:41:15Z",
        "content": "O ex-secretário especial de Cultura do governo Jair Bolsonaro, Mario Frias, foi internado na noite de segunda-feira (4), com quadro de \"infarto agudo do miocárdio\". Segundo boletim médico divulgado n… [+789 chars]"
    }

source -> origem da noticia 
authorId -> id do criador

Em caso de sucesso, é retornado a seguinte resposta:

    {
	"source": {
		"name": "Globo"
	},
	"authorId": 1,
	"title": "Mario Frias é internado em Brasília e passa por novo cateterismo, após 'infarto agudo do miocárdio' - Globo",
	"description": "Segundo boletim médico, ex-secretário de Cultura do governo federal está na UTI do hospital Santa Lúcia, desde noite de segunda (4). Está é, pelo menos, a terceira vez que ele é internado com quadro similar.",
	"url": "https://g1.globo.com/df/distrito-federal/noticia/2022/07/05/mario-frias-e-internado-em-brasilia-e-passa-por-novo-cateterismo-apos-infarto-agudo-do-miocardio.ghtml",
	"urlToImage": "https://s2.glbimg.com/TxLXAcUoQH5eo-0kKPWcJcLeLzc=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2020/7/h/C23LnQQBOXN2kUWn4hsw/mario-frias.jpg",
	"publishedAt": "2022-07-05T14:41:15Z",
	"content": "O ex-secretário especial de Cultura do governo Jair Bolsonaro, Mario Frias, foi internado na noite de segunda-feira (4), com quadro de \"infarto agudo do miocárdio\". Segundo boletim médico divulgado n… [+789 chars]",
	"id": 4
    }

**Criar comentario**

POST -> baseURL/comments

Os dados solicitados pela API são:

    {
		"ownerId": 1,
		"articleId": 1,
	    "content": "saudade macaco twelves, tenho que parar de ver gregnews e ver kenzie news "
    }

ownerId -> id de quem fez o comentario 
articleId -> id do artigo comentado

Em caso de sucesso, é retornado a seguinte resposta:

    {
	"ownerId": 1,
	"articleId": 1,
	"content": "saudade macaco twelves, tenho que parar de ver gregnews e ver kenzie news ",
	"id": 3
    }

**deletar artigo**

DELETE -> baseURL/articles/:id

Em caso de sucesso, é retornado a seguinte resposta:

    {}

**deletar comentario**

DELETE -> baseURL/comments/:id

Em caso de sucesso, é retornado a seguinte resposta:

    {}

**Reportar Artigo**

Nesse endpoint é possível adicionar um like em um artigo.

PATCH-> baseURL/articles/:id

{
	"likes": 3 
}

Em caso de sucesso, é retornado a seguinte resposta:

	{
		"source": {
			"name": "Globo"
		},
		"authorId": 1,
		"title": "Inflação do Brasil está entre as mais altas do mundo, aponta OCDE; veja comparativo - Globo",
		"description": "Na conjunto de países do grupo G20, taxa anual atingiu 8,8% em maio, contra 11,7% no Brasil. Entre as grandes economias, apenas Turquia, Argentina e Rússia também possuem inflação acima de 10% ao ano.",
		"url": "https://g1.globo.com/economia/noticia/2022/07/05/inflacao-do-brasil-esta-entre-as-mais-altas-do-mundo-aponta-ocde-veja-comparativo.ghtml",
		"urlToImage": "https://s2.glbimg.com/c6BZPgFXO1_W6EJwH2GIPxs3Ag8=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/z/0/sDKKB2Q9ir0grLPc3fGA/fta20220618131.jpg",
		"publishedAt": "2022-07-05T15:28:12Z",
		"content": "Novo relatório divulgado pela OCDE (Organização para a Cooperação e Desenvolvimento Econômico) mostra que a inflação do Brasil segue entre as maiores do mundo e bem acima da média das grandes economi… [+2191 chars]",
		"id": 1,
		"likes": 3,
		"reports": 1
	}

**Adicionar artigo a lista de Reportados**

Nesse endpoint é possível adicionar uma artigo ja denunciado a lista de reportados para futura analise.

POST-> baseURL/reported

	[
		{
			"source": {
				"name": "Globo"
			},
			"authorId": 1,
			"title": "Inflação do Brasil está entre as mais altas do mundo, aponta OCDE; veja comparativo - Globo",
			"description": "Na conjunto de países do grupo G20, taxa anual atingiu 8,8% em maio, contra 11,7% no Brasil. Entre as grandes economias, apenas Turquia, Argentina e Rússia também possuem inflação acima de 10% ao ano.",
			"url": "https://g1.globo.com/economia/noticia/2022/07/05/inflacao-do-brasil-esta-entre-as-mais-altas-do-mundo-aponta-ocde-veja-comparativo.ghtml",
			"urlToImage": "https://s2.glbimg.com/c6BZPgFXO1_W6EJwH2GIPxs3Ag8=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/z/0/sDKKB2Q9ir0grLPc3fGA/fta20220618131.jpg",
			"publishedAt": "2022-07-05T15:28:12Z",
			"content": "Novo relatório divulgado pela OCDE (Organização para a Cooperação e Desenvolvimento Econômico) mostra que a inflação do Brasil segue entre as maiores do mundo e bem acima da média das grandes economi… [+2191 chars]",
			"id": 1,
			"likes": 2,
			"reports": 1
		}
	]

Em caso de sucesso, é retornado a seguinte resposta:

	{
		"source": {
			"name": "Globo"
		},
		"authorId": 1,
		"title": "Inflação do Brasil está entre as mais altas do mundo, aponta OCDE; veja comparativo - Globo",
		"description": "Na conjunto de países do grupo G20, taxa anual atingiu 8,8% em maio, contra 11,7% no Brasil. Entre as grandes economias, apenas Turquia, Argentina e Rússia também possuem inflação acima de 10% ao ano.",
		"url": "https://g1.globo.com/economia/noticia/2022/07/05/inflacao-do-brasil-esta-entre-as-mais-altas-do-mundo-aponta-ocde-veja-comparativo.ghtml",
		"urlToImage": "https://s2.glbimg.com/c6BZPgFXO1_W6EJwH2GIPxs3Ag8=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/z/0/sDKKB2Q9ir0grLPc3fGA/fta20220618131.jpg",
		"publishedAt": "2022-07-05T15:28:12Z",
		"content": "Novo relatório divulgado pela OCDE (Organização para a Cooperação e Desenvolvimento Econômico) mostra que a inflação do Brasil segue entre as maiores do mundo e bem acima da média das grandes economi… [+2191 chars]",
		"id": 1,
		"likes": 2,
		"reports": 1
	}

**Adicionar Avaliação em um artigo**

Nesse endpoint é possível adicionar um like em um artigo.

PATCH-> baseURL/articles/:id

	{
		"likes": 3 
	}

Em caso de sucesso, é retornado a seguinte resposta:

	{
		"source": {
			"name": "Globo"
		},
		"authorId": 1,
		"title": "Inflação do Brasil está entre as mais altas do mundo, aponta OCDE; veja comparativo - Globo",
		"description": "Na conjunto de países do grupo G20, taxa anual atingiu 8,8% em maio, contra 11,7% no Brasil. Entre as grandes economias, apenas Turquia, Argentina e Rússia também possuem inflação acima de 10% ao ano.",
		"url": "https://g1.globo.com/economia/noticia/2022/07/05/inflacao-do-brasil-esta-entre-as-mais-altas-do-mundo-aponta-ocde-veja-comparativo.ghtml",
		"urlToImage": "https://s2.glbimg.com/c6BZPgFXO1_W6EJwH2GIPxs3Ag8=/1200x/smart/filters:cover():strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/z/0/sDKKB2Q9ir0grLPc3fGA/fta20220618131.jpg",
		"publishedAt": "2022-07-05T15:28:12Z",
		"content": "Novo relatório divulgado pela OCDE (Organização para a Cooperação e Desenvolvimento Econômico) mostra que a inflação do Brasil segue entre as maiores do mundo e bem acima da média das grandes economi… [+2191 chars]",
		"id": 1,
		"likes": 3,
		"reports": 1
	}

**Editar um artigo**

Nesse endpoint é possível alterar um artigo.

PATCH-> baseURL/articles/:id

	{
		"source": {
			"name": "Correiobraziliense.com.br"
		},
		"authorId": 1,
		"title": "Motorista que invadiu parada na Rodoviária teria passado mal ao volante - Correio Braziliense",
		"description": "Mulher que estava no carona disse que o motorista teria perdido o controle do carro, após passar mal ao volante. O rapaz faz uso de remédios controlados",
		"url": "https://www.correiobraziliense.com.br/cidades-df/2022/07/5020364-motorista-que-invadiu-parada-na-rodoviaria-teria-passado-mal-ao-volante.html",
		"urlToImage": "https://midias.correiobraziliense.com.br/_midias/jpg/2022/07/06/675x450/1_whatsapp_image_2022_07_06_at_08_58_13-26004818.jpeg?20220706091046?20220706091046",
		"publishedAt": "2022-07-06T12:26:00Z",
		"content": "O homem que dirigia o carro que invadiu uma parada na plataforma superior da Rodoviária do Plano Piloto, sentido Asa Sul para a Asa Norte, próximo a Teatro Nacional, na manhã desta quarta-feira (6/7)… [+1248 chars]",
		"id":1,
		"likes": 50135,
		"reports": 0
	}

Em caso de sucesso, é retornado a seguinte resposta:

	{
		"source": {
			"name": "Correiobraziliense.com.br"
		},
		"authorId": 1,
		"title": "Motorista que invadiu parada na Rodoviária teria passado mal ao volante - Correio Braziliense",
		"description": "Mulher que estava no carona disse que o motorista teria perdido o controle do carro, após passar mal ao volante. O rapaz faz uso de remédios controlados",
		"url": "https://www.correiobraziliense.com.br/cidades-df/2022/07/5020364-motorista-que-invadiu-parada-na-rodoviaria-teria-passado-mal-ao-volante.html",
		"urlToImage": "https://midias.correiobraziliense.com.br/_midias/jpg/2022/07/06/675x450/1_whatsapp_image_2022_07_06_at_08_58_13-26004818.jpeg?20220706091046?20220706091046",
		"publishedAt": "2022-07-06T12:26:00Z",
		"content": "O homem que dirigia o carro que invadiu uma parada na plataforma superior da Rodoviária do Plano Piloto, sentido Asa Sul para a Asa Norte, próximo a Teatro Nacional, na manhã desta quarta-feira (6/7)… [+1248 chars]",
		"id": 1,
		"likes": 50135,
		"reports": 0
	}

**Editar Cadastro**

Nesse endpoint é possível alterar os dados do seu perfil.

PATCH-> baseURL/users/:id

	{
	"email": "churrosEditado@gmail.com",
	"password": "$2a$10$dYfRUT8oMVdJ0S5QpQWLHeUpyni8rSa8LwdKy6WyXo8zI/BhxEAaa",
	"name": "churros Editado",
	"avatar": "https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg",
	"type": "reader",
	"data": {
		"phone": "(xx) x xxxx-xxxx",
		"adress": {
			"cep": "12345678",
			"street": "limão",
			"district": "limoeira",
			"city": "carapicuiba",
			"state": "são paulo"
		}
	},
	"id": 2
	}

Em caso de sucesso, é retornado a seguinte resposta:

	{
	"email": "churrosEditado@gmail.com",
	"password": "$2a$10$8lgwtdUV2UPhzbj0iGpT/eCPZYBbUAcT/yr.3DnkXtMp/67ch6izy",
	"name": "churros Editado",
	"avatar": "https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg",
	"type": "reader",
	"data": {
		"phone": "(xx) x xxxx-xxxx",
		"adress": {
			"cep": "12345678",
			"street": "limão",
			"district": "limoeira",
			"city": "carapicuiba",
			"state": "são paulo"
		}
	},
	"id": 2
	}

SIM, ISSO É UMA IMAGEM DE UM MACACO FOFO.
![enter image description here](https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg)

humor e piadas, hahaha.