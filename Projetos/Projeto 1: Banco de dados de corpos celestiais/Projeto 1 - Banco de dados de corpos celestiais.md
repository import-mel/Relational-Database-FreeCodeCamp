# Banco de dados de corpos celestiais

Este projeto faz parte do curso de **Banco de Dados Relacionais** da freeCodeCamp. O desafio consiste em criar um banco de dados chamado `universe` que modela entidades celestiais, como galáxias, estrelas, planetas e luas, seguindo as regras estabelecidas para concluir o desafio.

## Índice
1. [Regras do Desafio](#regras-do-desafio)
2. [Modelagem dos Dados](#modelagem-dos-dados)
	1. [Tabela `Galaxy`](#tabela-galaxy)
	2. [Tabela `Star`](#tabela-star)
	3. [Tabela `Planet`](#tabela-planet)
	4. [Tabela `Moon`](#tabela-moon)
	5. [Tabela `Nebula`](#tabela-nebula)
	6. [Tabela `Mission`](#tabela-mission)
	7. [Tabela junção `Planet_Mission`](#tabela-junção-planet_mission)
    8. [Relacionamento entre as Tabelas](#relacionamento-entre-as-tabelas)
3. [Instalação e Execução](#instalação-e-execução)
4. [Conclusão](#conclusão)

## Regras do Desafio

O desafio exige que você crie um banco de dados chamado `universe` e siga as seguintes regras:
        
1. **Criação das Tabelas**:
    - Crie tabelas chamadas `galaxy`, `star`, `planet` e `moon`.
    - Cada tabela deve ter uma chave primária que incremente automaticamente.
    - Cada tabela deve ter uma coluna `name`.
        
2. **Tipos de Dados**:
    - Use o tipo `INT` para pelo menos duas colunas que não sejam chaves primárias ou estrangeiras.
    - Use o tipo `NUMERIC` pelo menos uma vez.
    - Use o tipo `TEXT` pelo menos uma vez.
    - Use o tipo `BOOLEAN` em pelo menos duas colunas.
        
3. **Relacionamentos**:
    - Cada `star` deve ter uma chave estrangeira que referencia uma linha na tabela `galaxy`.
    - Cada `planet` deve ter uma chave estrangeira que referencia uma linha na tabela `star`.
    - Cada `moon` deve ter uma chave estrangeira que referencia uma linha na tabela `planet`.
        
4. **Estrutura do Banco de Dados**:
    - O banco de dados deve ter pelo menos cinco tabelas.
    - Cada tabela deve ter pelo menos três linhas.
    - As tabelas `galaxy` e `star` devem ter pelo menos seis linhas cada.
    - A tabela `planet` deve ter pelo menos 12 linhas.
    - A tabela `moon` deve ter pelo menos 20 linhas.
    - Cada tabela deve ter pelo menos três colunas.
    - As tabelas `galaxy`, `star`, `planet` e `moon` devem ter pelo menos cinco colunas cada.
        
5. **Restrições**:
    - Pelo menos duas colunas por tabela não devem aceitar valores `NULL`.
    - Pelo menos uma coluna de cada tabela deve ser `UNIQUE`.        
    - Todas as colunas chamadas `name` devem ser do tipo `VARCHAR`.
        
6. **Convenções de Nomenclatura**:
    - Cada coluna de chave primária deve seguir o padrão `table_name_id`.
    - Cada coluna de chave estrangeira deve ter o mesmo nome da coluna que está referenciando.

## Modelagem dos Dados

Como primeiro passo do desafio, organizei e planejei a estrutura do banco de dados, levando em consideração as entidades celestiais e os relacionamentos entre elas. A modelagem dos dados é essencial nesse estágio, pois permite uma compreensão clara das interações e dependências dentro do sistema, garantindo que a base seja eficiente e escalável. A partir dessa modelagem, fui capaz de projetar as tabelas principais, detalhando suas colunas e as descrições correspondentes. A seguir, apresento uma visão geral de cada uma delas.

### Tabela `galaxy`

| Coluna                 | Tipo              | Restrições        | Descrição                                           |
| ---------------------- | ----------------- | ----------------- | --------------------------------------------------- |
| **`galaxy_id`**         | `SERIAL`          | `PRIMARY KEY`     | Identificador único da galáxia                      |
| **`galaxy_name`**       | `VARCHAR(100)`    | `UNIQUE NOT NULL` | Nome da galáxia                                     |
| **`galaxy_type`**       | `TEXT`            | `NOT NULL`        | Tipo da galáxia (Espiral, Elíptica, Irregular)      |
| **`description_galaxy`**| `TEXT`            |                   | Descrição geral da galáxia                          |
| **`distance_from_earth`**| `NUMERIC`         |                   | Distância da galáxia até a Terra                    |
| **`diameter_kly`**      | `NUMERIC(10,2)`   | `NOT NULL`        | Diâmetro da galáxia em milhares de anos-luz         |
| **`has_supernovae`**    | `BOOLEAN`         |                   | Indica se a galáxia já teve supernovas             |
| **`has_nebula`**       | `BOOLEAN`         |                   | Indica se a galáxia contém nebulosas                |
| **`mass_solar`**        | `NUMERIC(15,2)`   |                   | Massa da galáxia em relação ao Sol                  |
| **`age_billion`**       | `INT`             |                   | Idade da galáxia em bilhões de anos                 |
| **`discovery_year_galaxy`** | `INT`         |                   | Ano da descoberta da galáxia                        |

### Tabela `star`

| **Coluna**                 | **Tipo**        | **Restrições**    | **Descrição**                                          |
| -------------------------- | --------------- | ----------------- | ------------------------------------------------------ |
| **`star_id`**              | `SERIAL`        | `PRIMARY KEY`     | Identificador único da estrela                         |
| **`star_name`**            | `VARCHAR(100)`  | `UNIQUE NOT NULL` | Nome da estrela                                        |
| **`galaxy_id`**            | `INT`           | `FOREIGN KEY`     | Referência à galáxia                                   |
| **`star_type`**            | `TEXT`          | `NOT NULL`        | Classificação da estrela (ex: Anã, Supergigante, etc.) |
| **`spectral_type`**        | `VARCHAR(10)`   | `NOT NULL`        | Tipo espectral (O, B, A, F, G, K, M)                   |
| **`temperature_k`**        | `NUMERIC(10,2)` | `NOT NULL`        | Temperatura da estrela em Kelvin                       |
| **`luminosity`**           | `NUMERIC(10,2)` |                   | Luminosidade em relação ao Sol                         |
| **`mass_solar`**           | `NUMERIC(10,2)` |                   | Massa da estrela em relação ao Sol                     |
| **`main_sequence`**        | `BOOLEAN`       | `NOT NULL`        | Indica se a estrela está na sequência principal        |
| **`rotation_period_days`** | `NUMERIC(10,2)` |                   | Período de rotação da estrela (dias)                   |

### Tabela `planet`

| Coluna                      | Tipo            | Restrições        | Descrição                                                                  |
| --------------------------- | --------------- | ----------------- | -------------------------------------------------------------------------- |
| **`planet_id`**             | `SERIAL`        | `PRIMARY KEY`     | Identificador único do planeta                                             |
| **`planet_name`**           | `VARCHAR(100)`  | `UNIQUE NOT NULL` | Nome do planeta                                                            |
| **`star_id`**               | `INT`           | `FOREIGN KEY`     | Referência à estrela                                                       |
| **`orbital_period_days`**   | `NUMERIC(10,2)` | `NOT NULL`        | Período orbital em dias                                                    |
| **`is_exoplanet`**          | `BOOLEAN`       |                   | Indica se o planeta é um exoplaneta (está dentro ou fora do sistema solar) |
| **`radius_km`**             | `NUMERIC(12,2)` | `NOT NULL`        | Raio do planeta em km                                                      |
| **`gravity_m_s2`**          | `NUMERIC(10,2)` |                   | Gravidade do planeta em m/s²                                               |
| **`has_life`**              | `BOOLEAN`       | `NOT NULL`        | Indica se há evidência de vida                                             |
| **`atmosphere`**            | `TEXT`          |                   | Composição da atmosfera                                                    |
| **`surface_temperature_c`** | `NUMERIC(10,2)` |                   | Temperatura média da superfície em °C                                      |
| **`discovery_year`**        | `INT`           |                   | Ano da descoberta do planeta                                               |
| **`distance_from_star_km`** | `NUMERIC(12,2)` |                   | Distância da estrela do sistema em que o planeta se encontra               |

### Tabela `moon`
| Coluna                        | Tipo            | Restrições        | Descrição                                       |
| ----------------------------- | --------------- | ----------------- | ----------------------------------------------- |
| **`moon_id`**                 | `SERIAL`        | `PRIMARY KEY`     | Identificador único da lua                      |
| **`moon_name`**               | `VARCHAR(100)`  | `UNIQUE NOT NULL` | Nome da lua                                     |
| **`planet_id`**               | `INT`           | `FOREIGN KEY `    | Referência ao planeta                           |
| **`radius_km`**               | `NUMERIC(10,2)` | `NOT NULL`        | Raio da lua em km                               |
| **`orbital_period_days`**     | `NUMERIC(10,2)` | `NOT NULL`        | Período orbital em dias                         |
| **`tidally_locked`**          | `BOOLEAN`       | `NOT NULL`        | Indica se a lua está travada gravitacionalmente |
| **`composition_moon`**             | `TEXT`          |                   | Composição da lua                               |
| **`distance_from_planet_km`** | `NUMERIC(10,2)` |                   | Distância média da lua ao planeta               |

### Tabela `nebula`

| Coluna               | Tipo            | Restrições    | Descrição                                                                |
| -------------------- | --------------- | ------------- | ------------------------------------------------------------------------ |
| **`nebula_id`**      | `SERIAL`        | `PRIMARY KEY` | Identificador único da nebulosa.                                         |
| **`nebula_name`**    | `VARCHAR(100)`  | `UNIQUE` `NOT NULL`    | Nome da nebulosa (ex: "Nebulosa de Órion", "Nebulosa do Caranguejo").    |
| **`nebula_type`**    | `VARCHAR(50)`   | `NOT NULL`    | Tipo da nebulosa (ex: "Emissão", "Reflexão", "Escuridão", "Planetária"). |
| **`galaxy_id`**      | `INT`           | `FOREIGN KEY` | Referência à galáxia onde a nebulosa está localizada.                    |
| **`diameter_ly`**    | `NUMERIC(10,2)` | `NOT NULL`    | Diâmetro da nebulosa, medido em anos-luz.                                |
| **`distance_ly`**    | `NUMERIC(10,2)` | `NOT NULL`    | Distância da nebulosa em relação à Terra, em anos-luz.                   |
| **`luminosity`**     | `NUMERIC(15,2)` |               | Luminosidade da nebulosa, medida em relação ao Sol.                      |
| **`composition_nebula`**    | `TEXT`          |               | Composição da nebulosa (ex: "Hidrogênio, hélio, poeira interestelar").   |
| **`discovery_year`** | `INT`           |               | Ano em que a nebulosa foi descoberta.                                    |
| **`location_nebula`**       | `TEXT`          |               | Localização da nebulosa (ex: "Constelação de Órion", "Braço de Órion").  |
| **`photo_url`**      | `TEXT`          |               | URL de uma foto ou imagem associada à nebulosa.                          |


### Tabela `mission`

| Coluna                    | Tipo            | Restrições    | Descrição                                                 |
| ------------------------- | --------------- | ------------- | --------------------------------------------------------- |
| **`mission_id`**          | `SERIAL`        | `PRIMARY KEY` | Identificador único da missão.                            |
| **`mission_name`**        | `VARCHAR(100)`  | `UNIQUE` `NOT NULL`    | Nome da missão (ex: "Mars 2020", "Voyager 2").            |
| **`mission_type`**        | `VARCHAR(100)`  | `NOT NULL`    | tipo de missão (exploração, mapeamento, observação, etc.) |
| **`agency`**              | `VARCHAR(100)`  | `NOT NULL`    | Agência responsável pela missão (ex: "NASA", "ESA").      |
| **`launch_date`**         | `DATE`          | `NOT NULL`    | Data de lançamento da missão.                             |
| **`budget`**              | `NUMERIC(15,2)` |               | Orçamento total da missão (USD).                                |
| **`description_mission`** | `TEXT`          |               | Descrição geral da missão e seus objetivos.               |

### Tabela junção `planet_mission`

| Coluna                  | Tipo          | Restrições    | Descrição                                                                       |
| ----------------------- | ------------- | ------------- | ------------------------------------------------------------------------------- |
| **`planet_mission_id`** | `SERIAL`      | `PRIMARY KEY` | Identificador único do relacionamento.                                          |
| **`planet_id`**         | `INT`         | `FOREIGN KEY` | Referência ao planeta na tabela `Planet`.                                       |
| **`mission_id`**        | `INT`         | `FOREIGN KEY` | Referência à missão na tabela `Mission`.                                        |
| **`mission_status`**    | `VARCHAR(50)` | `NOT NULL`    | Status da missão em relação ao planeta (ex: "ongoing", "completed", "aborted"). |
| **`start_date`**        | `DATE`        | `NOT NULL`    | Data de início da missão para aquele planeta.                                   |
| **`end_date`**          | `DATE`        |               | Data de término da missão para aquele planeta, se aplicável.                    |
| **`results`**           | `TEXT`        |               | Resultados ou descobertas da missão em relação ao planeta.                      |


### Relacionamento entre as Tabelas

Abaixo estão descritos os relacionamentos entre as tabelas, incluindo o tipo de associação entre elas:

- **Galaxy → Star: 1:N (um-para-muitos)** - Uma galáxia (`Galaxy`) pode conter **muitas estrelas** (`Star`), mas uma estrela pertence a **apenas uma galáxia**.
- **Star → Planet:** **1:N (um-para-muitos)** - Uma estrela (`Star`) pode ter **muitos planetas** (`Planet`), mas um planeta orbita **apenas uma estrela**.
- **Planet → Moon**: **1:N (um-para-muitos)** - Um planeta (`Planet`) pode ter **muitas luas** (`Moon`), mas uma lua orbita **apenas um planeta**.


Além dos relacionamentos propostos inicialmente no desafio, foram adicionados dois novos relacionamentos para expandir o modelo de dados:

- **Galaxy → Nebula**: **1:N (um-para-muitos)** - Uma galáxia (`Galaxy`) pode conter **muitas nebulosas** (`Nebula`), mas uma nebulosa está localizada em **apenas uma galáxia**
- **Planeta_Missão (N:N - muitos-para-muitos)**
	- A tabela `Planet_Mission` é uma **tabela de junção** que estabelece um relacionamento muitos-para-muitos entre as tabelas `Planet` e `Mission`. Esse relacionamento foi criado para representar cenários complexos, como:
	    - Uma missão pode explorar **múltiplos planetas** (por exemplo, uma missão interplanetária que visita Marte e Júpiter).
	    - Um planeta pode ser alvo de **diversas missões** (por exemplo, Marte, que foi explorado por várias missões ao longo dos anos).
    
	- Como resultado, o relacionamento entre as tabelas **Mission → Planet_Mission** e **Planet → Planet_Mission** é de **1:N (um-para-muitos)**

## Instalação e Execução

Para executar este projeto no terminal interativo do `psql`, siga os passos abaixo para configurar o banco de dados e rodar os scripts SQL.

### 1. Pré-requisitos

Antes de começar, certifique-se de ter as seguintes ferramentas instaladas:

- **PostgreSQL**: Sistema de gerenciamento de banco de dados relacional utilizado neste projeto. [Instruções de instalação do PostgreSQL](https://www.postgresql.org/download/)
- **Git**: Para clonar o repositório. [Instruções de instalação do Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

### 2. Clonando o Repositório

Clone o repositório para a sua máquina local usando o Git. No terminal, execute:

```bash
git clone https://github.com/seu-usuario/universe-database.git
```

Acesse o diretório do projeto:

```bash
cd universe-database
```

### 3. Criando o Banco de Dados

Agora, crie um banco de dados chamado `universe` no PostgreSQL.

1. Abra o terminal e execute o comando abaixo para acessar o PostgreSQL:

```bash
psql --username=seu_usuário --dbname=postgres
```

Substitua `seu_usuario` pelo nome de usuário do PostgreSQL.

2. No terminal interativo do `psql`, crie o banco de dados:

```sql
CREATE DATABASE universe;
```

1. Conecte-se ao banco de dados `universe`:

```sql
\c universe
```

### 4. Executando o Script SQL

Agora que você está conectado ao banco de dados `universe`, execute o script SQL para criar a estrutura do banco de dados (tabelas, restrições, etc.).

2. Para rodar o script `universe.sql` que cria as tabelas e configura os relacionamentos, execute o seguinte comando no terminal do `psql`:

```sql
\i /caminho/para/o/arquivo/universe.sql
```

Substitua `/caminho/para/o/arquivo/` pelo caminho completo onde o arquivo `universe.sql` está localizado.

### 5. Verificando a Estrutura do Banco de Dados

Após executar o script, você pode verificar se as tabelas foram criadas corretamente. No terminal do `psql`, execute o seguinte comando:

```sql
\dt
```

Isso exibirá a lista de tabelas criadas no banco de dados `universe`.

## Conclusão

Ao concluir este projeto, pude consolidar meus conhecimentos em modelagem de dados e em como estruturar um banco de dados relacional eficiente. Durante o desenvolvimento, aprendi a importância de planejar com cuidado as entidades e os relacionamentos entre elas, garantindo que o banco de dados fosse não apenas funcional, mas também escalável e organizado. O desafio me proporcionou uma visão mais clara sobre como implementar restrições e relacionamentos complexos, além de me permitir explorar detalhes técnicos, como tipos de dados, normalização e a criação de tabelas de junção.