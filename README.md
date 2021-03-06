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
    "email": "demonstrandoApi@gmail.com",
	"name": "demonstrandoApi",
	"password":"12345Teste@"
	}

Em caso de sucesso na criação de usuário, é retornado a seguinte resposta:

    {
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRlbW9uc3RyYW5kb0FwaUBnbWFpbC5jb20iLCJpYXQiOjE2NTc2MzQ5NzMsImV4cCI6MTY1NzYzODU3Mywic3ViIjoiNiJ9.27j2x51GsDKmRt5pC-Di6B8UTlZkUYlAdj7739tmkXE",
	"user": {
		"email": "demonstrandoApi@gmail.com",
		"name": "demonstrandoApi",
		"id": 6
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
    	"email": "email@gmail.com",
    	"password": "@aB123456"
    }

Em caso de sucesso no login usuário, é retornado a seguinte resposta:

    {
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRlbW9uc3RyYW5kb0FwaUBnbWFpbC5jb20iLCJpYXQiOjE2NTc2MzUwMjAsImV4cCI6MTY1NzYzODYyMCwic3ViIjoiNiJ9.nnUlNC0TDJ--BpB6uMMLnTElh5QE2jpXHvMe6MzYw4A",
	"user": {
		"email": "demonstrandoApi@gmail.com",
		"name": "demonstrandoApi",
		"id": 6
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
			"name": "Editalconcursosbrasil.com.br",
			"category": "tecnologia",
			"authorId": 1,
			"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
			"author": "juninho",
			"title": "Dá para mudar a cor do WhatsApp? Veja se truques realmente funcionam - Edital Concursos Brasil",
			"description": "Entenda se é possível ou permitido mudar a cor do WhatsApp no seu celular e quais são as possibilidades para que isso aconteça. Evite se expor a algum risco desnecessário",
			"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
			"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
			"content": "Você gostaria de poder mudar a cor do WhatsApp de um jeito prático e bem simples? Saiba que isso pode ser feito sem colocar suas informações ou o próprio celular em algum tipo de risco. Vamos entender mais sobre o assunto a partir de agora. Veja também: Alô timidez! Nova função no WhatsApp vai alegrar pessoas discretas. Cuidado com apps para mudar a cor do WhatsApp. Muitas pessoas gostam de deixar o aparelho celular e seus aplicativos com um toque a mais de personalidade. Isso quer dizer, que esses usuários buscam ferramentas para mudar a cor, a fonte e o aspecto dos programas instalados no dispositivo. Para conseguir esses efeitos e mudar a cor do WhatsApp, alguns usuários acabam instalando programas suspeitos em seus dispositivos. No entanto, essa prática pode colocar seus dados em risco e você pode acabar se dando mal.",
			"id": 1,
			"likes": 3,
			"reports": 0
		}
    ]

**Listar artigos com paginação**

Nesse endpoint é possível listar todos artigos, com o parametro "_page" criamos uma paginação e com o "_limit" definimos quantos artigos estão dispostos por pagina e com _embed=comments mostramos os comentarios.

GET-> baseURL/articles?_page=1&_limit=1&_embed=comments 

    [
		{
			"name": "Editalconcursosbrasil.com.br",
			"category": "tecnologia",
			"authorId": 1,
			"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
			"author": "juninho",
			"title": "Dá para mudar a cor do WhatsApp? Veja se truques realmente funcionam - Edital Concursos Brasil",
			"description": "Entenda se é possível ou permitido mudar a cor do WhatsApp no seu celular e quais são as possibilidades para que isso aconteça. Evite se expor a algum risco desnecessário",
			"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
			"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
			"content": "Você gostaria de poder mudar a cor do WhatsApp de um jeito prático e bem simples? Saiba que isso pode ser feito sem colocar suas informações ou o próprio celular em algum tipo de risco. Vamos entender mais sobre o assunto a partir de agora......",
			"id": 1,
			"likes": 3,
			"reports": 0,
			"comments": [
				{
					"id": 1,
					"ownerId": 2,
					"articleId": 1,
					"content": "Nossa não sabia desses perigos dos aplicativos de trocar a cor do Zap",
					"userImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
					"username": "Juninho"
				},
				{
					"ownerId": 5,
					"articleId": 1,
					"content": "Que mentira, baixei e funcionou!",
					"id": 4
				}
			]
		}
	]

**Listar artigos Reportados**

Nesse endpoint é possível listar todos os artigos que foram reportados por usuarios.

GET-> baseURL/reported

	[
		{
		"name": "Editalconcursosbrasil.com.br",
		"category": "tecnologia",
		"authorId": 1,
		"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
		"author": "juninho",
		"title": "Dá para mudar a cor do WhatsApp? Veja se truques realmente funcionam - Edital Concursos Brasil",
		"description": "Entenda se é possível ou permitido mudar a cor do WhatsApp no seu celular e quais são as possibilidades para que isso aconteça. Evite se expor a algum risco desnecessário",
		"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
		"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
		"content": "Você gostaria de poder mudar a cor do WhatsApp de um jeito prático e bem simples? Saiba que isso pode ser feito sem colocar suas informações ou o próprio celular em algum tipo de risco. Vamos entender mais sobre o assunto a partir de agora....",
		"id": 1,
		"likes": 3,
		"reports": 0,
		}
	]
    
## Rotas precisam de autenticação

**Criar novo artigo**

POST -> baseURL/articles

Os dados solicitados pela API são:

    {
		"name": "demonstração",
		"category": "demonstração",
		"authorId": 1,
		"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
		"author": "demonstração",
		"title": "demonstração",
		"description": "demonstração",
		"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
		"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
		"content": "demonstração....",
		"id":4,	
		"likes": 3,
		"reports": 0
	}

source -> origem da noticia 
authorId -> id do criador

Em caso de sucesso, é retornado a seguinte resposta:

    {
	"name": "demonstração",
	"category": "demonstração",
	"authorId": 1,
	"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
	"author": "demonstração",
	"title": "demonstração",
	"description": "demonstração",
	"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
	"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
	"content": "demonstração....",
	"id": 4,
	"likes": 3,
	"reports": 0
	}

**Criar comentario**

POST -> baseURL/comments

Os dados solicitados pela API são:

    {
		"ownerId": 2,
		"articleId": 1,
		"content": "teste",
		"userImg":"https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
		"username": "teste"
	}

ownerId -> id de quem fez o comentario 
articleId -> id do artigo comentado

Em caso de sucesso, é retornado a seguinte resposta:

    {
	"ownerId": 2,
	"articleId": 1,
	"content": "teste",
	"userImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
	"username": "teste",
	"id": 5
	}

**deletar artigo**

DELETE -> baseURL/articles/:id

Em caso de sucesso, é retornado a seguinte resposta:

    {}

**deletar comentario**

DELETE -> baseURL/comments/:id

Em caso de sucesso, é retornado a seguinte resposta:

    {}

**reportar Artigo**

Nesse endpoint é possível adicionar uma denuncia em um artigo.

PATCH-> baseURL/articles/:id

	{
		"reports": 1
	}

Em caso de sucesso, é retornado a seguinte resposta:

	{
	"name": "Editalconcursosbrasil.com.br",
	"category": "tecnologia",
	"authorId": 1,
	"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
	"author": "juninho",
	"title": "Dá para mudar a cor do WhatsApp? Veja se truques realmente funcionam - Edital Concursos Brasil",
	"description": "Entenda se é possível ou permitido mudar a cor do WhatsApp no seu celular e quais são as possibilidades para que isso aconteça. Evite se expor a algum risco desnecessário",
	"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
	"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
	"content": "Você gostaria de poder mudar a cor do WhatsApp de um jeito prático e bem simples? Saiba que isso pode ser feito sem colocar suas informações ou o próprio celular em algum tipo de risco. Vamos entender mais sobre o assunto a partir de agora. Veja também: Alô timidez! Nova função no WhatsApp vai alegrar pessoas discretas. Cuidado com apps para mudar a cor do WhatsApp. Muitas pessoas gostam de deixar o aparelho celular e seus aplicativos com um toque a mais de personalidade. Isso quer dizer, que esses usuários buscam ferramentas para mudar a cor, a fonte e o aspecto dos programas instalados no dispositivo. Para conseguir esses efeitos e mudar a cor do WhatsApp, alguns usuários acabam instalando programas suspeitos em seus dispositivos. No entanto, essa prática pode colocar seus dados em risco e você pode acabar se dando mal.",
	"id": 1,
	"likes": 3,
	"reports": 1
	}

**Adicionar artigo a lista de Reportados**

Nesse endpoint é possível adicionar uma artigo ja denunciado a lista de reportados para futura analise.

POST-> baseURL/reported

	{
		"name": "Editalconcursosbrasil.com.br",
		"category": "tecnologia",
		"authorId": 1,
		"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
		"author": "juninho",
		"title": "Dá para mudar a cor do WhatsApp? Veja se truques realmente funcionam - Edital Concursos Brasil",
		"description": "Entenda se é possível ou permitido mudar a cor do WhatsApp no seu celular e quais são as possibilidades para que isso aconteça. Evite se expor a algum risco desnecessário",
		"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
		"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
		"content": "Você gostaria de poder mudar a cor do WhatsApp de um jeito prático e bem simples? Saiba que isso pode ser feito sem colocar suas informações ou o próprio celular em algum tipo de risco. Vamos entender mais sobre o assunto a partir de agora. Veja também: Alô timidez! Nova função no WhatsApp vai alegrar pessoas discretas. Cuidado com apps para mudar a cor do WhatsApp. Muitas pessoas gostam de deixar o aparelho celular e seus aplicativos com um toque a mais de personalidade. Isso quer dizer, que esses usuários buscam ferramentas para mudar a cor, a fonte e o aspecto dos programas instalados no dispositivo. Para conseguir esses efeitos e mudar a cor do WhatsApp, alguns usuários acabam instalando programas suspeitos em seus dispositivos. No entanto, essa prática pode colocar seus dados em risco e você pode acabar se dando mal.",
		"id": 1,
		"likes": 3,
		"reports": 1
	}

Em caso de sucesso, é retornado a seguinte resposta:

	{
	"name": "Editalconcursosbrasil.com.br",
	"category": "tecnologia",
	"authorId": 1,
	"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
	"author": "juninho",
	"title": "Dá para mudar a cor do WhatsApp? Veja se truques realmente funcionam - Edital Concursos Brasil",
	"description": "Entenda se é possível ou permitido mudar a cor do WhatsApp no seu celular e quais são as possibilidades para que isso aconteça. Evite se expor a algum risco desnecessário",
	"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
	"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
	"content": "Você gostaria de poder mudar a cor do WhatsApp de um jeito prático e bem simples? Saiba que isso pode ser feito sem colocar suas informações ou o próprio celular em algum tipo de risco. Vamos entender mais sobre o assunto a partir de agora. Veja também: Alô timidez! Nova função no WhatsApp vai alegrar pessoas discretas. Cuidado com apps para mudar a cor do WhatsApp. Muitas pessoas gostam de deixar o aparelho celular e seus aplicativos com um toque a mais de personalidade. Isso quer dizer, que esses usuários buscam ferramentas para mudar a cor, a fonte e o aspecto dos programas instalados no dispositivo. Para conseguir esses efeitos e mudar a cor do WhatsApp, alguns usuários acabam instalando programas suspeitos em seus dispositivos. No entanto, essa prática pode colocar seus dados em risco e você pode acabar se dando mal.",
	"id": 1,
	"likes": 3,
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
	"name": "demonstração EDITADA",
	"category": "demonstração",
	"authorId": 1,
	"authorImg": "https://s2.glbimg.com/jsaPuF7nO23vRxQkuJ_V3WgouKA=/e.glbimg.com/og/ed/f/original/2014/06/10/461777879.jpg",
	"author": "demonstração",
	"title": "demonstração",
	"description": "demonstração",
	"url": "https://editalconcursosbrasil.com.br/noticias/2022/07/da-para-mudar-a-cor-do-whatsapp-descubra-se-truques-realmente-funcionam/",
	"urlToImage": "https://editalconcursosbrasil.com.br/wp-content/uploads/2022/04/WhatsApp-3-1.jpg",
	"content": "demonstração....",
	"id":4,	
	"likes": 0,
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
		"email": "testeEDIT2@gmail.com",
		"password": "$2a$10$qDTTB1IYTWMmt4SkLmAc1.PtRWNoWbWalTNbvPXWhKcwhxvBgCVxi",
		"name": "TESTEEDIT2",
		"avatar": "https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg",
		"type": "content creator",
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
		"id": 6
	}

Em caso de sucesso, é retornado a seguinte resposta:

	{
	"email": "testeEDIT2@gmail.com",
	"password": "$2a$10$/fhAEutLe/NQKB10ioKopOUe9AzhZg.tAgY.fwzsckEWntCtmimKi",
	"name": "TESTEEDIT2",
	"avatar": "https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg",
	"type": "content creator",
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
	"id": 6
	}

**Visualizar Perfis**

Nesse endpoint é possível visualizar os perfis criados.

GET-> baseURL/users

	[
	{
		"email": "contentCreator@gmail.com",
		"password": "$2a$10$dYfRUT8oMVdJ0S5QpQWLHeUpyni8rSa8LwdKy6WyXo8zI/BhxEAaa",
		"name": "contentCreator",
		"avatar": "https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg",
		"type": "content creator",
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
		"id": 1
	},
	{
		"email": "company@gmail.com",
		"password": "$2a$10$dYfRUT8oMVdJ0S5QpQWLHeUpyni8rSa8LwdKy6WyXo8zI/BhxEAaa",
		"name": "company",
		"avatar": "https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg",
		"type": "company",
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
	},
	{
		"email": "reader@gmail.com",
		"password": "$2a$10$dYfRUT8oMVdJ0S5QpQWLHeUpyni8rSa8LwdKy6WyXo8zI/BhxEAaa",
		"name": "reader",
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
		"id": 3
	},
	{
		"email": "testeEDIT3@gmail.com",
		"password": "$2a$10$aQIJdMcDZYMlWCL7gbi/keiyg37MJCfzzuWmpx8e5PgEPjJO353sW",
		"name": "TESTEEDIT3",
		"avatar": "https://cdn.discordapp.com/attachments/886307601548214355/993915130905636925/foto_de_macaco_para_perfil.jpg",
		"type": "content creator",
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
		"id": 4
	},
	{
		"email": "rogerinho1@teste.com",
		"password": "$2a$10$HBRXcUTOV/12WD9/22fXOeYY3L1Lr4KrdkamV4.tUd38V8FEKs4sy",
		"name": "Rogerinho",
		"confirmPassword": "@Qq123456",
		"type": "reader",
		"id": 5
	},
	{
		"email": "demonstrandoApi@gmail.com",
		"password": "$2a$10$Uz99cPwKZBQRhcW9P9ZFVuLQTjIOr05UQsyxJquH7EbbE10AKiwSS",
		"name": "demonstrandoApi",
		"id": 6
	}
	]