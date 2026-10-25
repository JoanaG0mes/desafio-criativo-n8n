# Desafio Criativo: Planejando Automações com N8N Usando Apenas Bons Prompts

**Projeto:** Sistema Automatizado de Justificativa de Faltas e Análise de Documentos Acadêmicos com IA  
**Plataforma de Automação:** n8n  
**Objetivo:** Automatizar o atendimento à secretaria/coordenação acadêmica, analisando atestados/documentos via IA com visão computacional, registrando no sistema escolar e notificando o aluno.

---

## 🧱 Passo 1: Defina a automação desejada

**Quero criar uma automação no N8N para:**
Receber solicitações de justificativa de faltas e requerimentos acadêmicos enviados por alunos, analisar os comprovantes e atestados anexados através de IA (visão computacional), abonar/justificar as faltas diretamente no sistema acadêmico via API, registrar o histórico em planilha e notificar o aluno por e-mail com o parecer final.

* **Público ou responsável:**
  Secretaria Acadêmica, Coordenação de Curso e os próprios Alunos.

* **Resultado esperado:**
  Reduzir o tempo de resposta das solicitações de dias para minutos, eliminar a conferência manual de atestados simples, manter a planilha de controle e o sistema acadêmico 100% atualizados e fornecer retorno transparente ao aluno por e-mail.

---

## 🧱 Passo 2: Contexto e Regras

* **Ferramentas envolvidas:**
  * **Google Forms ou E-mail (IMAP / Gmail Trigger):** Ponto de entrada onde o aluno envia matrícula, justificativa e anexa o documento/imagem.
  * **Google Sheets:** Registro e rastreio de todos os chamados, status (Aprovado, Rejeitado, Em Análise Manual) e timestamps.
  * **OpenAI (GPT-4o / Vision) ou Google Gemini:** Análise visual do atestado/documento anexado (leitura de CRM do médico, datas, legibilidade, assinatura e motivo).
  * **API do Sistema Acadêmico (ex: TOTVS, Q-Acadêmico, SIGA ou ERP Educacional):** Endpoint REST para registrar a dispensa/justificativa de faltas na frequência do aluno.
  * **Gmail / SendGrid:** Envio do e-mail formal ao aluno comunicando se o pedido foi deferido ou indeferido.

* **Fluxo desejado:**
  1. **Entrada:** Receber o requerimento do aluno com matrícula, motivo da ausência e anexo do documento (foto/PDF do atestado).
  2. **Registro Inicial:** Adicionar nova linha no Google Sheets com status `"Recebido"`.
  3. **Análise por IA (Visão Computacional):**
     * Enviar a imagem do documento para o modelo multimodal de IA.
     * Extrair dados: Data do atestado, quantidade de dias de repouso, legibilidade do documento e dados do emissor (CRM/médico).
     * Validar se o período do atestado coincide com a data da falta informada pelo aluno.
  4. **Tomada de Decisão (If / Switch Node):**
     * **Caso Aprovado:** 
       1. Disparar requisição HTTP à API do Sistema Acadêmico para abonar a falta.
       2. Atualizar a planilha com status `"Aprovado / Falta Justificada"`.
       3. Enviar e-mail ao aluno confirmando a resolução e o período abonado.
     * **Caso Inválido / Ilegível / Suspeito:** 
       1. Atualizar a planilha com status `"Necessita Análise Manual"` ou `"Recusado"`.
       2. Enviar e-mail ao aluno orientando a reenviar o documento legível ou agendar comparecimento presencial.

* **Regras importantes:**
  * Documentos ilegíveis ou cortados nunca devem ser aprovados automaticamente; devem cair em rota de contingência para conferência humana.
  * O prazo limite para submissão do atestado deve ser validado (ex: até 48h após a ausência).
  * Tratar erros da API do sistema acadêmico com retentativas automáticas e notificação à equipe de TI/Secretaria se o sistema estiver fora do ar.

---

## 🧱 Passo 3: Monte o prompt final

```text
Atue como um Arquiteto de Soluções especialista em N8N e integrações com Inteligência Artificial.

Crie uma automação completa no N8N para:
Processar requerimentos de justificativa de faltas escolares, com análise visual de documentos por IA, atualização de sistema acadêmico via API, controle em planilha e retorno por e-mail ao aluno.

Público:
Secretaria Acadêmica, Coordenação e Alunos.

Ferramentas envolvidas:
- Google Forms / Webhook ou Gmail Trigger (Recebimento de requerimentos e anexos)
- Google Sheets (Controle de solicitações e histórico)
- OpenAI GPT-4o / Vision ou Google Gemini (Análise e OCR inteligente de atestados/documentos)
- HTTP Request Node (Integração com API REST do Sistema Acadêmico)
- Gmail / SendGrid Node (Comunicação de deferimento/indeferimento ao aluno)

Fluxo:
1. Receber a solicitação contendo dados do aluno (matrícula, data da falta) e imagem/PDF do comprovante.
2. Salvar o registro inicial no Google Sheets com status "Em Análise".
3. Processar a imagem com nó de IA multimodal para extrair datas, assinatura, carimbo e verificar autenticidade/legibilidade.
4. Avaliar com nó de decisão (If/Switch):
   - Se os critérios forem atendidos: chamar a API do Sistema Acadêmico via HTTP Request justificando as faltas, atualizar a linha na planilha para "Deferido" e disparar e-mail de confirmação ao aluno.
   - Se o documento for ilegível ou inválido: atualizar a planilha como "Pendente de Revisão" e notificar o aluno por e-mail com as instruções de reenvio.

Regras:
- Não aprovar automaticamente atestados sem data legível, sem assinatura/carimbo ou enviados fora do prazo regulamentar.
- Tratar exceções e erros de conexão com a API acadêmica sem interromper a execução do fluxo.

Explique quais nós do N8N devem ser utilizados, a configuração do nó de IA para visão/OCR, o payload JSON da requisição HTTP e a lógica detalhada de funcionamento do workflow.
```

---

## ☁️ Como entregar seu Desafio na DIO

1. **Google Drive:**
   * Faça upload deste arquivo `.md` no seu Google Drive.
   * Ajuste o acesso para **"Qualquer pessoa com o link"**.
   * Copie o link e envie na plataforma da DIO.

2. **GitHub:**
   * Crie um repositório (ex: `desafio-n8n-dio`).
   * Suba este arquivo com o nome `README.md`.
   * Envie o link do repositório na DIO.
