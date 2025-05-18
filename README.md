# Documentação Técnica do Sistema de Análise de Boletins de Medição
Visão Geral
O sistema de análise de boletins de medição é um aplicativo web desenvolvido em Streamlit, com integração à API Gemini 2.5 Pro do Google e processamento de arquivos PDF utilizando a biblioteca pdfplumber.
O objetivo principal do sistema é:
1.	Automatizar a verificação de medições com base em contratos fornecidos.
2.	Utilizar agentes de inteligência artificial para validação e revisão de dados financeiros.
3.	Facilitar o processo de auditoria e controle de possíveis divergências contratuais.
A aplicação foi projetada com foco em usabilidade, precisão na extração de dados e clareza nos relatórios gerados por IA.
________________________________________
Arquitetura
•	Frontend: Streamlit
•	Processamento de PDFs: pdfplumber
•	IA Generativa: Gemini 2.5 Pro via google.generativeai
•	Autenticação e Chaves: st.secrets com a variável GEMINI_API_KEY
________________________________________
Estrutura dos Dados
O sistema aceita os seguintes arquivos:
•	Um arquivo PDF contendo o boletim de medição
•	Um ou mais arquivos PDF contendo os contratos base
Os dados extraídos são estruturados em:
•	Tabelas de medição: listas tabulares com descrição, quantidade e valores
•	Preços contratuais: mapeamento entre a descrição (função ou item) e valor unitário
________________________________________
Funcionalidades
1. Upload de Arquivos
•	Upload de um arquivo PDF de medição
•	Upload de até 10 arquivos PDF contendo contratos de referência
2. Extração de Tabelas
•	Extração das tabelas página por página
•	Conversão das tabelas para texto tabular
3. Agente Validador (Gemini)
Responsável por:
•	Analisar a tabela de medição
•	Comparar os valores com os preços contratuais
•	Identificar inconsistências como:
o	Divergência de valores unitários
o	Erros de cálculo (quantidade × valor unitário)
o	Possíveis duplicidades ou indícios de superfaturamento
O agente utiliza prompt com contexto técnico-financeiro.
4. Agente Revisor (Gemini)
Responsável por:
•	Revisar a resposta do agente validador
•	Corrigir imprecisões e refinar a linguagem
•	Adicionar informações relevantes
•	Garantir clareza e precisão técnica para o usuário final
O agente utiliza prompt com contexto de revisão técnica em auditoria.
5. Geração de Relatório Final
•	As análises são organizadas por página
•	O resultado é formatado em Markdown
•	A exibição é feita dinamicamente com st.write_stream
________________________________________
Segurança
•	A chave da API Gemini é armazenada com segurança utilizando st.secrets
•	Nenhum dado carregado pelo usuário é armazenado localmente
•	O sistema é executado localmente e projetado para ambientes internos e controlados

