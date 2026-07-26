# 🏗️ Arquitetura de Software e Engenharia da Aplicação

Este documento descreve a estrutura organizacional do código-fonte e as decisões de arquitetura adotadas no protótipo do **SafeFood**.

---

## 📌 Padrão de Arquitetura (Feature-First)

A aplicação utiliza uma abordagem **Feature-First Architecture**, onde o código é segmentado por funcionalidades/módulos independentes. Essa separação garante alta coesão, baixo acoplamento e facilita a evolução contínua da base de código.

```text
lib/
│── firebase_options.dart      # Configurações do projeto no Firebase
│── main.dart                  # Ponto de entrada do aplicativo
│
├── core/                      # Módulo central e utilitários globais
│   ├── auth_gate.dart         # Controle de estado de autenticação (Redirecionamento)
│   ├── routes.dart            # Mapeamento de rotas e navegação
│   ├── theme.dart             # Identidade visual e estilização global
│   └── constants/
│       └── prompts.dart       # Instruções de sistema e restrições da IA
│
├── features/                  # Módulos funcionais da aplicação
│   ├── auth/                  # Módulo de autenticação (Welcome, Login, Registro)
│   ├── chat_ia/               # Interface conversacional com LLM (Gemini)
│   ├── checklist/             # Autoavaliação objetiva da RDC nº 216/2004
│   ├── scanner/               # Módulo de leitura ótica (EAN-13) e API OpenFoodFacts
│   ├── home/                  # Painel de controle e navegação do usuário
│   └── historico/             # Módulo preparado para persistência de dados
│
├── layout/
│   └── main_screen.dart       # Estrutura base de navegação e BottomNavigationBar
│
├── services/
│   └── auth_service.dart      # Camada de comunicação com o Firebase Auth
│
└── widgets/
    └── custom_button.dart     # Componentes visuais reutilizáveis de UI
