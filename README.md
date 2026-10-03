# 🕵️‍♂️ Sistema Antiplágio (API de Detecção de Similaridade Textual)

API RESTful robusta desenvolvida para análise, comparação e detecção de similaridade em documentos e trabalhos académicos. Focada na garantia da integridade académica, processamento eficiente de texto e rastreabilidade de submissões.

---

## 👨‍💻 Desenvolvedor

**Santiago da Rocha Souza**
* Bacharel em Sistemas de Informação (UEG)
* Especialista em Segurança da Informação e Inteligência Artificial
* Pós Graduando em Engenharia de Dados e IA
* Mestrando em Ciência da Computação (UFJ)
---

## 🚀 Visão Geral do Projeto

Esta aplicação atua como um motor de análise textual focado na identificação de potenciais plágios em documentos e código. O sistema gere o ciclo completo de submissão e análise, garantindo a segurança e o processamento através da seguinte hierarquia: **Autenticação Segura -> Submissão de Ficheiro (Upload) -> Processamento Textual (Extração e Limpeza) -> Motor de Detecção (Cálculo de Similaridade) -> Emissão de Resultados.**

### Principais Funcionalidades:

* **Motor de Análise Lexical:** Processamento de textos submetidos para normalização e remoção de ruídos (stop words, pontuação) antes da fase de comparação algorítmica.
* **Cálculo de Similaridade Avançado:** Utilização de algoritmos de comparação de texto para cruzar a submissão atual com o acervo histórico e referências.
* **Gestão de Submissões (Uploads):** Receção, validação e armazenamento seguro de documentos e atividades académicas.
* **Relatórios Analíticos:** Retorno detalhado do percentual de similaridade encontrado, permitindo auditoria das áreas de texto com colisão.
* **Controlo de Acesso Segregado:** Autenticação via tokens JWT para garantir que apenas utilizadores legítimos possam submeter e analisar documentos, protegendo a integridade do acervo.

---

## 🛠️ Stack Tecnológica & Arquitetura

O sistema foi construído utilizando tecnologias modernas do ecossistema Microsoft e padrões de projeto consolidados para garantir manutenibilidade, segurança e alta performance.

### Backend

* **Framework:** .NET 8 (ASP.NET Core Web API).
* **Linguagem:** C#.
* **Base de Dados:** SQL Server.
* **ORM/Micro-ORM:** Utilização conjunta de **Entity Framework Core** (para gestão de estado, migrações e operações estruturadas) e **Dapper** (focado em alta performance para consultas complexas e cruzamento rápido de grandes volumes de texto).
* **Arquitetura:** Web API estruturada com **Camada de Serviço (Services)** e **Padrão Repository (Repositories)**.
  * *Por que Repositórios?* Utilizamos o Repository Pattern para desacoplar a lógica de negócio (o motor de detecção) da camada de acesso a dados. Isto facilita a manutenção, permite testes unitários limpos e centraliza as regras de consulta SQL, evitando código duplicado nas lógicas de verificação de similaridade.
* **Documentação Interativa:** Swagger / OpenAPI integrado para testes fluídos dos endpoints.

---

## 🔒 Segurança e Auditoria

A arquitetura de segurança foi desenhada aplicando o conceito de defesa em profundidade ("Defense in Depth"), desde a infraestrutura até ao nível aplicacional:

* **Proteção de Credenciais e Segredos (DevSecOps):**
  * Gestão rigorosa de variáveis de ambiente. Ficheiros de configuração sensíveis (como o `appsettings.Development.json`) são bloqueados nativamente via `.gitignore` e isolados do histórico do Git, garantindo que as cadeias de ligação (*connection strings*) e chaves criptográficas da base de dados nunca são expostas publicamente.
* **Autenticação e Controlo de Acesso (RBAC):**
  * Implementação do padrão Bearer Authentication através de JWT (JSON Web Tokens). As chaves secretas são validadas na memória da aplicação, garantindo sessões seguras e *stateless*.
  * Filtros globais de autorização protegem os *endpoints* sensíveis de cálculo e injeção de documentos.
* **Segurança no Tratamento de Ficheiros:**
  * Validação rigorosa durante o *upload* de atividades para mitigar vulnerabilidades críticas associadas à injeção de ficheiros maliciosos no servidor.
