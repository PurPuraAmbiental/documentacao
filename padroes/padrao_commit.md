# Padrões de commit
Esse documento tem como objetivo unificar o padrão de commit do projeto de maneira que seja fácil de identificar o que foi feito em cada commit.

## O que são bons commits?

Um bom commit tem que ter um **prefixo** e uma **mensagem**.
- O **prefixo** serve para identificar o tipo de commit.
- A **mensagem** serve para explicar o que foi feito no commit.

### Exemplos de bons commits

1. `(feat)` Adicionar um novo endpoint
2. `(bugfix)` Corrigir um bug
3. `(refactor)` Mudou nome de variável
4. `(chore)` Adicionou postgres ao pom.xml
5. `(test)` Adicionou um novo teste unitário
6. `(release)` Criou uma nova versão do projeto
7. `(merge)` Merge com outra branch
8. `(ci)` Modificando arquivo ci.yml
9. `(style)` Mudando formatação de código, espaçamentos

### Boas mensagens
Os exemplos acima demonstram operações únicas, atômicas e bem descritas, evite mensagens longas ou muito genéricas de commits


## Prefixos
Os prefixos podem ser usados em qualquer commit do projeto, mas eles podem ser usados de maneira diferente dependendo do commit que estiver sendo feito.


* ✨ **(feat)**: indica o desenvolvimento de uma nova feature ao projeto. 
    - Exemplo: Acréscimo de um serviço, funcionalidade, endpoint, etc.

* 🔧 **(refactor)**: usado quando houver uma refatoração de código que não tenha qualquer tipo de impacto na lógica/regras de negócio do sistema. 
    - Exemplos: Mudanças de código após um code review, nomes de arquivos, classes, variáveis etc.

* 💃 **(style)**: Mudança de formatação de código fonte, espaços entre funções, classes etc.

* 🐛 **(bugfix)**: utilizado quando há correção de erros que estão gerando bugs no sistema.
    - Exemplo: Aplicar tratativa para uma função que não está tendo o comportamento esperado e retornando erro.

* 🚫 **(remove)**: indica a remoção de arquivos, códigos, features etc do projeto.
    - Exemplo: Remover um endpoint, remover uma classe, tabela, remover um arquivo, etc.

* 🧹 **(chore)**: indica mudanças no projeto que não afetem o sistema ou arquivos de testes. São mudanças de desenvolvimento.
    - Exemplo: Mudar regras do de linters, pom.xml, adicionar prettier, adicionar mais extensões de arquivos ao .gitignore e Dockerfile

* 📝 **(doc)**: usado quando há mudanças na documentação do projeto.
    - Exemplo: adicionar informações na documentação da API (Swagger), mudar o README, etc.
    - Ou também quando se muda comentários no código

* ↩️ **(revert)**: indica a reverão de um commit anterior.

* 🎉 **(merge)**: indica a mescla de duas ou mais branches.
    - No entanto também é válida a mensagem de merge automática do git.

* 🧪 **(test)**: indica o desenvolvimento/alteração de um teste unitário.

* 🚀 **(release)**: indica a criação de uma nova versão do projeto.

* 👩‍💻 **(ci)**: indica commits relacionados ao GitHub Actions, modificações nas pipelines ci.yml


