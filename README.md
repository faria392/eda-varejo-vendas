# 📊 Análise Exploratória de Dados: Vendas no Varejo (Big Mart Sales)

Projeto de limpeza de dados e análise exploratória (EDA) sobre um dataset de vendas do varejo, com foco em identificar padrões entre **tamanho da loja**, **categoria de produto**, **teor de gordura** e **volume de vendas**.

---

## 🎯 Objetivo

Investigar quais fatores estruturais (tamanho de loja, tipo de produto, composição nutricional) apresentam relação com o total de vendas, aplicando boas práticas estatísticas de limpeza de dados para evitar viés na análise.

---

## 🗂️ Sobre o Dataset

O dataset contém informações de vendas de uma rede de varejo, com variáveis relacionadas a produtos (peso, tipo, preço, teor de gordura) e lojas (tamanho, tipo, localização, ano de estabelecimento).

- **Linhas:** 8.523 registros (após limpeza)
- **Colunas:** 12 variáveis (após remoção de coluna sem dados aproveitáveis)

---

## 🧹 Processo de Limpeza de Dados

A limpeza seguiu uma ordem específica para evitar viés e retrabalho:

| Etapa | Problema Identificado | Ação Tomada | Justificativa |
|---|---|---|---|
| 1 | 27 linhas duplicadas | Removidas (`drop_duplicates`) | Duplicatas exatas de erro de ingestão |
| 2 | Inconsistência categórica em `item_conteudo_gordura` (`BTG`, `reg`, `baixo teor de gordura`, etc.) | Padronização via mapeamento manual | Evitar fragmentação de grupos em análises futuras |
| 3 | 17,18% de nulos em `item_peso` | Imputação por mediana agrupada por `item_identificador`; apenas 4 itens sem nenhuma referência receberam mediana global | Peso é característica fixa do produto — imputação por grupo preserva precisão |
| 4 | 28,27% de nulos em `loja_tamanho` | Criação de categoria explícita `"Desconhecido"` | Ausência concentrada em 3 lojas específicas (padrão MNAR) — imputar inventaria dado inexistente |
| 5 | Coluna `item_quantidade_venda` 100% nula | Coluna removida | Nenhuma informação recuperável |

**Princípio seguido:** nenhuma imputação ou remoção foi feita sem antes investigar o mecanismo de ausência (aleatório vs. estrutural), para não distorcer os padrões reais dos dados.

---

## 📈 Principais Análises e Gráficos

### 1. Vendas Totais × Tamanho da Loja
Comparação de distribuição via **boxplot** (sem outliers, foco no percentil 97) e **boxenplot** (para visualizar a cauda completa da distribuição).

**Achado:** lojas "Desconhecido" apresentam padrão de vendas próximo às lojas "Pequeno", sugerindo que a ausência de informação não indica um comportamento atípico de vendas.

### 2. Vendas Totais × Categoria de Produto
Ranking por **mediana de vendas** (robusta a outliers) em gráfico de barras horizontais.

### 3. Vendas Totais × Teor de Gordura
Comparação via **violin plot** (formato da distribuição) e **boxplot** (comparação direta de mediana).

**Achado:** distribuições muito semelhantes entre "Baixo Teor de Gordura" e "Regular", indicando baixo poder explicativo isolado dessa variável sobre o volume de vendas.

---

## 🛠️ Tecnologias Utilizadas

- Python 3
- Pandas / NumPy
- Matplotlib / Seaborn

---

---

## 👤 Autor

**Gustavo Faria**
Estudante de Ciência de Dados — PUC-Campinas
