# Fluxos das APIs 🪼
Esse documento tem como objetivo documentar as requisições os quais o Mobile deverá de seguir para implementar os fluxos de usuário.

## Fluxo: Cadastrar um resíduo 🪴
### Passo 1.
Objetivo: Pegar a empresa:

* `[ApiMongo]` Pegar empresa 
```js
GET /empresa/{cnpj}
```


### Passo 2.
Objetivo: Consultar os endereços e chaves pix já cadastradas para mostrar as opções aos usuários.

* `[ApiMongo]` Pegar endereços
```js
GET /empresa/{cnpj}/endereco/all
```
* `[ApiMongo]` Pegar chaves pix
```js
GET /empresa/{cnpj}/pix/all
```

### Passo 3
Objetivo: Guardar os endereços e chaves pix na API.

#### Passo 3.1

Objetivo: Guardar o endereço na API
> Condição: Se for um **endereço novo**


* `[ApiMongo]` Mandar o endereço
```js
POST /empresa/{cnpj}/endereco
{
    "nome": ...,
    "cep": ...,
    "numero": ...,
    "complemento": ...
}
```

Por agora, guardar o ID do novo endereço em alguma variável.

#### Passo 3.2
Objetivo: Guardar a chave pix na API
> Condição: Se for uma **chave pix nova**


* `[ApiMongo]` Mandar a chave pix
```js
POST /empresa/{cnpj}/pix
{
    "nome": ...,
    "chave": ...
}
```


Por agora, guardar o ID da nova chave em alguma variável.

### Passo 4
Objetivo: De fato criar o resíduo, contendo chave pix e endereço atrelados.

* `[ApiMongo]` Criar o resíduo
```js
POST /empresa/{cnpj}/residuo
{
    "nome": ...,
    "peso": ...,
    "estoque":...,
    "tipoUnidade":...,
    "urlImagem": ...,
    "idEndereco": ... // <--- Use o ID do endereço aqui!
    "idChavePix": ... // <--- Use o ID da chave pix aqui!
}
```


## Fluxo: Adicionar um resíduo ao carrinho. 🛒

### Passo 1.
Objetivo: Pegar a empresa:

* `[ApiMongo]` Pegar a empresa por CNPJ.
```js
GET /empresa/{cnpj}
```

### Passo 2.
Objetivo: Pegar os resíduos da página principal, excluindo os resíduos da própria empresa (não faz sentido ela comprar dela mesma)

* `[ApiMongo]` Pegar os resíduos que ela pode comprar
```
GET /empresa/{cnpj}/residuos/viewmain?limit=10       // <--- Endpoint diferente!
```

* Retornará uma **lista**:
```js
[
    {
        "id": "...",
        "urlFoto": "...",
        "peso": ...,
        "estoque": ...,
        "tipoUnidade": "...",
        // ...
    },
    ...
]
```

**OBS:** Guardar o ID do resíduo.

**OBS Mobile:** No adapter, para cada resíduo usando um `for`; pegar seu `id`; criar um listener específico que redireciona para a tela de detalhes; passar um `Bundle` para a tela de detalhes.

### Passo 3.
Objetivo: Após o usuário clicar no card do resíduo, mostrar a tela de detalhes.

### Passo 3.1
Objetivo: Pegar informações adicionais do resíduo

* `[ApiMongo]` Pegar os detalhes do resíduo por ID
```js
GET /empresa/{cnpj}/residuo/{residuoId}/details
```
* Retorará:
```js
{ 
   "endereco": { "cep": ..., numero: ..., complemento: ... },
   "chavePix": { "nome": ..., chave: "..." }
}
```


**OBS:** Por hora, guardar o `cep` do `endereco` em uma variável

### Passo 3.2
Objetivo: Pegar detalhes mais específicos do local do CD pelo CEP.

* `[ApiMicro]` Pegar os detalhes do CEP

```js
GET /cep/{cep}
```
* Retornará:
```js
{
    "cidade": "São Paulo",
    "logradouro": "Rua Maciel Barbosa",
    "uf": "SP", 
    ...
}
```
