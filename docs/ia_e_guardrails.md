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
               │ GenerativeModel             │
               │ (Gemini 2.5 Flash API)       │
               │                              │
               │ SystemInstruction:           │
               │  └── AppPrompts.inspetor...  │
               └──────────────────────────────┘

📜 Instrução de Sistema (System Instruction & Persona)
A orquestração do modelo é regida pelo arquivo lib/core/constants/prompts.dart via Content.system(AppPrompts.inspetorSystemPrompt). A instrução define a persona do Inspetor SafeFood como um auditor sênior em vigilância sanitária focado estritamente na RDC nº 216/2004 (ANVISA).

Matriz de Validação Obrigatória (Checklist Mental do LLM):
Higiene dos Manipuladores: Lavagem de mãos, uniformização, ausência de adornos e uso de rede capilar.

Controle Vetorial e de Pragas: Telamento de aberturas, ralos sifonados e prevenção de vetores.

Higienização Operacional: Sanitização de superfícies e uso de saneantes regularizados.

Armazenamento e Rotulagem: Organização sob refrigeração e controle rígido de validade.

Manejo de Resíduos: Lixeiras com acionamento não manual (pedal) e frequência de descarte.

Controle Térmico: Monitoramento de temperatura em cadeia de frio e quente.

Diretrizes de Comportamento e Tom de Voz:
Tom Educativo: Parceria pedagógica em vez de postura punitiva.

Respostas Concisas: Restrição estrita a no máximo duas frases por intervenção, adequando-se ao ritmo ágil de cozinhas profissionais.

Agrupamento Inteligente de Respostas: Se o usuário responde sobre dois tópicos simultaneamente (ex: limpeza e validade), o modelo marca ambos como validados sem duplicar perguntas.

🛡️ Mecanismos de Segurança e Controle de Escopo (Guardrails)
Para evitar desvios temáticos e alucinações comuns em modelos abertos, o sistema utiliza retenção de contexto contínua via ChatSession:

Detecção de Fuga de Escopo: O modelo valida se o insumo recebido pertence ao domínio da segurança alimentar.

Manutenção do Bloqueio: Caso o usuário introduza assuntos alheios (ex: esportes ou notícias), o assistente responde de forma amigável, mas recusa o aprofundamento no tema alheio e reorienta a pauta imediatamente para a auditoria sanitária.

Persistência de Diálogo: A sessão (_chat = _model.startChat()) preserva a memória das checagens já realizadas durante toda a execução.

🎙️ Processamento Multimodal de Áudio & Acessibilidade
O aplicativo implementa escuta e resposta por voz direta, eliminando a dependência de digitação manual:

Captura Multimodal (Entrada):

O áudio é gravado via AudioRecorder em formato .m4a e convertido em array de bytes em memória.

Os bytes são enviados diretamente ao SDK do Gemini encapsulados em uma estrutura multimodal DataPart('audio/m4a', bytes) combinada com a instrução TextPart.

Síntese de Fala / Text-To-Speech (Saída):

A resposta textual retornada pelo Gemini é repassada imediatamente para a engine nativa FlutterTts.

A reprodução em áudio ocorre em português (pt-BR) com velocidade ajustada (0.6) para clareza em ambientes ruidosos.

⚙️ Ficha Técnica do Módulo ChatIAScreen.dart
Modelo Ativo: gemini-2.5-flash

SDK: google_generative_ai (Pacote oficial do Google para Flutter)

Gerenciamento de Mídia: record (gravação), path_provider (arquivos temporários), flutter_tts (síntese)

Arquivos do Módulo: lib/features/chat_ia/chat_ia_screen.dart e lib/core/constants/prompts.dart
