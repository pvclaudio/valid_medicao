# Documentação Técnica do Sistema de Análise de Boletins de Medição
Visão Geral
O sistema de análise de boletins de medição é um aplicativo web desenvolvido em Streamlit, com integração à API Gemini 2.5 Pro do Google e processamento de arquivos PDF com pdfplumber. Seu objetivo é:


1) Automatizar a verificação de medições com base em contratos fornecidos.

2) Utilizar agentes de IA para validação e revisão de dados financeiros.

3) Facilitar o processo de auditoria e controle de possíveis divergências contratuais.


A aplicação foi projetada com foco em usabilidade, precisão na extração de dados e clareza nos relatórios gerados por IA.

Arquitetura

**Frontend:** Streamlit
**Processamento de PDFs:** pdfplumber
**IA Generativa:** Gemini 2.5 Pro via google.generativeai
**Autenticação e Chaves:** st.secrets para a GEMINI_API_KEY

**Estrutura dos Dados**

O sistema aceita:

Um PDF com o boletim de medição

Um ou mais PDFs com os contratos base

Os dados extraídos são estruturados como:

Tabelas de medição: listas tabulares com descrição, quantidade e valores.

Preços contratuais: mapeamento entre a descrição (função ou item) e valor unitário.

Funcionalidades
1. Upload de Arquivos
Upload de:

PDF de medição

De 1 a 10 contratos de referência

Leitura automática e extração das tabelas com pdfplumber.

2. Extração de Tabelas
As tabelas são extraídas página por página.

Cada tabela é convertida em texto tabular para ser analisada pela IA.

É gerada uma lista contendo:

Número da página

Conteúdo tabular extraído

3. Agente Validador (Gemini)
Responsável por:

Analisar a tabela da medição.

Comparar os valores com os do contrato.

Detectar inconsistências como:

Valores unitários divergentes.

Erros nos totais (quantidade × valor unitário).

Itens repetidos ou possíveis fraudes.

Prompt com contexto técnico financeiro.

4. Agente Revisor (Gemini)
Responsável por:

Revisar a resposta do agente validador.

Corrigir erros, adicionar informações e refinar a linguagem.

Garantir clareza e precisão para o usuário final.

Prompt com contexto de revisor técnico em auditoria.

5. Geração de Relatório Final
O sistema concatena as análises por página em blocos de resposta formatados com Markdown.

A resposta final é apresentada via st.write_stream, simulando um fluxo dinâmico de geração.

Segurança
A chave da API Gemini é armazenada de forma segura via st.secrets.

O sistema não armazena localmente os dados carregados.

Execução local segura, ideal para uso interno ou em ambiente controlado.

Considerações Finais
Este sistema é modular e pode ser expandido com:

Armazenamento em Google Drive ou banco de dados.

Dashboard de medições anteriores.

Logs e histórico de análises realizadas.

Integração com ferramentas de workflow como Zapier ou Airflow.

O uso de múltiplos agentes (validador e revisor) melhora significativamente a confiabilidade e a qualidade das análises.
