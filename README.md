# Documentação Técnica do Sistema de Análise de Boletins de Medição
Visão Geral
O sistema de análise de boletins de medição é um aplicativo web desenvolvido em Streamlit, com integração à API Gemini 2.5 Pro do Google e processamento de arquivos PDF utilizando a biblioteca pdfplumber.

O objetivo principal do sistema é:

Automatizar a verificação de medições com base em contratos fornecidos.

Utilizar agentes de inteligência artificial para validação e revisão de dados financeiros.

Facilitar o processo de auditoria e controle de possíveis divergências contratuais.

A aplicação foi projetada com foco em usabilidade, precisão na extração de dados e clareza nos relatórios gerados por IA.

Arquitetura
Frontend: Streamlit

Processamento de PDFs: pdfplumber

IA Generativa: Gemini 2.5 Pro via google.generativeai

Autenticação e Chaves: st.secrets com variável GEMINI_API_KEY

Estrutura dos Dados
O sistema aceita os seguintes arquivos:

Um arquivo PDF contendo o boletim de medição.

Um ou mais arquivos PDF contendo os contratos base.

Os dados extraídos são estruturados em:

Tabelas de medição: listas tabulares com descrição, quantidade e valores.

Preços contratuais: mapeamento entre a descrição (função ou item) e o valor unitário contratado.

Funcionalidades
1. Upload de Arquivos
Upload de um arquivo PDF de medição.

Upload de até 10 arquivos PDF contendo os contratos.

2. Extração de Tabelas
Extração das tabelas de medição por página.

Conversão das tabelas para texto tabular estruturado.

3. Agente Validador (Gemini)
Responsável por:

Analisar a tabela de medição.

Comparar os valores com os preços contratuais.

Identificar inconsistências como:

Divergência nos valores unitários.

Cálculos incorretos (quantidade × valor unitário).

Possíveis duplicidades ou indícios de superfaturamento.

Utiliza prompt com contexto técnico financeiro.

4. Agente Revisor (Gemini)
Responsável por:

Revisar a análise gerada pelo agente validador.

Corrigir imprecisões, adicionar informações relevantes e refinar a linguagem.

Assegurar precisão técnica e clareza na comunicação com o usuário final.

Utiliza prompt com contexto de revisão técnica em auditoria.

5. Geração de Relatório Final
As análises são organizadas por página.

O resultado final é formatado em Markdown.

A exibição é feita de forma dinâmica utilizando st.write_stream.

Segurança
A chave da API Gemini é armazenada com segurança em st.secrets.

Nenhum dado enviado pelo usuário é armazenado localmente.

O sistema é projetado para execução local segura, adequado para ambientes controlados.
