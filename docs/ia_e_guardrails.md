# 🤖 Engenharia de Prompt, Multimodalidade e Guardrails do LLM

Este documento detalha a arquitetura do módulo **Inspetor IA (`ChatIAScreen.dart`)**, responsável por conduzir auditorias sanitárias interativas alimentadas pelo modelo de linguagem **Google Gemini 2.5 Flash** (`google_generative_ai`).

---

## 🏗️ Arquitetura do Módulo Conversacional

O módulo combina processamento de linguagem natural (PLN), multimodalidade por áudio em tempo real e síntese de voz (TTS) para permitir a operação *Hands-Free* (sem uso continuado das mãos), essencial para ambientes de manipulação de alimentos.

```text
  ┌─────────────────────────────────────────────────────────┐
  │                    Usuário (App)                        │
  └───────────┬─────────────────────────────────▲───────────┘
              │                                 │
   [Texto ou Áudio .m4a]               [Resposta em Áudio (TTS)]
              │                                 │
              ▼                                 │
  ┌──────────────────────┐             ┌────────────────────┐
  │ AudioRecorder        │             │ FlutterTTS         │
  │ (Record/PathProvider)│             │ (pt-BR / Rate 0.6) │
  └───────────┬──────────┘             └────────▲───────────┘
              │                                 │
        [DataPart Bytes]                 [Text Response]
              │                                 │
              └───────────────┐ ┌───────────────┘
                              ▼ │
               ┌──────────────────────────────┐
               │ GenerativeModel              │
               │ (Gemini 2.5 Flash API)       │
               │                              │
               │ SystemInstruction:           │
               │  └── AppPrompts.inspetor...  │
               └──────────────────────────────┘
```

---

## 📜 Instrução de Sistema (System Instruction & Persona)

A orquestração do modelo é regida pelo arquivo **`lib/core/constants/prompts.dart`**, por meio de `Content.system(AppPrompts.inspetorSystemPrompt)`. Essa instrução define a persona do **Inspetor SafeFood** como um auditor sênior em vigilância sanitária, especializado exclusivamente na **RDC nº 216/2004 (ANVISA)**.

### ✅ Matriz de Validação Obrigatória (Checklist Mental do LLM)

Durante toda a conversa, o modelo verifica sistematicamente os seguintes eixos sanitários:

- **Higiene dos Manipuladores**
  - Lavagem correta das mãos;
  - Uniformização adequada;
  - Ausência de adornos;
  - Uso de rede capilar.

- **Controle Vetorial e de Pragas**
  - Telamento de aberturas;
  - Ralos sifonados;
  - Medidas preventivas contra vetores.

- **Higienização Operacional**
  - Sanitização de superfícies;
  - Utilização de saneantes regularizados.

- **Armazenamento e Rotulagem**
  - Organização sob refrigeração;
  - Controle rigoroso da validade dos produtos.

- **Manejo de Resíduos**
  - Lixeiras com acionamento não manual (pedal);
  - Frequência adequada de descarte.

- **Controle Térmico**
  - Monitoramento da cadeia de frio;
  - Monitoramento da cadeia quente.

### 🗣️ Diretrizes de Comportamento

O comportamento conversacional do modelo segue regras explícitas definidas na *System Instruction*:

- **Tom educativo**, privilegiando orientação e parceria em vez de postura punitiva;
- **Respostas concisas**, limitadas a no máximo duas frases por interação;
- **Agrupamento inteligente de respostas**, permitindo validar múltiplos requisitos quando o usuário responde sobre mais de um tópico simultaneamente.

---

## 🛡️ Mecanismos de Segurança e Controle de Escopo (Guardrails)

Para reduzir alucinações e impedir desvios temáticos, o sistema utiliza retenção contínua de contexto através da classe `ChatSession`.

### 🔒 Controle de Escopo

O modelo verifica continuamente se cada mensagem recebida pertence ao domínio da segurança dos alimentos.

Caso o usuário introduza assuntos externos (como esportes, notícias ou política), o assistente:

- responde de forma cordial;
- informa que está restrito ao domínio sanitário;
- redireciona imediatamente a conversa para a auditoria de alimentos.

### 🧠 Persistência de Contexto

A sessão iniciada por:

```dart
_chat = _model.startChat();
```

mantém a memória de toda a auditoria durante a execução, evitando repetição de perguntas já respondidas e preservando o estado da inspeção.

---

## 🎙️ Processamento Multimodal de Áudio e Acessibilidade

O módulo implementa interação completamente por voz, reduzindo a necessidade de digitação durante inspeções sanitárias.

### 🎤 Entrada por Áudio

O fluxo de captura multimodal ocorre da seguinte forma:

1. O áudio é gravado utilizando **AudioRecorder** em formato `.m4a`;
2. O arquivo é convertido para um vetor de bytes em memória;
3. Os bytes são enviados ao Gemini através de:

```dart
DataPart('audio/m4a', bytes)
```

4. O `DataPart` é combinado com um `TextPart`, permitindo que o modelo interprete simultaneamente a entrada de voz e a instrução textual.

### 🔊 Síntese de Voz (Text-to-Speech)

Após a geração da resposta:

- o texto é encaminhado automaticamente ao **FlutterTts**;
- a síntese é realizada em **Português (pt-BR)**;
- a velocidade de reprodução é configurada para **0.6**, favorecendo inteligibilidade em ambientes ruidosos.

---

## ⚙️ Ficha Técnica do Módulo (`ChatIAScreen.dart`)

| Componente | Implementação |
|------------|---------------|
| **Modelo LLM** | Gemini 2.5 Flash |
| **SDK** | `google_generative_ai` |
| **Gravação de Áudio** | `record` |
| **Arquivos Temporários** | `path_provider` |
| **Text-to-Speech** | `flutter_tts` |
| **Tela Principal** | `lib/features/chat_ia/chat_ia_screen.dart` |
| **Prompt de Sistema** | `lib/core/constants/prompts.dart` |

---

<p align="center">
© 2026 <strong>Gabriel Tupynambá</strong>. Todos os direitos reservados.
</p>
