# 📦 Projeto de Análise Exploratória - Olist E-Commerce
Impulsionado pela facilidade de compra e diversidade de produtos, o comércio eletrônico brasileiro está bastante presente no dia a dia da população, em contrapartida, apresenta vários desafios logísticos significativos, como atrasos na entrega, inconsistências nos cadastros e grande variação de características de produtos. Essas imperfeições são típicas de um ambiente real de comercio online. Diante desse cenário, surge o problema real tratado nesse trabalho: O que afeta a experiência e satisfação do cliente no e-commerce brasileiro?

## 👥 Integrantes
- Antônio Neves Aguiar Neto
- Wickham Carneiro Pereira

---

## 🔗 Base de Dados Utilizada
O projeto utiliza parte do conjunto de dados públicos da **Olist**, disponibilizado originalmente no Kaggle:

**Link da base completa:**  
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data

Datasets utilizados no projeto:
- `olist_orders_dataset.csv`  
- `olist_order_items_dataset.csv`  
- `olist_products_dataset.csv`

Olist_order_items_dataset – Itens vendidos em cada pedido
Esse dataset relaciona cada pedido aos produtos comprados, representa apenas compras reais, por isso foi usada como tabela principal no processo de merge, pra evitar pedidos incompletos e cancelados.
Tem atributos como: order_id, Product_id, seller_id, order_item_id, price, freight_value, shipping_limit_date

Olist_orders_dataset – Informações dos pedidos
Esse dataset tem os dados de cada pedido realizado na plataforma, tem atributos como: order_id, custumer_id, order_status e datas do processo.

Olist_products_dataset – Informações dos produtos
Esse dataset tem atributos de cada produto vendido, tem atributos como: Product_id, Product_category_name, Product_name_lenght, Product_description_lenght, Product_photos_qty.
Esse dataset em específico possui vários valores ausentes, o que veremos depois.
---

## 🎯 Objetivo do Projeto
Aplicar o ciclo de vida da Ciência de Dados para descobrir o que afeta a experiência e satisfação do cliente no e-commerce brasileiro, investigando os padrões que influenciam:

● Atrasos de entrega
● Baixa ou alta satisfação
● Diferenças de preço e frete
● Categorias de produtos problemáticas
● Variações no tempo de processamento e envio


O objetivo final foi construir um dataset limpo, padronizado e enriquecido, capaz de gerar insights relevantes sobre desempenho logístico e experiência do cliente.

---

## 🛠️ Descrição do Processo de Tratamento dos Dados

O pré-processamento seguiu as etapas ensinadas em aula:

### **1. Exploração Inicial**
- Uso de `df.head()`, `df.info()` e `df.describe()`  
- Identificação de tipos, estatísticas e valores ausentes  
- Visualizações iniciais com heatmap para correlação

### **2. Tratamento de Valores Ausentes**
- Preenchimento por mediana para variáveis numéricas  
- Categoria “desconhecido” para valores ausentes em texto  
- Identificação de alta ausência no dataset de produtos

### **3. Remoção/Correção de Inconsistências**
- Padronização textual (`str.lower()`, `str.strip()`)  
- Correção de pesos iguais a zero ou negativos  
- Conversão de colunas de data para `datetime`

### **4. Outliers**
- Analisados via estatísticas e gráficos  
- **Apenas valores inválidos foram corrigidos**  
- Outliers reais foram mantidos por representarem casos legítimos (ex.: móveis caros)

### **5. Conversão e Padronização de Tipos**
- Datas → `datetime`  
- Quantidades numéricas → `int64`

### **6. Codificação de Dados Categóricos**
- One-Hot Encoding aplicado em `order_status`

### **7. Normalização**
- Padronização com StandardScaler em atributos numéricos selecionados

### **8. Feature Engineering**
Criação das seguintes features:
- `delivery_delay_days` – dias de atraso/adiantamento  
- `is_late_delivery` – atraso binário  
- `processing_time_days` – tempo que o vendedor levou para despachar  
- `freight_per_kg` – custo logístico proporcional ao peso  

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

- **Atrasos não dependem apenas da transportadora:** o tempo de processamento do vendedor é um fator crucial.  
- **Peso e dimensões influenciam diretamente o frete**, com correlação clara entre eles.  
- **A maioria dos pedidos é entregue dentro do prazo**, demonstrando boa eficiência logística.  
- **A limpeza dos dados foi essencial** para corrigir distorções, como pesos inválidos e categorias duplicadas.  
- As features criadas permitiram **identificar padrões logísticos profundos**, como relação entre atraso × processamento e custo logístico × peso.  
- Produtos maiores e mais pesados apresentam comportamento logístico completamente diferente de produtos pequenos.

---

