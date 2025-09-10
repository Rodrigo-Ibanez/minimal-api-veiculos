# Minimal API de Veículos

API em .NET 7 utilizando **Minimal APIs** para cadastro de veículos e gerenciamento de administradores com autenticação **JWT**.

Este projeto foi ajustado para o **desafio DIO**, incluindo correção da leitura da chave JWT, remoção de `RequireAuthorization` duplicado e configuração correta do Swagger.

---

## Tecnologias
- C# / .NET 7
- Minimal API
- JWT (Json Web Token)
- EF Core (MySQL)
- Swagger (OpenAPI)
- Testes de integração (WebApplicationFactory)

---

## Funcionalidades

- Login de administradores e geração de token JWT
- CRUD de administradores (somente usuários com role `Adm`)
- CRUD de veículos (roles `Adm` e `Editor`)
- Validação básica de DTOs
- Swagger UI integrado para teste rápido de endpoints

---

## Endpoints Principais

| Método | Endpoint | Descrição | Roles |
|--------|----------|-----------|-------|
| POST   | `/administradores/login` | Login do administrador e retorno de token JWT | Todos |
| GET    | `/administradores`       | Listar administradores | Adm |
| POST   | `/administradores`       | Criar administrador | Adm |
| GET    | `/veiculos`             | Listar veículos | Adm, Editor |
| POST   | `/veiculos`             | Criar veículo | Adm, Editor |
| PUT    | `/veiculos/{id}`        | Atualizar veículo | Adm |
| DELETE | `/veiculos/{id}`        | Deletar veículo | Adm |

---

## Ajustes aplicados

1. **JWT**  
   - Alterada leitura da chave JWT para:  
     ```csharp
     key = Configuration["Jwt:Key"] ?? "";
     ```

2. **RequireAuthorization**  
   - Removidos `RequireAuthorization()` duplicados nas rotas, deixando apenas as roles específicas.

3. **Swagger**  
   - Configurado com endpoint explícito:  
     ```csharp
     app.UseSwagger();
     app.UseSwaggerUI(c =>
     {
         c.SwaggerEndpoint("/swagger/v1/swagger.json", "Minimal API V1");
     });
     ```

---

## Como rodar a aplicação

1. Clone o repositório:

```bash
git clone https://github.com/Rodrigo-Ibanez/minimal-api-veiculos.git
cd minimal-api-veiculos
