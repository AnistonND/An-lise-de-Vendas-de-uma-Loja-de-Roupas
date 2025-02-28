# Análise de Vendas de uma Loja de Roupas


Este projeto realiza uma análise de vendas de uma loja de roupas, fornecendo estatísticas e visualizações gráficas para auxiliar na tomada de decisão. Os dados incluem produtos, categorias, preços e quantidades vendidas.

## 📌 Funcionalidades
- Criar um DataFrame com os dados de vendas da loja.
- Filtrar produtos com preço acima de um valor definido.
- Exibir estatísticas gerais sobre as vendas.
- Gerar gráficos para melhor visualização dos dados.

## 📂 Estrutura do Código
O código está dividido em funções para facilitar a modularização e reutilização.

### 1️⃣ Criar DataFrame
A função `criar_dataframe()` cria um DataFrame com informações sobre os produtos da loja:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

def criar_dataframe():
    """DataFrame com dados de vendas de uma loja de roupas."""
    data = {
        'Produto': ['Camiseta', 'Calça Jeans', 'Vestido', 'Jaqueta', 'Tênis', 'Blusa', 'Shorts', 'Saia', 'Moletom', 'Bermuda'],
        'Categoria': ['Casual', 'Casual', 'Feminino', 'Inverno', 'Calçados', 'Feminino', 'Casual', 'Feminino', 'Inverno', 'Casual'],
        'Preco': [50, 160, 150, 200, 250, 80, 90, 100, 180, 110],
        'Quantidade_Vendida': [300, 150, 120, 90, 130, 180, 210, 160, 95, 175]
    }
    return pd.DataFrame(data)
```

### 2️⃣ Filtrar Produtos por Preço
A função `filtrar_produtos(df, preco_minimo=100)` filtra os produtos cujo preço é superior a um determinado valor.

```python
def filtrar_produtos(df, preco_minimo=100):
    """Filtra produtos com preço acima de um determinado valor."""
    return df[df['Preco'] > preco_minimo]
```

### 3️⃣ Exibir Estatísticas de Vendas
A função `exibir_estatisticas(df)` calcula e exibe estatísticas importantes sobre as vendas.

```python
def exibir_estatisticas(df):
    """Estatísticas sobre as vendas da loja."""
    faturamento_total = np.sum(df["Preco"] * df["Quantidade_Vendida"])
    stats = {
        'Faturamento Mensal': f'R$ {faturamento_total / 12:,.2f}',
        'Faturamento Anual': f'R$ {faturamento_total:,.2f}',
        'Produto Mais Vendido': df.loc[df['Quantidade_Vendida'].idxmax(), 'Produto'],
        'Produto Mais Caro': df.loc[df['Preco'].idxmax(), 'Produto'],
        'Média de Preço': f'R$ {df["Preco"].mean():,.2f}',
        'Total de Itens Vendidos': df['Quantidade_Vendida'].sum(),
        'Número de Reclamações': 15,
        'Taxa de Satisfação dos Clientes': '92%',
        'Tráfego': '500.000 visitas/mês',
        'Engajamento': '18%'
    }
    for key, value in stats.items():
        print(f"{key}: {value}")
```

### 4️⃣ Gerar Gráficos
A função `plotar_graficos(df)` cria três gráficos para análise visual dos dados.

```python
def plotar_graficos(df):
    """Plota gráficos sobre vendas e categorias com estilo profissional."""
    sns.set_style("whitegrid")
    fig, axes = plt.subplots(1, 3, figsize=(18, 6))
    
    # Gráfico de Preço por Produto
    sns.barplot(ax=axes[0], x=df['Produto'], y=df['Preco'], palette='coolwarm', edgecolor='black')
    axes[0].set_xlabel('Produto', fontsize=12, fontweight='bold')
    axes[0].set_ylabel('Preço (R$)', fontsize=12, fontweight='bold')
    axes[0].set_title('Preço por Produto', fontsize=14, fontweight='bold')
    axes[0].tick_params(axis='x', rotation=45)
    
    # Gráfico de Quantidade Vendida por Categoria
    categoria_vendas = df.groupby('Categoria')['Quantidade_Vendida'].sum().reset_index()
    sns.barplot(ax=axes[1], x=categoria_vendas['Categoria'], y=categoria_vendas['Quantidade_Vendida'], palette='viridis', edgecolor='black')
    axes[1].set_xlabel('Categoria', fontsize=12, fontweight='bold')
    axes[1].set_ylabel('Quantidade Vendida', fontsize=12, fontweight='bold')
    axes[1].set_title('Quantidade Vendida por Categoria', fontsize=14, fontweight='bold')
    
    # Gráfico de Distribuição de Vendas (Pizza)
    wedges, texts, autotexts = axes[2].pie(df['Quantidade_Vendida'], labels=df['Produto'], autopct='%1.1f%%', colors=sns.color_palette('pastel'), wedgeprops={'edgecolor': 'black'})
    for text in texts + autotexts:
        text.set_fontsize(10)
        text.set_fontweight('bold')
    axes[2].set_title('Distribuição de Vendas por Produto', fontsize=14, fontweight='bold')
    
    plt.tight_layout()
    plt.show()
```

## 🚀 Como Executar o Projeto
1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/analise-vendas-loja.git
   ```
2. Instale as dependências:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
3. Execute o script:
   ```bash
   python nome_do_arquivo.py
   ```

## 📌 Tecnologias Utilizadas
- **Python**
- **Pandas** para manipulação de dados
- **NumPy** para cálculos
- **Matplotlib e Seaborn** para visualização de dados

---



