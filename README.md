# Guia de Bolso: C# 14 & .NET 10
**Referência Rápida para Desenvolvimento Moderno**

**Autor:** [Seu Nome/Usuário]  
**Versão:** 1.5 (Atualizado com Dapper e Blazor)  
**Repositório:** [Link do seu GitHub]

---

## 📑 Índice
1. [Comandos Essenciais do CLI](#1-comandos-essenciais-do-cli)
2. [Sintaxe C# - Tipos e Declarações](#2-sintaxe-c---tipos-e-declarações)
3. [Sintaxe C# - Controle de Fluxo](#3-sintaxe-c---controle-de-fluxo)
4. [Sintaxe C# - Modificadores e OOP](#4-sintaxe-c---modificadores-e-oop)
5. [Coleções e LINQ](#5-coleções-e-linq)
6. [Entity Framework Core CLI](#6-entity-framework-core-cli-dotnet-ef)
7. [FluentValidation (Validação de Modelos)](#7-fluentvalidation-validação-de-modelos)
8. [FluentMigrator (Migrations em Código)](#8-fluentmigrator-migrations-em-código)
9. [Blazor & Sintaxe Razor](#9-blazor--sintaxe-razor)
10. [Dapper (Micro-ORM de Performance)](#10-dapper-micro-orm-de-performance)

<div style="page-break-after: always;"></div>

---

## 1. Comandos Essenciais do CLI (.NET 10)

O `dotnet` CLI é a base do ecossistema. Aqui estão os comandos para o dia a dia.

| Comando | Descrição |
| :--- | :--- |
| `dotnet new <template>` | Cria um projeto. Templates comuns: `console`, `webapi`, `blazor`. |
| `dotnet new sln` | Cria um arquivo de Solução em branco (`.sln`). |
| `dotnet sln add <proj>` | Adiciona um projeto existente à solução. |
| `dotnet build` | Compila o código e suas dependências. |
| `dotnet run` | Compila (se necessário) e executa a aplicação. |
| `dotnet watch` | Executa a aplicação e aplica *Hot Reload* ao salvar arquivos. |
| `dotnet test` | Executa os projetos de teste da solução. |
| `dotnet clean` | Limpa a saída das compilações anteriores (pastas `bin` e `obj`). |
| `dotnet restore` | Restaura as dependências e ferramentas do NuGet. |
| `dotnet add package <pkg>` | Instala um pacote NuGet no projeto atual. |
| `dotnet remove package <pkg>` | Remove um pacote NuGet do projeto. |
| `dotnet add reference <proj>` | Adiciona a referência de outro projeto da mesma solução. |
| `dotnet publish -c Release` | Gera os arquivos otimizados para implantação em produção. |

---

## 2. Sintaxe C# - Tipos e Declarações

Foco na sintaxe moderna, limpa e expressiva do C# 14.

| Sintaxe | Exemplo / Descrição |
| :--- | :--- |
| **Variáveis Implícitas** | `var nome = "Guia";` (O compilador infere o tipo string). |
| **Constantes** | `const double Pi = 3.14159;` (Valor imutável em compilação). |
| **Strings Interpoladas** | `$"Olá, {nome}!"` (Insere variáveis diretamente na string). |
| **Raw String Literals** | `"""Texto com "aspas" sem escape"""` (Ideal para JSON/SQL). |
| **Records** | `public record Pessoa(string Nome);` (Tipos imutáveis por padrão). |
| **Construtor Primário** | `public class Servico(ILogger log) { }` (Injeção na classe). |
| **Expressões de Coleção** | `int[] numeros = [1, 2, 3];` (Sintaxe enxuta para arrays). |
| **Tuplas** | `(string Nome, int Id) = ("Admin", 1);` (Retorno de múltiplos valores). |

<div style="page-break-after: always;"></div>

---

## 3. Sintaxe C# - Controle de Fluxo

Estruturas lógicas atualizadas com *Pattern Matching*.

| Estrutura | Exemplo Prático |
| :--- | :--- |
| **if / else** | `if (x > 0) { /*...*/ } else { /*...*/ }` |
| **Operador Ternário** | `var status = idade >= 18 ? "Maior" : "Menor";` |
| **Null-Coalescing** | `var nomeReal = nomeNulo ?? "Padrão";` (Se nulo, usa o padrão). |
| **Switch Expression** | `var cor = tipo switch { 1 => "Azul", _ => "Cinza" };` |
| **Pattern Matching** | `if (obj is string { Length: > 5 } s) { /* usa 's' aqui */ }` |
| **for / foreach** | `foreach (var item in lista) { Console.WriteLine(item); }` |
| **using (Escopo)** | `using var file = new StreamReader("a.txt");` (Dispose automático). |

---

## 4. Sintaxe C# - Modificadores e OOP

Palavras-chave para organizar e proteger seu domínio.

| Modificador | Descrição |
| :--- | :--- |
| `public` | Acesso liberado para qualquer código. |
| `private` | Acesso restrito apenas ao próprio escopo da classe/struct. |
| `protected` | Acesso permitido à própria classe e suas derivadas (herança). |
| `internal` | Acesso permitido apenas dentro do mesmo *Assembly* (projeto). |
| `static` | Pertence ao tipo em si, e não a uma instância específica (objeto). |
| `readonly` | O valor só pode ser atribuído na declaração ou no construtor. |
| `required` | Força que a propriedade seja inicializada ao instanciar o objeto. |
| `init` | Permite atribuir valor apenas durante a inicialização do objeto. |
| `sealed` | Impede que a classe seja herdada por outras. |

---

## 5. Coleções e LINQ

Manipulação de dados em memória de forma declarativa.

| Comando / Método | Descrição |
| :--- | :--- |
| `List<T>` | Coleção dinâmica mais comum. Ex: `List<int> idades = [];` |
| `Dictionary<K, V>` | Coleção de chave/valor para buscas rápidas (O(1)). |
| `IEnumerable<T>` | Interface base para iteração. Retorno padrão do LINQ. |
| `Where(x => ...)` | Filtra a coleção baseada em uma condição (lambda). |
| `Select(x => ...)` | Projeta/transforma cada elemento em um novo formato. |
| `FirstOrDefault()` | Retorna o primeiro item ou nulo/padrão se não encontrar. |
| `Any(x => ...)` | Retorna `true` se pelo menos um item atender à condição. |
| `OrderBy(x => ...)` | Ordena a coleção (use `OrderByDescending` para inversa). |
| `GroupBy(x => ...)` | Agrupa elementos que compartilham a mesma chave. |

<div style="page-break-after: always;"></div>

---

## 6. Entity Framework Core CLI (`dotnet ef`)

Pré-requisito: A ferramenta global do EF Core precisa estar instalada (`dotnet tool install -g dotnet-ef`).

| Comando | Descrição |
| :--- | :--- |
| **`dotnet ef migrations add <Nome>`** | Cria uma nova migration com as alterações recentes do modelo. |
| **`dotnet ef migrations remove`** | Remove a última migration (desde que não aplicada ao banco). |
| **`dotnet ef migrations list`** | Lista todas as migrations existentes no projeto. |
| **`dotnet ef migrations script`** | Gera um script SQL contendo todas as migrations. |
| **`dotnet ef database update`** | Aplica as migrations pendentes ao banco de dados. |
| **`dotnet ef database drop`** | Exclui o banco de dados (Cuidado: ação destrutiva!). |
| **`dotnet ef dbcontext info`** | Exibe informações sobre o tipo do `DbContext` atual. |
| **`dotnet ef dbcontext list`** | Lista todos os `DbContext` disponíveis no projeto. |
| **`dotnet ef dbcontext scaffold <Conexao> <Provider>`** | Gera modelos a partir de um banco existente (Database-First). |
| **`dotnet ef dbcontext optimize`** | Gera um modelo compilado para acelerar o tempo de inicialização. |

<div style="page-break-after: always;"></div>

---

## 7. FluentValidation (Validação de Modelos)

Pré-requisito: Pacote `FluentValidation`. Crie uma classe herdando de `AbstractValidator<T>`.

| Comando / Regra | Descrição Prática |
| :--- | :--- |
| **`RuleFor(x => x.Prop)`** | Inicia a cadeia de validação para uma propriedade específica. |
| **`NotEmpty()`** | Falha se o valor for nulo, vazio ou o valor padrão (ex: `0`, `""`). |
| **`NotNull()`** | Falha estritamente se o valor for `null`. |
| **`Length(min, max)`** | Valida se uma string tem o tamanho exato entre os valores. |
| **`GreaterThan(val)`** | Falha se o número/data for menor ou igual ao valor. |
| **`LessThan(val)`** | Falha se o número/data for maior ou igual ao valor. |
| **`EmailAddress()`** | Valida se a string possui um formato de e-mail válido. |
| **`Matches("regex")`** | Valida a string contra uma Expressão Regular. |
| **`Must(x => ...)`** | Cria uma validação customizada baseada em um predicado (lambda). |
| **`WithMessage("Erro")`**| Substitui a mensagem padrão por uma personalizada para a regra anterior. |
| **`When(cond, () => { })`**| Aplica um bloco de regras condicionalmente, apenas se `cond` for `true`. |
| **`RuleForEach(x => x.L)`**| Aplica regras a cada elemento de uma coleção de forma individual. |

<div style="page-break-after: always;"></div>

---

## 8. FluentMigrator (Migrations em Código)

Pré-requisito CLI: `dotnet tool install -g FluentMigrator.DotNet.Cli`.  

### 8.1 CLI do FluentMigrator (`dotnet-fm`)

| Comando CLI | Descrição |
| :--- | :--- |
| **`dotnet-fm migrate`** | Executa todas as migrations pendentes (métodos `Up()`). |
| **`dotnet-fm migrate down`** | Reverte (rollback) a última migration aplicada (método `Down()`). |
| **`dotnet-fm rollback:to -v <versao>`**| Reverte o banco até uma versão específica de migration. |
| **`dotnet-fm rollback:all`** | Reverte todas as migrations, esvaziando a estrutura do banco. |
| **`dotnet-fm list`** | Lista todas as migrations que já foram aplicadas no banco. |

### 8.2 Sintaxe Fluente (Métodos `Up` e `Down`)

| Sintaxe | Exemplo Prático |
| :--- | :--- |
| **`Create.Table("Nome")`** | Inicia a criação de uma nova tabela. |
| **`.WithColumn("Id")`** | Adiciona uma coluna à tabela sendo criada ou alterada. |
| **`.AsInt32()` / `.AsString()`** | Define o tipo de dados da coluna. |
| **`.PrimaryKey()`** | Define a coluna atual como a Chave Primária. |
| **`.Identity()`** | Define a coluna atual como auto-incremento. |
| **`.NotNullable()` / `.Nullable()`** | Define se a coluna aceita (ou não) valores nulos. |
| **`Alter.Table("Nome")`** | Permite adicionar/modificar colunas em uma tabela existente. |
| **`Delete.Table("Nome")`** | Remove uma tabela inteira do banco de dados. |

<div style="page-break-after: always;"></div>

---

## 9. Blazor & Sintaxe Razor

O framework web full-stack do .NET. Utiliza a mistura de C# e HTML nos arquivos `.razor`.

### 9.1 CLI do Blazor

| Comando CLI | Descrição |
| :--- | :--- |
| **`dotnet new blazor`** | Cria um Blazor Web App (suporta SSR, Server e WebAssembly juntos). |
| **`dotnet new blazorwasm`**| Cria um projeto Blazor estrito em WebAssembly (Standalone). |
| **`dotnet new razorcomponent -n Nome`** | Cria um novo arquivo de componente Razor (`Nome.razor`). |

### 9.2 Diretivas Razor (Sintaxe de Componente)

| Diretiva | Descrição Prática |
| :--- | :--- |
| **`@page "/rota"`** | Define a URL pela qual o componente pode ser acessado no navegador. |
| **`@code { ... }`** | Bloco onde você escreve a lógica em C# (propriedades, métodos). |
| **`@inject Tipo Nome`** | Injeta um serviço registrado na injeção de dependência (ex: HttpClient). |
| **`@rendermode`** | Define como o componente renderiza (`InteractiveServer`, `InteractiveWebAssembly`). |
| **`@if (cond) { }`** | Renderiza o HTML interno apenas se a condição C# for verdadeira. |
| **`@foreach (v in lista)`**| Itera sobre uma coleção C# para gerar HTML repetido. |
| **`@bind="Prop"`** | *Two-way data binding*. Sincroniza o valor do HTML com a propriedade C#. |
| **`@onclick="Metodo"`** | Vincula o evento de clique do HTML a um método C# no bloco `@code`. |

<div style="page-break-after: always;"></div>

---

## 10. Dapper (Micro-ORM de Performance)

Pré-requisito: Pacote `Dapper`. Extensão direta da interface `IDbConnection` (ex: `SqlConnection`, `NpgsqlConnection`).

| Método / Comando | Descrição Prática |
| :--- | :--- |
| **`Query<T>(sql, param)`** | Executa a instrução SQL e mapeia os resultados para um `IEnumerable<T>`. |
| **`QueryFirstOrDefault<T>()`** | Retorna o primeiro registro mapeado ou `null` se não houver resultados. |
| **`QuerySingle<T>()`** | Retorna exatamente um registro (lança exceção se houver zero ou mais de um). |
| **`Execute(sql, param)`** | Executa comandos (INSERT, UPDATE, DELETE) e retorna o número de linhas afetadas. |
| **`ExecuteScalar<T>()`** | Executa a query e retorna apenas a primeira coluna da primeira linha (útil para `COUNT` ou pegar IDs inseridos). |
| **`QueryMultiple(sql)`** | Executa múltiplos *statements* SQL de uma vez. Retorna um `GridReader` para ler os vários conjuntos de resultados. |
| **Parâmetros Anônimos** | Previne *SQL Injection* passando objetos anônimos: `new { Id = 1, Status = "Ativo" }`. |
| **`DynamicParameters`** | Classe para lidar com parâmetros complexos (ex: variáveis de `OUTPUT`, listas para `IN` e Stored Procedures). |

> **Exemplo Prático Rápido:** > `var sql = "SELECT * FROM Usuarios WHERE Id = @Id";`  
> `var usuario = await conexao.QueryFirstOrDefaultAsync<Usuario>(sql, new { Id = 10 });`

---
*Gerado para a comunidade de desenvolvedores .NET.*
