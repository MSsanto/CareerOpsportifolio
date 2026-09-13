# CareerOps Portfolio

CareerOps é uma plataforma pessoal para organizar e automatizar operações de carreira: descoberta de vagas, análise de aderência, priorização de oportunidades e acompanhamento de candidaturas.

> Este repositório é a vitrine pública e sanitizada do projeto. O código de produção, integrações, dados de candidaturas, documentos pessoais e configurações sensíveis permanecem em repositório privado.

## Problema

Buscar emprego em múltiplas plataformas gera dados dispersos, candidaturas duplicadas, baixa rastreabilidade e muito trabalho manual para comparar requisitos, adaptar currículos e acompanhar processos seletivos.

O CareerOps transforma esse fluxo em uma operação estruturada e mensurável.

## Objetivos

- centralizar oportunidades encontradas em diferentes fontes;
- normalizar dados de vagas;
- reduzir duplicidades;
- calcular aderência entre vaga e perfil profissional;
- explicar os principais pontos fortes e gaps de cada oportunidade;
- priorizar vagas com maior potencial;
- acompanhar candidaturas, entrevistas e resultados;
- apoiar a criação de materiais direcionados para cada candidatura.

## Fluxo do produto

```text
Fontes de vagas
      │
      ▼
Ingestão / coleta
      │
      ▼
Normalização e deduplicação
      │
      ├─────────────► Perfil profissional
      │                    │
      └─────────────┬──────┘
                    ▼
             Matching Engine
                    │
                    ▼
         Priorização de vagas
                    │
                    ▼
        Pipeline de candidaturas
                    │
                    ▼
         Métricas e aprendizado
```

## Matching explicável

A primeira versão do motor utiliza regras determinísticas para evitar uma pontuação de "caixa-preta". A evolução prevista considera pesos independentes para requisitos técnicos, experiência, senioridade, idioma, localização, modalidade de trabalho, contratação e faixa salarial.

Exemplo fictício:

```text
Application Support Analyst
CareerOps Score: 89%

Skills técnicas           92%
Experiência               95%
Idioma                    80%
Modalidade               100%
Faixa salarial            85%

Recomendação: ALTA PRIORIDADE

Pontos fortes
✓ suporte técnico e troubleshooting
✓ redes e ambientes Linux/Windows
✓ APIs e bancos de dados

Gaps
△ inglês avançado desejável
△ experiência específica com uma ferramenta do cliente
```

## Stack atual

### Backend

- Python 3.12
- FastAPI
- Pydantic
- SQLAlchemy 2
- REST / OpenAPI

### Qualidade e entrega

- Pytest
- Ruff
- Docker
- GitHub Actions

### Evolução planejada

- PostgreSQL
- migrations
- aplicação web responsiva
- dashboard de oportunidades
- ingestão automatizada
- matching ponderado
- analytics do funil de candidaturas
- geração assistida de materiais para candidatura

## Arquitetura

O projeto é desenvolvido em camadas, mantendo regras de negócio fora das rotas HTTP e separando ingestão, domínio, persistência e apresentação.

```text
┌────────────────────────────────────────────┐
│                  Web UI                    │
└─────────────────────┬──────────────────────┘
                      │ REST
┌─────────────────────▼──────────────────────┐
│                FastAPI API                 │
├────────────────────────────────────────────┤
│ Services / Matching / Application Workflow │
├────────────────────────────────────────────┤
│ Repositories / Persistence                 │
└─────────────────────┬──────────────────────┘
                      │
                 PostgreSQL

        ▲
        │
Job ingestion / connectors / scheduled jobs
```

Mais detalhes: [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).

## Estado do projeto

### MVP 0.1

- [x] API REST inicial
- [x] modelo de vaga
- [x] criação, listagem e consulta de oportunidades
- [x] prevenção básica de duplicidade por URL
- [x] matching inicial por skills
- [x] score persistido
- [x] testes unitários iniciais
- [x] lint automatizado
- [x] Dockerfile
- [x] CI no GitHub Actions

### Próximas etapas

- [ ] perfil profissional estruturado e versionado
- [ ] matching ponderado e explicável v2
- [ ] PostgreSQL e migrations
- [ ] dashboard web
- [ ] ingestão automática de vagas
- [ ] pipeline completo de candidatura
- [ ] métricas de conversão

## Privacidade e segurança

O CareerOps manipula informações profissionais e potencialmente pessoais. Por isso, a implementação de produção permanece privada.

Este repositório público não contém:

- currículos reais;
- histórico de candidaturas;
- empresas/processos privados associados ao usuário;
- salários ou preferências pessoais reais;
- mensagens ou e-mails;
- tokens, credenciais ou chaves de API;
- dumps de banco de dados;
- código de integração que dependa de segredos.

Todos os exemplos públicos utilizam dados fictícios ou sanitizados.

## Sobre esta vitrine

Este repositório existe para demonstrar o raciocínio de produto, arquitetura, decisões técnicas, evolução e práticas de engenharia do CareerOps sem expor o ambiente privado utilizado no dia a dia.
