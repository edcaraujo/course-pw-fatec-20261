---
marp: true

author: "Eduardo Cruz Araujo"
title: "Programação Web"
description: "Disciplina de Programação Web."

theme: "default"
class: "invert"

footer: "Eduardo Cruz Araujo | Fatec | 2026.1 | Programação Web | API: Contextualização"

paginate: "true"

---

# Programação Web :mortar_board:
## API: Contextualização

---

API: Contextualização
## O que é uma API?

---

## O que é uma API?

Uma API (**A**pplication **P**rogramming **I**nterface) é um conjunto de regras, protocolos e ferramentas que define a comunicação e a interoperabilidade entre diferentes componentes de software. 

---

## O que é uma API?

Ela funciona como um contrato que especifica como um cliente (uma aplicação, um serviço, etc.) deve interagir com um servidor para acessar ou manipular recursos.

---

## O que é uma API?

*A Analogia do Restaurante*

- **Você (Cliente):** O seu aplicativo.
- **O Cardápio:** A documentação da API.
- **O Garçom (API):** Recebe seu pedido e o leva para a cozinha.
- **A Cozinha (Servidor):** Processa o pedido e prepara a resposta.

---

## Por que usamos APIs?

- **Modularidade:** Componentes independentes.
- **Reutilização:** O mesmo serviço para diferentes plataformas (Web, Mobile, IoT).
- **Interoperabilidade:** Sistemas diferentes "conversando" entre si.
- **Acesso a Dados e Serviços:** Pagamentos, mapas, dados meteorológicos.

---

API: Contextualização
## Protocolos e Arquiteturas

---

## Protocolos e Arquiteturas

- **HTTP/HTTPS**: O protocolo de comunicação principal da web. Métodos (GET, POST, PUT, DELETE), cabeçalhos e códigos de status.

- **REST** (Representational State Transfer): A arquitetura mais popular para APIs web. APIs que seguem os princípios REST são chamadas de **APIs RESTful**.

---

## Protocolos e Arquiteturas

- **SOAP** (Simple Object Access Protocol): Uma alternativa mais antiga e "pesada", mas ainda utilizada em sistemas corporativos.

- **GraphQL**: Uma abordagem mais moderna para resolver problemas de over-fetching e under-fetching.

---

## Protocolos e Arquiteturas

| Característica | REST | SOAP | GraphQL |
| :--- | :--- | :--- | :--- |
| **Simplicidade** | Alta | Baixa | Média |
| **Flexibilidade** | Média | Baixa | Alta |
| **Protocolo** | HTTP | HTTP, SMTP | HTTP |
| **Formato** | JSON, XML | XML | JSON |

---

API: Contextualização
## HTTP/HTTPS

---

## HTTP/HTTPS

- **HTTP (Hypertext Transfer Protocol):**
  - Protocolo stateless (sem estado) para a web.
  - A base de toda comunicação API.

- **HTTPS (HTTP Secure):**
  - A versão segura do HTTP.
  - Criptografia para proteger os dados.

---

## REST

**REST (*Representational State Transfer*)** é um estilo arquitetural para sistemas distribuídos que utiliza um subconjunto de HTTP. APIs que seguem os princípios REST são chamadas de **APIs RESTful**.

---

## REST

- **Cliente-Servidor**: Separação de responsabilidades, permitindo que cliente e servidor evoluam independentemente.
- **Stateless (Sem Estado)**: Cada requisição do cliente para o servidor deve conter todas as informações necessárias para que o servidor entenda a requisição. O servidor não armazena informações sobre as requisições anteriores do cliente.

---

## REST


- **Cacheable**: As respostas do servidor podem ser marcadas como cacheáveis ou não, permitindo que os clientes e intermediários armazenem em cache as respostas para melhorar a performance.

---

## REST

- **Uniform Interface (Interface Uniforme)**: Simplifica a arquitetura e melhora a visibilidade.
    - **Identificação de Recursos**: Recursos são identificados por URIs.
    - **Manipulação de Recursos via Representações**: O cliente manipula recursos utilizando representações (ex: JSON, XML).
    - **Mensagens Auto-descritivas**: Cada mensagem contém informações suficientes para o cliente entender como processá-la.
    - **HATEOAS (Hypermedia As The Engine Of Application State)**: O cliente interage com a aplicação inteiramente através de hiperlinks contidos nas representações dos recursos.

---

## Métodos

Os **métodos HTTP**, também conhecidos como verbos HTTP, indicam a ação que você deseja realizar em um recurso específico. Eles são a base da comunicação cliente-servidor na web.

---

- **GET**: Solicita a representação de um recurso específico. Não deve ter efeitos colaterais (não muda o estado do servidor).
    - Exemplo: `GET /produtos/123` (Obter detalhes do produto com ID 123)

---

- **POST**: Envia dados para serem processados a um recurso específico. Geralmente resulta na criação de um novo recurso.
    - Exemplo: `POST /usuarios` (Criar um novo usuário)

---

- **PUT**: Atualiza um recurso existente ou cria um se ele não existir, utilizando a carga de dados fornecida. É idempotente (múltiplas requisições resultam no mesmo estado).
    - Exemplo: `PUT /produtos/123` (Atualizar o produto com ID 123)

---

- **DELETE**: Remove um recurso específico.
    - Exemplo: `DELETE /produtos/123` (Remover o produto com ID 123)

---

- **PATCH**: Aplica modificações parciais a um recurso. É uma alternativa ao PUT para atualizações incrementais.
    - Exemplo: `PATCH /usuarios/456` (Atualizar apenas o email do usuário com ID 456)

---

- **HEAD**: É semelhante ao GET, mas solicita apenas os cabeçalhos de resposta, sem o corpo. Útil para verificar a existência de um recurso ou seus metadados.
- **OPTIONS**: Descreve as opções de comunicação para o recurso de destino.

---

## Códigos de Status

Os **códigos de status HTTP** são respostas numéricas que o servidor envia ao cliente para indicar o status da requisição. Eles são essenciais para depurar e entender o que aconteceu durante a interação.

---

  * **1xx - Informacional**: A requisição foi recebida e o processo continua.
  * **2xx - Sucesso**: A ação foi recebida, entendida e aceita.
    * **200 OK**: Requisição bem-sucedida.
    * **201 Created**: Novo recurso foi criado com sucesso.
    * **204 No Content**: Ação bem-sucedida, mas sem conteúdo para retornar.

---

- **3xx - Redirecionamento**: É necessária uma ação adicional para completar a requisição.
   - **301 Moved Permanently**: O recurso foi movido permanentemente para uma nova URL.
   - **302 Found (Previously "Moved Temporarily")**: O recurso foi encontrado temporariamente em uma nova URL.

---

- **4xx - Erro do Cliente**: A requisição contém sintaxe incorreta ou não pode ser satisfeita.
    - **400 Bad Request**: A requisição é inválida.
    - **401 Unauthorized**: Autenticação é necessária.
    - **403 Forbidden**: O cliente não tem permissão para acessar o recurso.
    - **404 Not Found**: O recurso solicitado não foi encontrado.
    - **405 Method Not Allowed**: O método HTTP usado não é permitido para o recurso.

---

- **5xx - Erro do Servidor**: O servidor falhou ao cumprir uma requisição aparentemente válida.
    - **500 Internal Server Error**: Um erro inesperado ocorreu no servidor.
    - **502 Bad Gateway**: O servidor atuando como gateway ou proxy recebeu uma resposta inválida de um servidor upstream.
    - **503 Service Unavailable**: O servidor não está pronto para lidar com a requisição (ex: sobrecarga ou manutenção).

---

- [https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)
- [https://http.cat/](https://http.cat/)
- [https://http.dog/](https://http.dog/)

---

API: Contextualização
## Formatos de Dados

---

## Formatos de Dados

**JSON (*JavaScript Object Notation*)** e **XML (*Extensible Markup Language*)** são formatos amplamente utilizados para troca de dados em APIs web.

- **JSON** para a maioria dos **novos desenvolvimentos de APIs web**, onde leveza, agilidade e facilidade de uso são prioritárias.
- **XML** para cenários que exigem **validação de dados rigorosa, integração com sistemas legados ou representação de documentos hierárquicos muito complexos**.

---

### JSON

- **Sintaxe**: Baseado na notação de objetos do JavaScript.
- **Estrutura**: `{ "chave": "valor", "array": [1, 2, 3] }`
- **Vantagens**: Leve, fácil de ler e escrever por humanos e máquinas, amplamente suportado por linguagens de programação.
- **Uso Comum**: Preferido na maioria das APIs RESTful modernas.

---

### XML

- **Sintaxe**: Linguagem de marcação com tags.
  * **Estrutura**:
    ```xml
    <produto>
        <nome>Notebook</nome>
        <preco>2500.00</preco>
    </produto>
    ```
- **Vantagens**: Bem estruturado, robusto para documentos complexos, suporte a schemas (XSD) para validação.
- **Uso Comum**: Ainda presente em sistemas legados e algumas APIs SOAP.

---

API: Contextualização
## Endpoints

---

## Recursos

- Um **Recurso** é qualquer objeto ou dado que você queira expor na sua API.
    - Ex: um usuário, um produto, um pedido.
- Pense em "coisas" (substantivos), não em "ações" (verbos).
- **ERRADO:** `/getUsers`, `/createProduct`
- **CERTO:** `/users`, `/products`

---

## Nomenclatura e Pluralização

- O endpoint é a URL que identifica um recurso.
- Sempre use **substantivos no plural** para as coleções de recursos.
    - `/products` (coleção de produtos)
    - `/users` (coleção de usuários)
- Use **o verbo HTTP** para a ação.
    - `GET /products` → Lista todos os produtos
    - `POST /products` → Cria um novo produto

---

## Nomenclatura e Pluralização

- Use o plural seguido de um **ID único** para acessar um recurso individual.
    - `/products/42` (produto com ID 42)
    - `/users/johndoe` (usuário com nome de usuário `johndoe`)
- Ação via verbo HTTP:
    - `GET /products/42` → Pega os dados do produto 42
    - `PUT /products/42` → Atualiza o produto 42
    - `DELETE /products/42` → Deleta o produto 42

---

## Aninhamento (Nested Resources)

- Use o aninhamento para mostrar a relação entre recursos.
- **Sintaxe:** `/recurso-pai/{id-pai}/recurso-filho`
- **Exemplo:** Comentários de um post
    - `GET /posts/1/comments` → Lista todos os comentários do post 1.
    - `POST /posts/1/comments` → Cria um novo comentário no post 1.

---

## Exemplo

| Verbo HTTP | Endpoint | Descrição |
| :--- | :--- | :--- |
| **`GET`** | `/users` | Lista todos os usuários. |
| **`POST`** | `/users` | Cria um novo usuário. |
| **`GET`** | `/users/5` | Retorna o usuário com ID 5. |
| **`PUT`** | `/users/5` | Atualiza o usuário com ID 5. |
| **`DELETE`**| `/users/5` | Deleta o usuário com ID 5. |
| **`GET`** | `/users/5/posts` | Lista posts do usuário 5. |

---

## Versionamento

- Sua API está em produção e muitos clientes a estão usando.
- Você precisa adicionar um novo campo ou alterar o formato de dados.
- **Problema:** A alteração pode quebrar os aplicativos dos clientes.
- **Solução:** Crie uma nova versão para a API.

---

## Versionamento

- **1. Versionamento por URL:**
    - A forma mais comum e recomendada.
    - A versão é parte da URL.
    - **Exemplo:** `api.exemplo.com/v1/users` e `api.exemplo.com/v2/users`

---

## Versionamento

- **2. Versionamento por Header:**
    - A versão é informada no cabeçalho HTTP.
    - Mais limpo na URL, mas menos visível.
    - **Exemplo:** `Accept: application/vnd.exemplo.v1+json`

---

## Versionamento

- **3. Versionamento por Query Parameter:**
    - A versão é passada como parâmetro na URL.
    - **Exemplo:** `api.exemplo.com/users?version=2`

---

API: Contextualização
## Síncrono vs. Assíncrono

---

## APIs Síncronas

- O cliente **faz uma requisição** e **espera** pela resposta.
- O processo fica "bloqueado" até que a resposta chegue.
- **Analogia:** Ligar para um restaurante, fazer o pedido e ficar na linha esperando a confirmação.

---

## APIs Síncronas

- **Vantagens:**
    - Simples de implementar e entender.
- **Desvantagens:**
    - Pode bloquear o sistema e causar lentidão.
    - Ineficiente para processos longos.

---

## APIs Assíncronas

- O cliente faz a requisição e **continua seu trabalho** sem esperar.
- A resposta é enviada quando estiver pronta.
- **Analogia:** Fazer um pedido por um aplicativo e receber uma notificação quando ele estiver pronto para ser retirado.

---

## APIs Assíncronas

- **Vantagens:**
    - Não bloqueia o sistema.
    - Eficiente para processos demorados.
- **Desvantagens:**
    - Mais complexo de implementar.
    - Requer um mecanismo para notificar o cliente (ex: *callbacks*).

---

## APIs Assíncronas

- **Webhooks:**
    - Um tipo de *callback* HTTP.
    - A API notifica o cliente quando um evento acontece.
    - Ex: um sistema de pagamentos notifica seu servidor quando uma transação é concluída.

---

## APIs Assíncronas

- **WebSockets:**
    - Permitem uma comunicação **bidirecional e contínua** entre cliente e servidor.
    - Úteis para aplicações em tempo real.
    - Ex: chats, jogos online, cotações de bolsa.

---

## Casos de uso

| Cenário | Síncrono | Assíncrono |
| :--- | :--- | :--- |
| **Login de usuário** | ✔️ | ❌ |
| **Processamento de vídeo** | ❌ | ✔️ |
| **Obter dados de perfil** | ✔️ | ❌ |
| **Notificação de novos e-mails**| ❌ | ✔️ |
| **Comunicação em chat**| ❌ | ✔️ |

---

# Obrigado :metal:

---

## Eduardo Cruz Araujo

- E-mail: [eduardo.araujo28@fatec.sp.gov.br](eduardo.araujo28@fatec.sp.gov.br)
- Linkedin: [edcaraujo](https://www.instagram.com/)
- Github: [edcaraujo](https://github.com/edcaraujo)