# 🤖 Chatbot de Análise de Dados com n8n, Supabase e IA

Este projeto demonstra como construir um chatbot inteligente que responde a perguntas em **linguagem natural (português)** sobre dados complexos, combinando automação low-code, IA generativa e banco de dados relacional.

---

## 🔍 Visão Geral

A proposta é simples e poderosa: permitir que **qualquer pessoa, mesmo sem conhecimento técnico**, extraia insights relevantes de um banco de dados de **notas fiscais** apenas perguntando, como em:

- “Qual foi o faturamento total em janeiro?”
- “Liste os 5 produtos mais vendidos.”
- “Quantas notas foram emitidas para o estado de São Paulo?”

Sem precisar escrever SQL. Apenas **perguntas naturais.**

---

## 🧠 Arquitetura e Fluxo

A solução é construída sobre um fluxo do **n8n**, com dois LLMs (usando Google Gemini) em funções específicas:

1. **Especialista em SQL** – Traduz perguntas em queries.
2. **Comunicador Amigável** – Interpreta os dados e responde ao usuário.
>
> **📌 Veja o fluxo completo abaixo:**  
>![image](https://github.com/user-attachments/assets/72daba66-8d6a-477e-a47b-8e5b68812dd2)


---

## ⚙️ Etapas do Funcionamento

### 1. 💬 Trigger: Recebe a pergunta
O usuário envia uma mensagem para o chatbot via webhook.

### 2. 🧠 Geração da Query SQL
O primeiro LLM interpreta a pergunta e gera a query SQL com base em:
- Schema da base
- Regras de negócio
- Tradução de termos naturais

### 3. 🧼 Limpeza e Execução
Um nó em JavaScript limpa a query (caso venha com Markdown) e o n8n a executa no banco **PostgreSQL** via **Supabase**.

### 4. 🗣️ Resposta Inteligente
O segundo LLM recebe os dados brutos e responde em linguagem natural, analisando contexto e resultado da query.

---

## 🗄️ Base de Dados: Supabase + PostgreSQL

A base está hospedada no [Supabase](https://supabase.com/), com milhares de registros reais de **notas fiscais**.

> **📌 Exemplo de estrutura da tabela:**  
![image](https://github.com/user-attachments/assets/2ab13a3e-1d72-4a7d-ad09-ff82d5db5cb0)


---

## 🚀 Como Usar Este Projeto

### ✅ Pré-requisitos

- Uma instância do **n8n** (cloud ou self-hosted)  
- Conta no **Supabase** com PostgreSQL  
- API Key para o **Google Gemini** (ou outro LLM)

### 📥 Instalação

```bash
git clone https://github.com/backhenry/Chatbot-Analise-Dados-n8n-Supabase.git
```

### 🔄 Importar o Workflow  
No painel do **n8n**, importe o arquivo `workflow.json` incluído neste repositório.

### 🏗️ Configurar o Banco de Dados  
Crie uma tabela no **Supabase** com o schema correspondente.  
Importe seus próprios dados ou use os dados de exemplo.

### 🔐 Configurar Credenciais  
No nó **PostgreSQL**, configure a conexão com seu Supabase.  
Nos nós **Gemini**, insira sua chave de API.

### 🛠️ Ajustar Prompts  
Revise os prompts dos nós **LLM** para garantir que eles reflitam o seu schema e lógica de negócio.

### ▶️ Rodar o Chatbot  
Ative o workflow no **n8n**.  
Use o endpoint do **webhook** para conversar com seu chatbot.
