# API da Kenzie Donation

A API da **KenzieDonation** tem como objetivo permitir cadastro e login de usuários, e que estes possam inserir itens à serem doados ou solicitados. Pode-se, também, editar o item criado ou apaga-lo. Todas as itens podem ser lidas sem autenticação, mas sua criação, edição ou apagar precisam de token de autorização.

## Rotas
baseUrl: https://kenzie-donation-api.onrender.com/

## Registro
Para fazer o registro:
**Endpoint:** POST https://kenzie-donation-api.onrender.com/register

*exemplo de body*
```
{
  "name": "Kenzinho",
  "email": "xanadu@mail.com",
  "password": "123456",
  "avatar": "",
  "phone": "11234567890",
  "state": "Goias"
}
```
*exemplo de resposta* 
```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjU1NiwiZXhwIjoxNjczMDA2MTU2LCJzdWIiOiIzIn0.qfT2uD4SOO4y59JWJd-exHfTBB9mhDGmJku5q91ZhyM",
	"user": {
		"email": "xanadu@mail.com",
		"name": "Kenzinho",
		"avatar": "",
		"phone": "11234567890",
		"state": "Goias",
		"id": 3
	}
}
```

## Login

Para fazer o login:
**Endpoint:** POST https://kenzie-donation-api.onrender.com/login

*exemplo de body*
```
{
	"email": "xanadu@mail.com",
	"password": "123456"
}
```
*exemplo de resposta* 
```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4",
	"user": {
		"email": "xanadu@mail.com",
		"name": "Kenzinho",
		"avatar": "",
		"phone": "11234567890",
		"state": "Goias",
		"id": 3
	}
}
```

*Tanto login como registro retornam token de validação*
## RESQUEST / SOLICITAÇÃO

### Criar solicitação

Para adicionar uma solicitação, o usuário precisa estar autenticado;
Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**Endpoint:** POST https://kenzie-donation-api.onrender.com/request

*exemplo de body*
```
{
	"title": "Preciso de um computador para trabalhar",
	"description": "Sou dev, mas estou desempregado",
	"img": "",
	"type": "solicitacao",
	"category": "Eletro",
	"userId": 3
}
```
*exemplo de resposta* 
201 - created
```
{
	"title": "Preciso de um computador para trabalhar",
	"description": "Sou dev, mas estou desempregado",
	"img": "",
	"type": "solicitacao",
	"category": "Eletro",
	"userId": 3,
	"id": 2
}
```

### Consultar solicitações (não precisa de autenticação - todos podem ver) 

Para consultar as solicitações:
**Endpoint:** GET https://kenzie-donation-api.onrender.com/request

*exemplo de body*
```
VAZIO
```

*exemplo de resposta* 

```
[
	{
		"title": "Preciso de um computador para trabalhar",
		"description": "Sou dev, mas estou desempregado",
		"img": "",
		"type": "solicitacao",
		"category": "Eletro",
		"userId": 3,
		"id": 2
	}
]
```

Para expandir o userId da resposta, e saber quem está por trás do id, insira "?_expand=user" ao fim do endpoint https://kenzie-donation-api.onrender.com/request?_expand=user

### Editar solicitação 

Para editar uma solicitação, o usuário precisa estar autenticado;
Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**__É obrigatório informar o userId no body da requisição__**

**Endpoint:** PATCH https://kenzie-donation-api.onrender.com/request/{idDoRequest}

*exemplo de body*
```
{
		"title": "Preciso de um computador para trabalhar",
		"description": "Estou empregado, mas sem computador",
		"img": "",
		"type": "solicitacao",
		"category": "Eletro",
		"userId": 3
}
```
*exemplo de resposta* 
200 - OK
```
{
	"title": "Preciso de um computador para trabalhar",
	"description": "Estou empregado, mas sem computador",
	"img": "",
	"type": "solicitacao",
	"category": "Eletro",
	"userId": 3,
	"id": 2
}
```

### Deletar uma solicitação 

Para deletar uma solicitação o usuário precisa estar autenticado;

Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**Endpoint:** DELETE https://kenzie-donation-api.onrender.com/request/{idDoRequest}

*exemplo de body*
```
VAZIO
```
*exemplo de resposta* 
200 - OK
```
{}
```

## Posts

### Criar um Post 

Para adicionar um Post, o usuário precisa estar autenticado;

Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**Endpoint:** POST https://kenzie-donation-api.onrender.com/donation

*exemplo de body*
```
{
	"title": "Estou doando um computador 4gb de ram",
	"description": "está funcional",
	"img": "",
	"type": "donation",
	"category": "Eletro",
	"userId": 3
}
```
*exemplo de resposta* 
201 - created
```
{
	"title": "Estou doando um computador 4gb de ram",
	"description": "está funcional",
	"img": "",
	"type": "donation",
	"category": "Eletro",
	"userId": 3,
	"id": 2
}
```

### Consultar Posts (não precisa de autenticação - todos podem ver) 

Para consultar os post:
**Endpoint:** GET https://kenzie-donation-api.onrender.com/donation

*exemplo de body*
```
VAZIO
```

*exemplo de resposta* 

```
[
	{
		"title": "Estou doando um computador 4gb de ram",
	  "description": "está funcional",
		"img": "",
		"type": "donation",
		"category": "Eletro",
		"userId": 3,
		"id": 2
	}
]
```

### Editar Post 

Para editar um post, o usuário precisa estar autenticado;
Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**__É obrigatório informar o userId no body da requisição__**

**Endpoint:** PATCH https://kenzie-donation-api.onrender.com/donation/{idDoPost}

*exemplo de body*
```
{
		"title": "Estou doando um computador 4gb de ram",
	  "description": "está funcional",
		"img": "",
		"type": "donation",
		"category": "Eletro",
		"userId": 3
}
```
*exemplo de resposta* 
200 - OK
```
{
	"title": "Estou doando um computador 4gb de ram",
	"description": "está funcional",
	"img": "",
	"type": "donation",
	"category": "Eletro",
	"userId": 3,
	"id": 2
}
```

### Deletar um post 

Para deletar um post o usuário precisa estar autenticado;

Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**Endpoint:** DELETE https://kenzie-donation-api.onrender.com/donation/{idDoPost}

*exemplo de body*
```
VAZIO
```
*exemplo de resposta* 
200 - OK
```
{}
```

## Usuário

### Ver usuário

**__ Necessário estar logado e autenticado __**

**Endpoint:** GET https://kenzie-donation-api.onrender.com/users/{idDoUser}?_embed=objects

Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

*exemplo de body*
```
VAZIO
```

*exemplo de resposta* 
200 - OK
```
{
	"email": "xanadu@mail.com",
	"password": "$2a$10$oju9246LRG.lXOm2B/iCiOLzpNpZCpd6HW3Ne3BJO9n6QwA6ndNGm",
	"name": "Kenzinho",
	"avatar": "",
	"phone": "11234567890",
	"state": "Goias",
	"id": 3,
	"objects": []
}
```

*Exemplo de resposta ao tentar acessar um usuário que não corresponde ao logado*

tentativa com id = 2 
(https://kenzie-donation-api.onrender.com/users/2?_embed=objects)
```
{
"Private resource access: entity must have a reference to the owner id"
}
```

### Editar usuário

Na edição de um usuário já criado, **só é permitido alterar os campos *"name", "avatar", "phone", "state"***

**É necessário indicar o id do usuário no endpoint e estar autenticado**

**Endpoint:** PATCH https://kenzie-donation-api.onrender.com/users/{idDoUser}

Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

*exemplo de body*
```
{
	"name": "José da Silva", //alterando o nome do usuário
	"avatar": "",
	"phone": "11234567890",
	"state": "Goias"
}
```

*exemplo de resposta* 
200 - OK
```
{
	"email": "xanadu@mail.com",
	"password": "$2a$10$oju9246LRG.lXOm2B/iCiOLzpNpZCpd6HW3Ne3BJO9n6QwA6ndNGm",
	"name": "José da Silva",
	"avatar": "",
	"phone": "11234567890",
	"state": "Goias",
	"id": 3
}
```

## Operações finalizadas
Para donations, use o endpoint com final "getdonation"; para requests, use o endpoint "getrequest" - body e passagem de token são iguais.

### Pegar doação 

Para adicionar um Post, o usuário precisa estar autenticado;

Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**Endpoint:** POST https://kenzie-donation-api.onrender.com/getdonation

*exemplo de body*
```
{
	"title": "Computador desktop ",
     	"description": "Funciona perfeitamente",
   	"category": "eletronico",
      	"type": "donation",
      	"image": "https://cdn.desapega.net/pictures/62/b262cb70de426a7fcef4fc9009d84c0fece79595491a3649741ae0e82d219e.jpg",
      	"userId": 4,
      	"id": 1
}
```
*exemplo de resposta* 
200 - ok
```
{
	"title": "Computador desktop ",
     	"description": "Funciona perfeitamente",
   	"category": "eletronico",
      	"type": "donation",
      	"image": "https://cdn.desapega.net/pictures/62/b262cb70de426a7fcef4fc9009d84c0fece79595491a3649741ae0e82d219e.jpg",
      	"userId": 4,
      	"id": 1
}
```

### Ver suas doações aceitas

Authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InhhbmFkdUBtYWlsLmNvbSIsImlhdCI6MTY3MzAwMjcwMiwiZXhwIjoxNjczMDA2MzAyLCJzdWIiOiIzIn0.iF_gIaDiUbtMihHTZBc6kdduhUz2eP4hKPdI2hMDId4'

**Endpoint:** GET https://kenzie-donation-api.onrender.com/getdonation

*exemplo de body*
```
VAZIO
```
*exemplo de resposta* 
200 - OK
```
[
	{
		"title": "Computador desktop ",
		"description": "Funciona perfeitamente",
		"category": "eletronico",
		"type": "donation",
		"image": "https://cdn.desapega.net/pictures/62/b262cb70de426a7fcef4fc9009d84c0fece79595491a3649741ae0e82d219e.jpg",
		"userId": 4,
		"id": 1
	},
	{
		"title": "Caminhãozinho de carga",
		"description": "Em bom estado ",
		"category": "Brinquedos",
		"type": "donation",
		"image": "https://i.ytimg.com/vi/7_BeDVCMEKY/mqdefault.jpg",
		"userId": 4,
		"id": 26
	}
]
```
