# Claude Marketplace

Uma coleção de plugins para o Claude Code voltados à **arquitetura de software** e à **documentação de design**. Os plugins automatizam tarefas como registrar decisões arquiteturais, gerar diagramas, analisar a arquitetura de projetos e produzir guias de desenvolvimento por linguagem.

## Plugins Disponíveis

Este marketplace oferece quatro plugins para documentação e análise arquitetural:

| Plugin | Descrição | Comandos |
|--------|-----------|----------|
| **[ADRs Management](./plugins/adrs-management/USAGE.md)** | Análise, geração e vinculação de Architecture Decision Records (ADRs) | `/adr-map`, `/adr-identify`, `/adr-generate`, `/adr-link` |
| **[Diagrams Generator](./plugins/diagrams-generator/USAGE.md)** | Geração de diagramas C4 (PlantUML) e Mermaid a partir de Feature Design Documents (FDDs) | `/c4-generate`, `/mermaid-generate` |
| **[Project Analyzer](./plugins/project-analizer/USAGE.md)** | Análise arquitetural completa, análise profunda de componentes e auditoria de dependências | `/generate-architectural-report`, `/run-dependency-audit` |
| **[Development Guidelines](./plugins/development-guidelines/USAGE.md)** | Geração de guias de desenvolvimento abrangentes e específicos por linguagem | `/generate-development-guideline` |

## Instalação

### Adicionar o Marketplace

Para usar estes plugins, primeiro adicione este marketplace ao Claude Code:

```bash
/plugin marketplace add Lucassamuel97/claude-plugins
```

Esse comando registra o repositório do GitHub como uma fonte de plugins (marketplace).

### Instalar os Plugins

Depois de adicionar o marketplace, instale os plugins individualmente:

```bash
# Instalar o plugin ADRs Management
/plugin install adrs-management@lucassamuel-plugins

# Instalar o plugin Diagrams Generator
/plugin install diagrams-generator@lucassamuel-plugins

# Instalar o plugin Project Analyzer
/plugin install project-analizer@lucassamuel-plugins

# Instalar o plugin Development Guidelines
/plugin install development-guidelines@lucassamuel-plugins
```

**Observação**: o identificador do marketplace (`lucassamuel-plugins`) é o campo `name` definido em [.claude-plugin/marketplace.json](.claude-plugin/marketplace.json). Após adicioná-lo, você também pode navegar pelos plugins disponíveis com:

```bash
/plugin
```

## Início Rápido

### ADRs Management

Documente decisões arquiteturais de forma sistemática, seguindo um fluxo de 3 fases (mapear → identificar → gerar) com vinculação ao final:

```bash
/adr-map                    # Fase 1: mapeia a base de código em módulos lógicos
/adr-identify AUTH DATA     # Fase 2: identifica ADRs em potencial nos módulos
/adr-generate BILLING       # Fase 3: gera ADRs formais no formato MADR
/adr-link                   # Vincula os ADRs com relacionamentos bidirecionais
```

Os ADRs podem ser gerados em vários idiomas (en, pt-BR, es, fr, de). O plugin aplica filtragem rigorosa — apenas cerca de 5% das descobertas viram ADRs — e usa o histórico do git para enriquecer o contexto temporal.

### Diagrams Generator

Crie documentação visual a partir de Feature Design Documents (FDDs):

```bash
/c4-generate docs/features/payment-fdd.md     # Diagramas C4 (C1–C4) em PlantUML
/mermaid-generate docs/features/auth-fdd.md   # Diagramas Mermaid (sequência, fluxo, classe, ER)
```

O idioma dos diagramas é detectado automaticamente a partir do FDD, mantendo os termos técnicos em inglês (Service, Gateway, Redis etc.). Nenhum diagrama é inventado quando o FDD não tem informação suficiente.

### Project Analyzer

Analise a arquitetura e as dependências do projeto (somente leitura — não modifica o código):

```bash
/generate-architectural-report   # Relatório arquitetural completo + análise de componentes
/run-dependency-audit            # Auditoria de dependências (versões, CVEs, licenças)
```

Inclui três agentes especializados: análise arquitetural, análise profunda de componentes e auditoria de dependências. Componentes são analisados em paralelo para resultados mais rápidos.

### Development Guidelines

Gere guias de desenvolvimento abrangentes para qualquer linguagem de programação:

```bash
/generate-development-guideline Python
/generate-development-guideline TypeScript --orm=prisma --web=express --testing=jest
/generate-development-guideline Go --orm=sqlc --web=chi --db=pgx
```

O guia é focado na **linguagem** (não em frameworks específicos): as bibliotecas informadas via parâmetros são listadas em uma seção "Project Stack" apenas como referência, enquanto os exemplos de código usam a biblioteca padrão da linguagem.

## Fluxo Combinado

Os plugins se complementam. Um fluxo de trabalho típico:

```bash
# 1. Entenda a arquitetura do projeto
/generate-architectural-report

# 2. Documente as decisões arquiteturais relevantes
/adr-map
/adr-identify AUTH DATA API
/adr-generate --include-consider AUTH DATA API
/adr-link

# 3. Gere diagramas para os componentes-chave
/c4-generate docs/features/payment-fdd.md
```

## Documentação

Para instruções detalhadas de uso, consulte a documentação de cada plugin:

- [Guia de Uso — ADRs Management](./plugins/adrs-management/USAGE.md)
- [Guia de Uso — Diagrams Generator](./plugins/diagrams-generator/USAGE.md)
- [Guia de Uso — Project Analyzer](./plugins/project-analizer/USAGE.md)
- [Guia de Uso — Development Guidelines](./plugins/development-guidelines/USAGE.md)