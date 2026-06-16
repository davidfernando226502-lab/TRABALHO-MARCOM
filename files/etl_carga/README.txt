============================================================
  Projeto Integrador I — Chikungunya SINAN 2026
  UniFAJ / UniMAX — Curso de Inteligência Artificial
============================================================

DESCRIÇÃO
---------
Pipeline de dados que carrega notificações de Chikungunya do
SINAN 2026 em um banco MySQL e gera um dashboard HTML interativo
com KPIs, gráficos e tabela por UF.

FONTE DOS DADOS
---------------
Portal: https://dados.gov.br
Dataset: SINAN — Chikungunya (agravo A920)
Ano: 2026 | Registros: ~83.668
Formato original: CSV (separador vírgula, encoding latin-1)

ESTRUTURA DO PROJETO
--------------------
tc_projeto_integrador/
  dados/
    raw/          ← coloque o CSV original aqui (CHIKBR26.csv)
    clean/        ← CSVs tratados (gerado pelo ETL se necessário)
  src/
    etl_carga.py          ← Etapa 1: ETL
    gera_dashboard.py     ← Etapa 2: Dashboard
  output/
    dashboard.html        ← resultado final (gerado pelo script)
  README.txt
  requirements.txt

PRÉ-REQUISITOS
--------------
- Python 3.8+
- MySQL 8.0+ rodando localmente
- Pacotes Python (instale com o comando abaixo):

    pip install mysql-connector-python pandas

COMO RODAR
----------
1. Baixe o CSV do SINAN em dados.gov.br e salve em dados/raw/CHIKBR26.csv

2. Crie o banco no MySQL (só na primeira vez):
     mysql -u root -p
     > CREATE DATABASE projeto_chikungunya;
     > EXIT;

3. Edite DB_CONFIG em etl_carga.py com sua senha do MySQL.

4. Execute o ETL:
     python src/etl_carga.py

5. Edite DB_CONFIG em gera_dashboard.py com sua senha do MySQL.

6. Gere o dashboard:
     python src/gera_dashboard.py

7. Abra output/dashboard.html no navegador (Chrome, Firefox, Edge).

VALIDAÇÃO RÁPIDA NO MYSQL
--------------------------
  SELECT COUNT(*) FROM notificacoes_chikungunya;
  -- Esperado: ~83.668

ERROS COMUNS
------------
- "Unknown database": rode CREATE DATABASE primeiro (passo 2)
- Encoding quebrado: altere CSV_ENCODING para 'utf-8' em etl_carga.py
- Separador errado: o script detecta automaticamente ; ou ,
- HTML vazio: verifique se o ETL foi executado antes do dashboard

============================================================
