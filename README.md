# 🛡️ SafeFood — Documentação Técnica do Protótipo Funcional

Bem-vindo ao repositório de documentação e auditoria visual do **SafeFood**: um protótipo de aplicativo móvel desenvolvido para simplificar a autoavaliação sanitária e a orientação sobre segurança dos alimentos, com base na **RDC nº 216/2004 (ANVISA)**.

> **Nota de Autoria e Confidencialidade:**  
> Este repositório destina-se exclusivamente à demonstração visual, arquitetural e documental da aplicação. O código-fonte integral permanece em repositório privado sob propriedade e autoria de **Gabriel Tupynambá**.

---

## 📱 Visão Geral do Sistema

O aplicativo combina três módulos principais para auxiliar manipuladores e consumidores:

1. **Modo Expresso (Checklist Offline):** Formulário interativo com 20 pontos de checagem derivados da RDC 216.
2. **Scanner de Alimentos:** Leitura de código de barras (EAN-13) integrada à base internacional *Open Food Facts*, exibindo informações do produto e diretrizes sanitárias de conservação.
3. **Inspetor IA:** Assistente conversacional alimentado por Inteligência Artificial (Google Gemini), programado com restrição estrita de escopo (*System Instruction*) para responder apenas a temas de segurança alimentar e ignorar assuntos alheios.

---

## 🖼️ Fluxo de Funcionamento e Telas Reais

### 1. Autenticação e Painel Principal
O sistema conta com fluxo simplificado de login/cadastro e painel dinâmico com navegação direta para os três módulos de inspeção.

| Tela de Entrada | Painel Principal |
| :---: | :---: |
| <img src="assets/login.jpeg" width="250"/> | <img src="assets/painel.jpeg" width="250"/> |

---

### 2. Leitura de Código de Barras e Categorização
Ao centralizar o código de barras na câmera (ex: produto *Piracanjuba Zero Lactose*), o protótipo identifica a nomenclatura e exibe as recomendações preliminares de conservação e higiene.

| Leitura da Embalagem | Resultado & Orientação |
| :---: | :---: |
| <img src="assets/scanner_camera.jpeg" width="250"/> | <img src="assets/scanner_resultado.jpeg" width="250"/> |

---

### 3. Assistente de IA & Restrição de Escopo (Guardrails)
Demonstração da Inteligência Artificial em ação. Quando questionada sobre assuntos fora da inspeção sanitária (ex: *"recorde de salto olímpico"*), a IA recusa a resposta e redireciona o usuário de volta à auditoria sanitária.

| Bloqueio de Assunto Alheio | Orientação Sanitária Válida |
| :---: | :---: |
| <img src="assets/ia_bloqueio.jpeg" width="250"/> | <img src="assets/ia_resposta.jpeg" width="250"/> |

---

## 🏗️ Ficha Técnica e Tecnologias Utilizadas

* **Linguagem & Framework:** Dart / Flutter
* **Backend & Autenticação:** Firebase Auth
* **Processamento de Imagem / Barcode:** `mobile_scanner` (Leitura nativa EAN-13)
* **Motor de IA Conversacional:** `google_generative_ai` (SDK Oficial Gemini)
* **Recursos de Acessibilidade (Voz):** `speech_to_text`, `record` e `flutter_tts` (Hands-Free)
* **Base de Dados Externa:** API *Open Food Facts*

---

## 🚀 Próximos Passos do Desenvolvimento (P&D)

Como evolução natural deste protótipo, o plano de trabalho prevê:
- [x] Construção da interface funcional e fluxo de navegação em Flutter.
- [x] Módulo de leitor de código de barras e filtro conversacional da IA.
- [ ] **Implementação da Arquitetura RAG (Retrieval-Augmented Generation):** Evolução da camada de regras determinísticas para busca vetorial na legislação sanitária.
- [ ] **Etapa de Alpha Testing:** Validação científica e curadoria do conteúdo gerado com supervisão especialista na RDC nº 216/2004.

---

## 🗝️ Acesso Demonstrativo para Avaliação

Para testes operacionais na build demonstrativa:
* **Usuário:** `ContaTeste`
* **Senha:** `testando`

---
© 2026 Gabriel Tupynambá. Todos os direitos reservados.
