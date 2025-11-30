# 📦 Projeto de Análise Exploratória - Olist E-Commerce
Impulsionado pela facilidade de compra e diversidade de produtos, o comércio eletrônico brasileiro está bastante presente no dia a dia da população, em contrapartida, apresenta vários desafios logísticos significativos, como atrasos na entrega, inconsistências nos cadastros e grande variação de características de produtos. Essas imperfeições são típicas de um ambiente real de comercio online.


Diante desse cenário, surge o problema real tratado nesse trabalho: O que afeta a experiência e satisfação do cliente no e-commerce brasileiro?

## 👥 Integrantes
- Antônio Neves Aguiar Neto
- Wickham Carneiro Pereira

---

## 🔗 Base de Dados Utilizada
O projeto utiliza parte do conjunto de dados públicos da Olist, disponibilizado originalmente no Kaggle:

**Link da base completa:**
[Olist Brazilian E-Commerce Dataset (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data)

Datasets utilizados no projeto:
- `olist_orders_dataset.csv`  
- `olist_order_items_dataset.csv`  
- `olist_products_dataset.csv`

Olist_order_items_dataset – Itens vendidos em cada pedido
Olist_orders_dataset – Informações dos pedidos
Olist_products_dataset – Informações dos produtos

---

## 🎯 Objetivo do Projeto
Aplicar o ciclo de vida da Ciência de Dados para descobrir o que afeta a experiência e satisfação do cliente no e-commerce brasileiro, investigando os padrões que influenciam:

- Atrasos de entrega
- Baixa ou alta satisfação
- Diferenças de preço e frete
- Categorias de produtos problemáticas
- Variações no tempo de processamento e envio


O objetivo final foi construir um dataset limpo, padronizado e enriquecido, capaz de gerar insights relevantes sobre desempenho logístico e experiência do cliente.

---

## 🛠️ Descrição do Processo de Tratamento dos Dados

O pré-processamento dos dados foi realizado seguindo uma sequência estruturada de etapas para garantir consistência, qualidade e confiabilidade das análises. As principais fases foram:

### **1. Carregamento e Exploração Inicial**
Iniciamos com a inspeção das bases utilizando `df.head()`, `df.info()` e `df.describe()`.  
Essa etapa permitiu identificar tipos de dados, presença de valores ausentes, estatísticas descritivas e possíveis problemas iniciais.

### **2. Identificação dos Valores Ausentes**
Com o comando `df.isnull().sum()`, contabilizamos a quantidade de valores ausentes em cada coluna.  
Isso permitiu definir quais atributos precisavam de imputação ou tratamento específico.

### **3. Tratamento dos Valores Ausentes**
- Variáveis numéricas receberam **imputação pela mediana por categoria**, garantindo coerência com o comportamento dos produtos.  
- Colunas categóricas tiveram seus valores ausentes substituídos por `"desconhecido"`.

### **4. Correção de Inconsistências**
- Valores impossíveis, como **pesos igual a zero ou negativos**, foram substituídos pela mediana da respectiva categoria de produto.  
- Realizamos padronização textual (`str.lower()` + `str.strip()`) para evitar categorias duplicadas devido a diferenças de maiúsculas/minúsculas ou espaços extras.

### **5. Codificação das Variáveis Categóricas**
Aplicamos **One-Hot Encoding** (`pd.get_dummies`) na coluna `order_status`, permitindo que os modelos e análises futuras trabalhem com variáveis categóricas de forma numérica e interpretável.

### **6. Normalização / Padronização das Variáveis Numéricas**
Utilizamos o **StandardScaler** para padronizar atributos numéricos, garantindo escalas equivalentes entre variáveis e evitando distorções em análises que dependem de magnitude.

### **7. Criação de Novas Features (Feature Engineering)**
Foram criados atributos que enriquecem a análise logística:
- **Tempo de entrega (delivery_delay_days)** 
- **Atraso binário (is_late_delivery)**
- **Dias de processamento (delivery_time_days)**
- **Custo do frete por peso (freight_per_kg)**

Essas features permitiram compreender melhor o comportamento logístico e identificar relações não visíveis nas colunas originais.

---

## 🚧 Principais Desafios Encontrados
- Alta ausência de dados no dataset de produtos  
- Peso e medidas com valores inconsistentes  
- Variáveis de data no formato texto  
- Necessidade de integrar três bases diferentes via merge  
- Outliers legítimos que não podiam ser removidos  
- Diferenças de categoria causadas por erros de escrita

---

## 📌 Principais Conclusões 

Foi revelado padrões importantes, as conclusões principais foram:

- **Atrasos dependem tanto do vendedor quanto da transportadora**  
   O tempo que o vendedor leva para processar e despachar o pedido tem forte impacto no atraso final, mostrando que a responsabilidade logística é compartilhada.

- **Peso e dimensões influenciam diretamente o valor do frete**  
   Produtos pesados ou volumosos, especialmente móveis, eletrodomésticos e utilidades domésticas grandes, apresentam fretes mais altos devido à complexidade do transporte.

- **A maioria dos pedidos é entregue no prazo ou antes**  
   A distribuição do atraso mostra uma operação estável, com poucas entregas realmente atrasadas.

- **Os dados apresentavam inconsistências relevantes**  
   Foram encontrados pesos inválidos, textos despadronizados e muitos valores ausentes no dataset de produtos. O pré-processamento foi essencial para corrigir esses problemas e garantir análises consistentes.

- **As novas features ampliaram a compreensão logística**  
   As variáveis criadas (`delivery_delay_days`, `is_late_delivery`, `processing_time_days`, `freight_per_kg`) ajudaram a explicar padrões de atraso, eficiência de vendedores e comportamento do frete de forma mais clara do que os dados originais permitiam.


---

