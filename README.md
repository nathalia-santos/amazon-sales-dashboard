# 📊 Amazon Sales Dashboard

Dashboard de análise de vendas construído a partir de dados reais do marketplace Amazon India, com foco em visualização de desempenho de produtos, distribuição de preços e engajamento de clientes.

---

## Sobre o projeto

O objetivo deste projeto é transformar dados brutos de produtos Amazon em informações visuais claras e úteis, permitindo uma análise eficaz do desempenho de vendas e a tomada de decisões baseadas em dados.

O resultado final é um arquivo Excel (`.xlsx`) com quatro abas estruturadas, formatação profissional e formatação condicional por escala de cores.

---

## Dados utilizados

**Arquivo fonte:** `amazon.csv`  
**Origem:** Amazon India Product Dataset (Kaggle)  
**Registros:** 1.465 produtos  
**Colunas originais:**

| Coluna | Descrição |
|---|---|
| `product_id` | Identificador único do produto |
| `product_name` | Nome completo do produto |
| `category` | Hierarquia de categorias separada por `\|` |
| `discounted_price` | Preço com desconto (em ₹) |
| `actual_price` | Preço original (em ₹) |
| `discount_percentage` | Percentual de desconto aplicado |
| `rating` | Nota média do produto (0–5) |
| `rating_count` | Número total de avaliações |
| `about_product` | Descrição e especificações |
| `user_id` | IDs dos usuários que avaliaram |
| `user_name` | Nomes dos avaliadores |
| `review_id` | IDs das avaliações |
| `review_title` | Títulos das avaliações |
| `review_content` | Texto das avaliações |
| `img_link` | URL da imagem do produto |
| `product_link` | URL da página do produto |

**Categorias principais presentes no dataset:**

- Electronics (526 produtos)
- Computers & Accessories (453 produtos)
- Home & Kitchen (448 produtos)
- Office Products (31 produtos)
- Outros: Musical Instruments, Home Improvement, Toys & Games, Car & Motorbike, Health & Personal Care

---

## Estrutura do dashboard (arquivo .xlsx)

### Aba 1 — Dashboard
Visão executiva com os principais indicadores do catálogo:

- **KPIs:** total de produtos, total de avaliações, rating médio e economia média por produto
- **Resumo por categoria:** quantidade de produtos, avaliações, rating médio e desconto médio
- **Distribuição de descontos:** faixas consolidadas por perfil (Baixo / Moderado / Alto / Agressivo / Liquidação)
- **Rating médio por faixa de desconto:** correlação entre nível de desconto e satisfação dos clientes

### Aba 2 — Top 20 Produtos
Ranking dos 20 produtos com maior volume de avaliações, contendo preço, desconto, rating e economia. Inclui barra de dados inline na coluna de avaliações e escala de cores no rating.

### Aba 3 — Dados Completos
Todos os 1.465 produtos com campos limpos e padronizados: ID, nome, categoria, subcategoria, preços, desconto, rating, número de avaliações e economia calculada. Escala de cores aplicada na coluna de rating.

### Aba 4 — Análise por Categoria
Tabela agregada por categoria com médias de rating, desconto, preço e economia, além de linha de totais gerais. Formatação condicional nas colunas de rating e desconto.

---

## Principais métricas extraídas

| Métrica | Valor |
|---|---|
| Total de produtos | 1.465 |
| Total de avaliações | 26,8 milhões |
| Rating médio geral | 4,09 ★ |
| Preço médio original | ₹ 5.445 |
| Preço médio com desconto | ₹ 3.125 |
| Economia média por produto | ₹ 2.320 |
| Desconto médio | 48% |
| Produtos com desconto acima de 50% | 759 (52% do catálogo) |

---

## Instruções para reprodução

### Pré-requisitos

- Python 3.8 ou superior
- Bibliotecas: `openpyxl`, `pandas` (opcional, para análise)

Instale as dependências com:

```bash
pip install openpyxl pandas
```

### Passo a passo

**1. acesse o arquivo xlsx localizado na pasta amazon_dashboard**

```
amazon_dashboard/
├── amazon_sales_dashboard.xlsx
└── README.md
```

## Lógica de tratamento dos dados

O script realiza as seguintes transformações antes de gerar o Excel:

- **Limpeza de preços:** remoção do símbolo `₹` e vírgulas, conversão para `float`
- **Limpeza de avaliações:** remoção de vírgulas em números como `24,269`, conversão para `int`
- **Limpeza de desconto:** remoção do caractere `%`, conversão para decimal (ex: `64%` → `0.64`)
- **Extração de categoria:** split pelo delimitador `|`, capturando nível 0 (categoria principal) e nível 1 (subcategoria)
- **Cálculo de economia:** `actual_price - discounted_price` para cada produto
- **Consolidação de faixas de desconto:** agrupamento por perfil de desconto para reduzir granularidade na visualização

---

## Insights principais

- **Electronics** domina em volume de avaliações (15,8M), indicando maior engajamento
- **Computers & Accessories** tem o maior desconto médio do catálogo (55%)
- **Office Products** tem o melhor rating médio (4,31 ★) apesar de menor volume
- A faixa de desconto mais comum é **40%–70%**, concentrando 728 produtos (50% do catálogo)
- Existe uma leve correlação negativa entre desconto e rating: produtos com 80% de desconto têm rating médio de 4,01 vs. 4,21 para produtos sem desconto — diferença de 0,20 pontos

---

## Tecnologias utilizadas

| Tecnologia | Uso |
|---|---|
| Python 3 | Processamento e geração do arquivo |
| openpyxl | Criação e formatação do Excel |
| csv (stdlib) | Leitura do arquivo de dados |
| re (stdlib) | Limpeza e parsing de strings |

---

## Licença

Projeto de uso educacional. Os dados são de domínio público e estão disponíveis no Kaggle sob licença aberta.
