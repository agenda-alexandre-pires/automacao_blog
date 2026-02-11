# Plano de Automação: Blog WordPress + IA + Redes Sociais

Este documento detalha o plano para criar um fluxo de automação no n8n que gera conteúdo otimizado para WordPress, LinkedIn e Instagram com aprovação via Telegram.

## 📋 Visão Geral

O objetivo é automatizar a criação de conteúdo para o público de áudio profissional, garantindo qualidade, precisão técnica (via Wikipedia) e um toque humano que não pareça gerado por IA.

**Tipo de Projeto:** BACKEND (Automação de Workflow)

## 🎯 Critérios de Sucesso

- [ ] Formulário inicial aceitando Palavras-chave, Capítulos e Quantidade de Palavras.
- [ ] Verificação de duplicidade no Google Sheets antes de iniciar a geração.
- [ ] Geração de post WordPress, textos para LinkedIn/Instagram e imagem de cabeçalho.
- [ ] Aprovação via Telegram com botões interativos e captura de motivo em caso de erro/rejeição.
- [ ] Publicação automática no WordPress após aprovação.
- [ ] Limpeza automática (excluir rascunho) em caso de rejeição.
- [ ] Loop de retorno: se rejeitado, o fluxo retorna para a IA com o "Motivo da Rejeição" para ajuste fino.

## 🛠️ Tech Stack

- **Orquestrador:** n8n
- **IA (Texto/Imagem):** OpenAI (GPT-4o para texto, DALL-E 3 para imagem) com persona "Emerson Porfa"
- **Pesquisa:** Wikipedia Tool (via nó de IA no n8n)
- **Plataformas:** WordPress (CMS), Google Sheets (Database), Telegram (Approval/Control)

## 📁 Estrutura de Arquivos Sugerida

- `/blog-automation-plan.md` (Este arquivo)
- `/prompts/` (Pasta para armazenar os prompts de referência do usuário)
- `/n8n/workflow.json` (Exportação do fluxo para backup)

## 📝 Divisão de Tarefas

### Fase 0: Infraestrutura e Versionamento (P0 - CRÍTICO)

- [ ] **Tarefa 0.1**: Inicializar repositório Git Local e criar `.gitignore`.
- [ ] **Tarefa 0.2**: Conectar ao repositório GitHub remoto.
- [ ] **Tarefa 0.3**: Definir protocolo de backup: Exportar o `workflow.json` do n8n para a pasta `./n8n/` a cada mudança significativa.

### Fase 1: Fundação e Dados (P0)

- [ ] **Tarefa 1.1**: Configurar planilha Google Sheets com colunas: `Data`, `Palavra-chave`, `Status`, `URL do Post`.
- [ ] **Tarefa 1.2**: Criar Bot no Telegram e obter API Token e Chat ID.
- [ ] **Tarefa 1.3**: Configurar Credenciais no n8n (OpenAI, WordPress, Google Sheets, Telegram).

### Fase 2: Inteligência e Geração (P1)

- [ ] **Tarefa 2.1**: Implementar `n8n Form Trigger` com os campos solicitados.
- [ ] **Tarefa 2.2**: Criar lógica de busca no Google Sheets para evitar repetição de palavras-chave.
- [ ] **Tarefa 2.3**: Configurar `AI Agent Node` no n8n com a Persona Emerson Porfa.
  - *Diretriz*: Usar gírias (micar, sobra, lama, punch, gain stage), foco no autodidata, frases curtas, sem clichês ("No mundo de hoje").
  - *Estrutura JSON*: Título curto, Slug amigável, MetaDesc (150-160 chars), Intro forte, Capítulos (HTML puro), ImagePrompt técnico.
- [ ] **Tarefa 2.4**: Integrar nó DALL-E 3 usando a "Visual Style Specification".
  - *Prompt Formula*: "Professional illustrated photography of [EQUIPMENT]... semi-realistic... no people".
- [ ] **Tarefa 2.5**: Gerar textos para redes sociais:
  - *LinkedIn*: Gancho rápido + 2-3 linhas de opinião + "Link nos comentários".
  - *Instagram*: Gancho impactante + texto curtíssimo (<60 palavras) + "Link na Bio".

### Fase 3: Postagem e Aprovação (P2)

- [ ] **Tarefa 3.1**: Criar nó WordPress para gerar o post como `draft` (Rascunho) e fazer upload da imagem.
- [ ] **Tarefa 3.2**: Configurar mensagem no Telegram enviando preview do Post + Legendas Redes Sociais.
- [ ] **Tarefa 3.3**: Implementar botões `Aprovar` (dispara publicação) e `Rejeitar` (abre prompt para digitar motivo).

### Fase 4: Finalização e Loop (P3)

- [ ] **Tarefa 4.1**: Lógica "Postar": Mudar status do WordPress para `publish` e atualizar Google Sheets (KeyWord + Status: Publicado).
- [ ] **Tarefa 4.2**: Lógica "Rejeitar":
  - Excluir post no WordPress.
  - Capturar o motivo enviado pelo Emerson.
  - Alimentar o AI Agent com o feedback para nova geração (ciclo iterativo).

## ✅ PHASE X: VERIFICAÇÃO FINAL

- [ ] Testar fluxo completo do formulário à postagem.
- [ ] Validar se o tom de voz está adequado para áudio profissional.
- [ ] Verificar segurança das credenciais.
- [ ] Confirmar que imagens estão sendo anexadas corretamente ao post.

---
**Próximo Passo:** Implementar o formulário inicial e a integração com o Google Sheets (Tarefa 1.1 e 2.1).
