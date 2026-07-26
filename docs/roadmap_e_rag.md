# 🔬 Roadmap de Pesquisa, Arquitetura RAG e Evolução Tecnológica (P&D)

Este documento apresenta a trajetória de desenvolvimento do **SafeFood**, estabelecendo a transição fundamentada entre o **protótipo funcional de validação técnica** e as etapas de evolução científica planejadas para a pesquisa de Iniciação Científica.

---

## 📊 Diagnóstico do Protótipo Atual (Proof of Concept)

A versão atual do aplicativo cumpre o papel de prova de conceito operacional:

- ✅ **Infraestrutura em Flutter e Firebase**
  - Interface reativa;
  - Autenticação anônima/teste;
  - Arquitetura modular (*Feature-First*).

- ✅ **Comunicação Multimodal com LLM**
  - Integração com o **Gemini 2.5 Flash**;
  - Suporte simultâneo a texto e áudio (`.m4a`).

- ✅ **Módulo Expresso (Checklist 100% Offline)**
  - Autoavaliação sanitária baseada na **RDC nº 216/2004**.

- ✅ **Scanner de Código de Barras**
  - Leitura ótica (EAN-13);
  - Integração com a API **Open Food Facts**;
  - Classificação inicial baseada em palavras-chave.

---

## 🎯 A Fronteira Científica: Arquitetura RAG (Retrieval-Augmented Generation)

A limitação das regras determinísticas atualmente empregadas no scanner de alimentos e no módulo conversacional abre espaço para o principal eixo científico do projeto: o desenvolvimento de um pipeline **Retrieval-Augmented Generation (RAG)** alimentado por uma base de conhecimento vetorial especializada.

```text
  ┌────────────────────────────────────────────────────────────────────────┐
  │                           ENTRADA DE DADOS                             │
  │  (Código de Barras EAN-13 / Dúvida do Usuário / Pauta de Inspeção)     │
  └───────────────────────────────────┬────────────────────────────────────┘
                                      │
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │                       MOTOR DE BUSCA VETORIAL                          │
  │                     (Retrieval-Augmented Layer)                        │
  └─────────┬────────────────────────────────────────────────────┬─────────┘
            │                                                    │
            ▼                                                    ▼
┌──────────────────────────────┐                      ┌────────────────────┐
│   BASE LEGAL E NORMATIVA     │                      │ LITERATURA TÉCNICA │
│ • RDC nº 216/2004 (ANVISA)   │                      │    E CIENTÍFICA    │
│ • Normas da Vigilância       │                      │ • Matriz de Risco  │
│   Sanitária                  │                      │   Microbiológico   │
│ • Legislação de Rotulagem    │                      │ • Inspeção POA     │
└───────────┬──────────────────┘                      └──────────┬─────────┘
            │                                                    │
            └─────────────────────────┬──────────────────────────┘
                                      │
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │                      GERAÇÃO FUNDAMENTADA (LLM)                        │
  │   Respostas e orientações sem alucinação, ancoradas na literatura      │
  └────────────────────────────────────────────────────────────────────────┘
```

---

## 🧠 Duplo Eixo de Conhecimento do RAG

A arquitetura proposta organiza a recuperação de informações em dois domínios complementares.

### 📜 Eixo Normativo (Autoavaliação e Auditoria)

Responsável pela indexação vetorial da legislação sanitária, permitindo que as respostas do modelo sejam fundamentadas em documentos oficiais.

Inclui, entre outros:

- RDC nº 216/2004;
- Regulamentos da Vigilância Sanitária;
- Normas complementares aplicáveis à manipulação de alimentos.

### 🦠 Eixo Científico e de Risco Biológico (Scanner de Alimentos)

Voltado à interpretação técnica dos alimentos identificados pelo scanner.

A base vetorial será composta por literatura consolidada em:

- Microbiologia de Alimentos;
- Inspeção de Produtos de Origem Animal (POA);
- Matrizes de risco microbiológico;
- Métodos de conservação e armazenamento.

Esse segundo eixo permitirá relacionar a composição dos alimentos aos riscos microbiológicos e às recomendações de conservação fundamentadas na literatura científica.

---

## 🧪 Metodologia de Validação Científica (Alpha Testing)

Para garantir a confiabilidade das respostas produzidas pelo sistema, será conduzido um processo contínuo de validação técnica.

### 🔬 Bateria de Testes de Estresse

O assistente será submetido a diferentes cenários experimentais, incluindo:

- perguntas complexas;
- casos limítrofes;
- tentativas deliberadas de fuga de escopo;
- solicitações potencialmente ambíguas.

### 👨‍🔬 Curadoria Especializada

As respostas produzidas pelo pipeline RAG serão avaliadas qualitativamente sob supervisão do orientador.

Cada resposta será confrontada com:

- RDC nº 216/2004;
- literatura científica utilizada na construção da base vetorial;
- demais referências normativas empregadas pelo projeto.

---

## 🗺️ Roadmap de Evolução da Plataforma

Além da evolução científica, o projeto contempla melhorias graduais na arquitetura de software.

### 📈 1. Histórico de Inspeções e Evolução Temporal (Offline-First)

#### 🔒 Privacidade

- Cadastro simplificado;
- Possibilidade de utilização anônima;
- Incentivo à autoavaliação sem receio de fiscalização punitiva.

#### 📊 Acompanhamento de Desempenho

- Armazenamento local dos checklists;
- Sincronização automática com a nuvem;
- Histórico completo das inspeções realizadas.

#### 📉 Dashboards

Visualização da evolução sanitária do estabelecimento por meio de gráficos comparativos ao longo do tempo.

---

### 📄 2. Emissão de Relatórios de Conformidade

Implementação de um módulo responsável pela geração automática de documentos em PDF contendo:

- pontuação final da inspeção;
- indicadores de conformidade;
- principais não conformidades identificadas;
- recomendações de melhoria.

Os relatórios terão finalidade de acompanhamento interno do estabelecimento.

---

### 🌐 3. Consolidação do Modo Offline

A arquitetura será expandida para permitir funcionamento integral em ambientes com conectividade limitada.

Entre as funcionalidades previstas:

- sincronização assíncrona;
- armazenamento local temporário;
- envio automático dos dados quando houver conexão disponível.

Essa abordagem permitirá a utilização do aplicativo em locais como:

- câmaras frias;
- depósitos;
- áreas de armazenamento;
- ambientes com cobertura instável de internet.

---

## ⚙️ Evolução Tecnológica Prevista

| Etapa | Objetivo |
|--------|----------|
| **Protótipo Atual** | Comunicação multimodal, checklist offline e scanner integrado ao Open Food Facts |
| **Curto Prazo** | Base vetorial inicial da RDC nº 216/2004 |
| **Médio Prazo** | Implementação completa da arquitetura RAG |
| **Longo Prazo** | Expansão da base científica, dashboards, relatórios e funcionamento Offline-First |

---

<p align="center">
© 2026 <strong>Gabriel Tupynambá</strong>. Todos os direitos reservados.
</p>
