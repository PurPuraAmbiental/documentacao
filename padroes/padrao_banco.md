# Modelo de atributos e Tabelas

## QUERIES
- Palavras chave do SQL em maiúsculo
```sql
SELECT FROM WHERE CREATE ALTER DROP JOIN 
```

## Nome de tabelas:
- Capitalizadas
- CamelCase
- Em SINGULAR


## Nome de Atributos / colunas:

* Composição:
```xml
<prefixo_primario> + <prefixo_secundario> + <NomeTabela>
```

* Exemplos
-> Código de Usuário : n + Cd + Usuario -> nCdUsuario
-> Nome de Usuário : c + Nm + Usuario -> cNmUsuario


### Prefixo primário
- n -> Decimal, Primary e Foreign Key
- c -> Strings, Varchar, Char(1)
- i -> Inteiros
- d -> Datas

### Prefixo secundário
- Cd -> Código / Primary e Foreign Key
- Nr -> Número
- Nm -> Nome
- Sg -> Siglas
- Qnt -> Quantidade


#### EXEMPLOS:

```sql
CREATE TABLE Usuario (
    nCdUsuario    DECIMAL(10, 0) PRIMARY KEY
    cNmUsuario    VARCHAR(100)   NOT NULL
    nCdEmpresa    DECIMAL(10, 0) FOREIGN KEY REFERENCES ...
    iQntVisitas   INTEGER        DEFAULT 0
    cAtivo        CHAR(1)        CHECK (cAtivo IN ('0', '1'))
)
```

#### EXCEÇÕES

Quando não se aplicam os prefixos secundários, usa-se os primários.

* Composição:
```xml
<prefixo_primario> + nomeAtributo
```

- cSenha
- cCpf
- cCnpj
- cEmail
- cTelefone

### Atributos comuns
- cAtivo (CHAR(1)) sempre 0 ou 1

#### Primary e Foreign Key
```xml
nCd + <NomeTabela>
```


## Exemplos de SQL
```sql
-- Empresa
-- PostgreSQL

CREATE TABLE Empresa 
(
    nCdEmpresa        SERIAL        PRIMARY KEY
,   cNmEmpresa        VARCHAR(100)  NOT NULL
,   cSgEmpresa        VARCHAR(10)   NOT NULL UNIQUE
,   cCnpj             VARCHAR(14)   NOT NULL UNIQUE
,   cEmail            VARCHAR(100)  NOT NULL
,   cTelefone         VARCHAR(15)   NOT NULL
)

CREATE TABLE EmpresaEndereco 
(
    nCdEmpresaEndereco SERIAL       PRIMARY KEY
,   cNrEmpresaEndereco VARCHAR(10)  NOT NULL
,   cLogradouro        VARCHAR(100) NOT NULL
,   cComplemento       VARCHAR(50)
,   cBairro            VARCHAR(50)  NOT NULL
,   cCidade            VARCHAR(50)  NOT NULL
,   cEstado            VARCHAR(2)   NOT NULL
,   cCep               VARCHAR(8)   NOT NULL
    nCdEmpresa         INT          FOREIGN KEY (nCdEmpresa) REFERENCES Empresa(nCdEmpresa),
);

```
