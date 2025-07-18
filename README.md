# Minimal API DIO

API minimalista para gerenciamento de administradores e veículos, desenvolvida em .NET 7, utilizando Entity Framework Core e autenticação JWT.

## Funcionalidades

- Autenticação de administradores via JWT
- CRUD de administradores (com controle de perfil: Adm, Editor)
- CRUD de veículos
- Paginação nas listagens
- Validação de dados
- Documentação automática via Swagger

## Estrutura do Projeto

- `Api/`: Projeto principal da API
  - `Dominio/`: Entidades, DTOs, Enums, Interfaces, ModelViews, Serviços
  - `Infraestrutura/Db/`: DbContext e configuração do banco
  - `Migrations/`: Migrações do banco de dados
  - `Program.cs` e `Startup.cs`: Configuração da aplicação
- `Test/`: Projeto de testes automatizados

## Endpoints Principais

### Home

- `GET /`  
  Retorna mensagem de boas-vindas e link para documentação.

### Administradores

- `POST /administradores/login`  
  Autentica administrador e retorna token JWT.

- `GET /administradores`  
  Lista administradores (requer perfil Adm).

- `GET /administradores/{id}`  
  Busca administrador por ID (requer perfil Adm).

- `POST /administradores`  
  Cria novo administrador (requer perfil Adm).

### Veículos

- `POST /veiculos`  
  Cria novo veículo (requer perfil Adm ou Editor).

- `GET /veiculos`  
  Lista veículos (requer autenticação).

- `GET /veiculos/{id}`  
  Busca veículo por ID (requer perfil Adm ou Editor).

- `PUT /veiculos/{id}`  
  Atualiza veículo (requer perfil Adm).

- `DELETE /veiculos/{id}`  
  Remove veículo (requer perfil Adm).

## Banco de Dados

- MySQL
- Tabelas: `Administradores`, `Veiculos`
- Migrations e seed incluídos

## Como rodar

1. Instale o .NET 7 SDK e MySQL.
2. Configure a string de conexão em `Api/appsettings.json`:
   ```
   "ConnectionStrings": {
     "MySql": "Server=localhost;Database=minimal_api;Uid=root;Pwd=root;"
   }
   ```
3. Execute as migrações:
   ```
   dotnet ef database update --project Api
   ```
4. Rode a API:
   ```
   dotnet run --project Api
   ```
5. Acesse a documentação Swagger em `/swagger`.

## Testes

- Projeto de testes em `Test/`
- Para rodar os testes:
  ```
  dotnet test Test
  ```

## Dependências principais

- Microsoft.AspNetCore.Authentication.JwtBearer
- Microsoft.EntityFrameworkCore
- Pomelo.EntityFrameworkCore.MySql
- Swashbuckle.AspNetCore (Swagger)

## Autor

- Raphael928
