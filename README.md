# CadastroDeAlunos
Criando um CRUD com Java Spring Booot

# Historia de usuario
Como Usuario do Sistema,

Eu quero ser capaz de adicionar, buscar, atualizar e remover cadastros de alunos, instituições de ensinos superiores e disciplinas de cada instituição no sistema. 


# Arquitetura do sistema

O sistema vai ser feito em `Java` com o Framework `Spring Boot`, a principio não terá UI para o usuario(Front-end), o sistema vai receber requisições `REST` no formato `JSON` para ser uma aplicação `Java para internet` ~que é `Javascrpit`~.

Utilize o https://start.spring.io para criar a estrutura da API em `Maven`, em `Group: com.api` e `Artifact: cadastroAluno` com as seguintes dependencias:
 - Spring Boot DevTools (Para recarregar as mudancas no codigo sem derrubar o projeto)
 - Spring Web Starter (Para incluir funções REst)
 - H2 Base (Bando de Dados em Memoria)

O sistema terá 3 Entidades com as seguintes nomeclaturas:
  - `AlunoEntidade.java`
  - `InstituiçãoEntidade.java`
  - `DisciplinasEntidade.java`
  
Atributos necessários da Classe `AlunoEntidade.java` junto com seus respectivos `getters` e `setters`:

        | idDoAluno (int)
        | nomeDoAluno (String)
        | telefoneDoAluno (long)
        | cpfDoAluno  (String)
        | emailDoAluno (String)
        | idDaInstituição (int)
        | idDaDisciplina (int)
  
Atributos necessários da Classe `InstituiçãoEntidade.java` junto com seus respectivos `getters` e `setters`:

        | idDaInstuição (int)
        | nomeDaInstuição (String)
        | telefoneDaInstituição (long)
        | cnpjDaInstuição (String)
        | emailDaInstuição (String)
        | qtdDeDisciplinasOfertadas (int)
        | notaDoMEC (int)
        | idDaDisciplina (int)
        
Atributos necessários da Classe `DisciplinasEntidade.java` junto com seus respectivos `getters` e `setters`:

        | idDaDisciplina (int)
        | nomeDaDisciplina (String)
        | primeiraNotaDoAluno (long)
        | segundaNotaDoAluno (long)
        | terceiraNotaDoAluno (long)
        | idDoAluno (int)
        
- OBS: Usar as Anotações necessárias, ex: @Id.


O sistema terá 3 Controllers com as seguintes nomeclaturas e `endpoints`:
  - `AlunoController.java`
  - `InstituçãoController.java`
  - `DisciplinasController.java`

Vamos comecar apenas com `AlunoController.java`:

```
 Requisição = (GET),
 Endpoint = /api/buscarAlunos,
 Metodo = buscarAlunos()
 ```
 
 ```
 Requisição = (GET),
 Endpoint = /api/buscarAluno/{idAluno},
 Metodo = buscarAlunoPorId(int idAluno)
 ```
 
 ```
 Requisição = (POST),
 Endpoint = /api/cadastrarAluno,
 Metodo = cadastrarAlunos(AlunoEntidade aluno),
 Body =
 {
    "nomeDoAluno": "qualquer nome",
    "telefoneDoAluno": "qualquer numero",
    "cpfDoAluno": "um cpf valido",
    "emailDoAluno": "email valido",
    "idDaInstituição": 0,
    "idDaDisciplina": 0 
 }
 ````
 
 ```
 Requisição = (PUT),
 Endpoint = /api/atualizarAluno/{idAluno},
 Metodo = atualizarAluno(int idAluno),
 Body =
 {
    "nomeDoAluno": "novo qualquer nome",
    "telefoneDoAluno": "novo qualquer numero",
    "cpfDoAluno": "novo um cpf valido",
    "emailDoAluno": "novo email valido",
    "idDaInstituição": 0,
    "idDaDisciplina": 0 
 }
``` 

 ```
 Requisição = (DELETE)
 Endpoint = /api/deletarAluno/{idAluno}
 Metodo = deletarAluno(int idAluno)
 ```
 
  Resposta Esperadas do sistema:
  
 ```
 GET
 Code = 200 (OK)
 ```
 
 ```
 POST
 Code = 201 (CREATED)
 Response = 
 {
    "nomeDoAluno": "Leozin1010",
    "telefoneDoAluno": "31956474733",
    "cpfDoAluno": "121.323.454-80",
    "emailDoAluno": "leozin1010@gmail.com",
    "idDaInstituição": 0,
    "idDaDisciplina": 0 
 }
 ```
 
 ```
 PUT
 Code = 201 (CREATED)
  Response = 
 {
    "nomeDoAluno": "Leozin1010Atualizado",
    "telefoneDoAluno": "31956474733",
    "cpfDoAluno": "121.323.454-80",
    "emailDoAluno": "leozin1010@gmail.com",
    "idDaInstituição": 0,
    "idDaDisciplina": 0 
 }
 ```
 
 ```
 DELETE
 Code = 200 (OK)
 
 ```
 
Para fazermos a comunicação REst com a API que iremos criar, utilizaremos o software Postman:
https://www.getpostman.com

Ele irá simular o nosso Front-end enviando os `JSONs` de nossas requisições acima.
 
 
O sistema terá 3 interfaces Services com as seguintes nomeclaturas:
  - `AlunoService.java`
  - `InstituçãoService.java`
  - `DisciplinasService.java`

Todas elas extendendo a interface `JPARepository` para fazer o `Autowired` nas Classes `Controllers`.

