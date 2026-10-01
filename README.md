# Análise do Mercado de Ações

Análise exploratória em Jupyter Notebook de cinco ações (IBM, Microsoft, Tesla, Oracle e Walmart) ao longo de um ano de pregões, comparando desempenho, risco, correlação e volume negociado.

## Conteúdo do projeto

```
.
├── analise_stockmarket.ipynb   # Notebook com toda a análise
├── StockMarket.xlsx            # Base de dados
└── README.md
```

## Base de dados

O arquivo `StockMarket.xlsx` possui uma aba (`StockMarket`) com 1.260 linhas e 7 colunas:

| Coluna  | Descrição                                   |
|---------|---------------------------------------------|
| Empresa | Nome da empresa                             |
| Data    | Data do pregão (texto no formato mm/dd/aaaa) |
| Close   | Preço de fechamento (US$)                   |
| Volume  | Quantidade de ações negociadas              |
| Open    | Preço de abertura (US$)                     |
| High    | Maior preço do dia (US$)                    |
| Low     | Menor preço do dia (US$)                    |

Cobertura: 5 empresas, 252 pregões cada, de 23/02/2022 a 23/02/2023. Não há valores nulos nem registros duplicados (Empresa + Data).

## Como executar

### 1. Pré-requisitos

- Python 3.9 ou superior
- Visual Studio Code com a extensão **Jupyter** (e a extensão Python)

### 2. Instalar as dependências

```bash
pip install pandas numpy matplotlib seaborn openpyxl ipykernel
```

Recomenda-se usar um ambiente virtual:

```bash
python -m venv .venv
source .venv/bin/activate      # Linux/macOS
.venv\Scripts\activate         # Windows
```

### 3. Abrir e rodar no VS Code

1. Deixe o `StockMarket.xlsx` na mesma pasta do notebook.
2. Abra `analise_stockmarket.ipynb` no VS Code.
3. Selecione o kernel Python do ambiente onde instalou as dependências (canto superior direito).
4. Clique em **Run All**.

Se o arquivo estiver em outra pasta, ajuste a variável `ARQUIVO` na primeira célula de código.

## Configuração

Na primeira célula de código há duas variáveis:

| Variável        | Padrão              | Função                                                         |
|-----------------|---------------------|----------------------------------------------------------------|
| `ARQUIVO`       | `StockMarket.xlsx`  | Caminho da planilha                                            |
| `EMPRESA_FOCO`  | `Tesla`             | Empresa usada nas médias móveis e nas Bandas de Bollinger      |

Valores aceitos para `EMPRESA_FOCO`: `IBM`, `Microsoft`, `Tesla`, `Oracle`, `Walmart`.

## O que o notebook faz

1. **Carga e limpeza**: converte as datas, ordena os dados e verifica nulos, duplicados e consistência entre High, Low, Open e Close.
2. **Visão geral**: estatísticas descritivas de preço e volume por empresa.
3. **Evolução de preços**: preço de fechamento, desempenho relativo em base 100 e faixa diária Low-High por empresa.
4. **Retornos e risco**: retorno acumulado, volatilidade, melhor e pior dia, drawdown, distribuição dos retornos, volatilidade móvel e retorno mensal.
5. **Correlação**: mapa de calor e gráfico de dispersão dos retornos diários.
6. **Médias móveis**: MM20 e MM50 com cruzamentos de alta e baixa, e Bandas de Bollinger.
7. **Volume**: média diária, evolução e relação entre volume e tamanho da variação de preço.
8. **Resumo comparativo**: tabela única com as principais métricas e conclusões geradas automaticamente.

## Resultados da execução

| Empresa   | Retorno acumulado | Volatilidade anualizada | Drawdown máximo |
|-----------|------------------:|------------------------:|----------------:|
| Oracle    |            +22,2% |                   29,9% |          -27,6% |
| IBM       |             +7,1% |                   23,6% |          -17,7% |
| Walmart   |             +5,2% |                   26,6% |          -26,0% |
| Microsoft |             -9,1% |                   35,7% |          -32,1% |
| Tesla     |            -20,7% |                   67,6% |          -71,7% |

Em resumo: a Oracle teve o melhor desempenho do período, a IBM foi a menos volátil e a Tesla combinou o pior retorno com a maior volatilidade e a maior queda desde o pico.

## Metodologia

- **Retorno diário**: variação percentual do preço de fechamento entre pregões consecutivos.
- **Retorno acumulado**: composição dos retornos diários ao longo de todo o período.
- **Volatilidade anualizada**: desvio padrão dos retornos diários multiplicado pela raiz de 252 (dias úteis no ano).
- **Drawdown**: queda percentual do preço em relação ao maior pico anterior; o drawdown máximo é o pior valor da série.
- **Retorno/Risco**: retorno médio anualizado dividido pela volatilidade anualizada, sem taxa livre de risco (não é o índice de Sharpe completo).
- **Médias móveis**: janelas de 20 e 50 pregões sobre o preço de fechamento.
- **Bandas de Bollinger**: média móvel de 20 pregões mais e menos 2 desvios padrão.
- **Amplitude intradiária**: (High - Low) / Open.

## Limitações

- O período cobre apenas um ano e cinco empresas, então os resultados não permitem generalizar para o mercado como um todo.
- Desempenho passado não garante resultados futuros. Este projeto tem finalidade educacional e não constitui recomendação de investimento.

## Tecnologias

Python, pandas, NumPy, Matplotlib, Seaborn e Jupyter.
