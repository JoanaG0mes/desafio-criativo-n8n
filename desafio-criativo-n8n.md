# Desafio Criativo: Planejando Automações com N8N Usando Apenas Bons Prompts

Projeto desenvolvido para o desafio da **DIO (Digital Innovation One)**, com foco em estruturar um prompt eficiente, contextualizado e completo para orientar a criação de workflows no **n8n**.

---

## 🧱 Passo 1: Definição da Automação

**Processo a ser automatizado:**
Quero criar uma automação no N8N para **qualificação, enriquecimento e distribuição automática de novos leads recebidos via webhook/formulário**.

* **Público ou responsável:**  
  Equipe de Vendas (SDRs/Closers) e Time de Marketing.

* **Resultado esperado:**  
  Capturar o lead em tempo real, enriquecer os dados corporativos, aplicar critérios de qualificação (lead scoring/fit), rotear e cadastrar no CRM (HubSpot/Pipedrive) e alertar imediatamente o canal comercial no Slack com ações rápidas.

---

## 🧱 Passo 2: Contexto e Regras

* **Ferramentas envolvidas:**
  * **Webhook / Typeform / Google Forms** (gatilho de entrada do lead)
  * **Clearbit / Hunter API ou HTTP Request** (enriquecimento de domínio/empresa)
  * **CRM (HubSpot ou Pipedrive)** (criação e atualização de contato/negócio)
  * **Slack** (notificação dinâmica em canal interno)
  * **SendGrid / Gmail** (e-mail automático de boas-vindas)

* **Fluxo desejado:**
  1. **Disparo:** Receber os dados do lead via Webhook ou acionador do formulário.
  2. **Validação:** Verificar se o e-mail informado é corporativo e possui formato válido.
  3. **Enriquecimento:** Realizar consulta via HTTP Request para buscar porte e setor da empresa.
  4. **Score & Roteamento (IF / Switch):**
     * Se for *Lead Qualificado* (ex: porte > 50 funcionários ou interesse prioritário): criar contato + oportunidade no CRM e enviar alerta de alta prioridade no canal `#vendas-hot-leads` do Slack.
     * Se for *Lead em Nutrição*: cadastrar apenas como contato no CRM e adicionar à régua de marketing.
  5. **Notificação ao Lead:** Disparar e-mail automático personalizado de boas-vindas com o material solicitado.
  6. **Tratamento de Erros:** Encaminhar qualquer falha ou dado corrompido para um canal `#alertas-ops`.

* **Regras importantes:**
  * Ignorar ou descartar submissões que não possuam e-mail válido ou com domínios temporários/descartáveis.
  * Realizar dedup (evitar duplicidade no CRM): pesquisar contato antes de criar um novo.
  * Timeout de 5 segundos na requisição de enriquecimento para não travar a esteira.

---

## 🧱 Passo 3: Prompt Final Estruturado

Copie o prompt abaixo para utilizá-lo diretamente no ChatGPT, Claude, Gemini ou qualquer assistente de IA:

```text
Atue como um Arquiteto de Soluções especialista em automações corporativas no N8N.

Crie uma automação completa e robusta para:
Qualificação, enriquecimento e roteamento inteligente de novos leads recebidos via formulário.

Público-alvo / Beneficiários:
Equipe Comercial (SDRs/Vendedores) e Operações de Marketing.

Ferramentas envolvidas:
- Webhook / Typeform (Gatilho)
- HTTP Request (API de enriquecimento)
- Hubspot ou Pipedrive (CRM)
- Slack (Comunicação interna)
- Gmail / SendGrid (Comunicação externa)

Fluxo detalhado:
1. Receber payload via Webhook ou Form Trigger.
2. Limpar e padronizar campos (Code node ou Edit Fields).
3. Validar se o e-mail é válido e corporativo (If node).
4. Buscar informações complementares da empresa via HTTP Request.
5. Calcular pontuação/fit do lead (Switch node):
   - Alta prioridade: Criar Deal no CRM e enviar card rico com botões no Slack (#vendas-hot).
   - Baixa prioridade: Salvar contato no CRM e acionar régua de nutrição.
6. Enviar e-mail de confirmação dinâmico com template HTML.

Regras e restrições:
- Verificar duplicidade no CRM antes de inserir.
- Ignorar submissões sem campos obrigatórios (Nome e E-mail).
- Tratar falhas de requisição externa com rota de fallback sem quebrar a execução.

Entrega esperada:
1. Lista dos nós nativos do N8N recomendados para cada etapa.
2. Explicação da arquitetura e fluxo de dados entre os nós.
3. Exemplo de estrutura do JSON/Workflow para importação direta no N8N.
```

---

## 💡 Como Usar e Submeter na DIO

1. **Repositório GitHub:**
   * Crie ou utilize um repositório público (ex: `desafios-n8n-prompts`).
   * Adicione este arquivo como `README.md` ou `desafio-n8n-prompt.md`.
   * Copie o link da página do GitHub e envie na plataforma da DIO.

2. **Google Drive:**
   * Salve este conteúdo em um arquivo de texto ou Google Docs.
   * Configure o compartilhamento para *"Qualquer pessoa com o link"*.
   * Cole o link na página de submissão da DIO.
