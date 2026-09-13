# CareerOps — Public Architecture Overview

Este documento descreve a arquitetura do CareerOps em nível de portfólio. Detalhes operacionais, credenciais, integrações privadas e dados reais não são publicados.

## Princípios

1. **Privacidade por padrão** — dados pessoais e histórico de candidaturas permanecem fora do repositório público.
2. **Matching explicável** — o score deve ser decomponível em fatores compreensíveis.
3. **Separação de responsabilidades** — rotas HTTP não concentram regras de negócio.
4. **Automação auditável** — ingestão e classificação devem manter origem e justificativa.
5. **Evolução incremental** — cada fatia deve ser testável antes de adicionar novas fontes ou inteligência.

## Componentes

### Job Ingestion

Responsável por receber vagas de fontes permitidas, adaptadores e entradas manuais. O resultado é convertido para um contrato interno comum antes de entrar no domínio.

### Normalization & Deduplication

Normaliza empresa, cargo, localização, modalidade, tecnologias e URL de origem. A deduplicação começa por identificadores/URLs e evolui para heurísticas adicionais.

### Candidate Profile

Representa o perfil profissional usado pelo matching. A arquitetura prevê skills, experiência, senioridade, idiomas, preferências de localização/modalidade, contratação e faixa de interesse.

### Matching Engine

Compara os requisitos normalizados da vaga com o perfil profissional. O objetivo é produzir não apenas uma nota, mas também uma explicação contendo requisitos atendidos, gaps e fatores que influenciaram a prioridade.

### Application Pipeline

Mantém o estado da oportunidade ao longo do funil, por exemplo descoberta, revisão, candidatura, entrevista, oferta, rejeição e arquivamento.

### Analytics

A evolução prevê métricas como vagas descobertas, taxa de candidatura, conversão para entrevista, fontes mais eficazes e distribuição de aderência.

## Camadas do backend

```text
HTTP / API
   │
   ▼
Routes / Controllers
   │
   ▼
Application Services
   │
   ├── Matching
   ├── Job workflow
   └── Normalization
   │
   ▼
Repositories
   │
   ▼
Database
```

As rotas validam entrada, delegam operações e transformam respostas HTTP. Regras de negócio permanecem nos serviços para facilitar testes e evolução.

## Dados públicos versus privados

| Categoria | Público nesta vitrine | Ambiente privado |
|---|---:|---:|
| Arquitetura conceitual | Sim | Sim |
| Stack e decisões técnicas | Sim | Sim |
| Exemplos fictícios | Sim | Sim |
| Código de produção completo | Não | Sim |
| Perfil profissional real estruturado | Não | Sim |
| Histórico de candidaturas | Não | Sim |
| Currículos e documentos | Não | Sim |
| Credenciais e tokens | Nunca | Secrets/ambiente seguro |

## Roadmap arquitetural

```text
MVP 0.1
API + Jobs + Matching básico + testes
        │
        ▼
MVP 0.2
Candidate Profile + Matching ponderado
        │
        ▼
MVP 0.3
PostgreSQL + migrations + pipeline
        │
        ▼
MVP 0.4
Ingestão automatizada + deduplicação
        │
        ▼
MVP 0.5
Dashboard web + analytics
        │
        ▼
Evolução
Assistência na preparação de candidaturas e aprendizado com resultados
```

## Segurança

Segredos não são versionados. Integrações utilizam variáveis de ambiente e mecanismos de secrets adequados ao ambiente de execução. Logs e exemplos públicos devem ser sanitizados antes de qualquer publicação.
