# Análise de Dados com Pandas

## 1. Exploração dos Dados

### groupBy()
- O método `groupby()` permite agrupar dados com base em uma ou mais colunas e, em seguida, aplicar funções de agregação, como `mean()` para calcular a média.
- **Exemplo:** Calcular a média de preços por tipo de imóvel.
    ```python
    media_precos_por_tipo = df.groupby('tipo_imovel')['preco'].mean()
    print(media_precos_por_tipo)
    ```

### value_counts()
- O método `value_counts()` conta a frequência de valores únicos em uma coluna.
- **Exemplo:** Contar a distribuição dos tipos de imóveis.
    ```python
    distribuicao_tipos_imoveis = df['tipo_imovel'].value_counts()
    print(distribuicao_tipos_imoveis)
    ```

### unique()
- O método `unique()` retorna os valores únicos de uma coluna.
- **Exemplo:** Listar os tipos de imóveis disponíveis.
    ```python
    tipos_imoveis_unicos = df['tipo_imovel'].unique()
    print(tipos_imoveis_unicos)
    ```

### query()
- O método `query()` permite filtrar dados com base em uma expressão.
- **Exemplo:** Filtrar imóveis com preços acima de um determinado valor.
    ```python
    imoveis_caros = df.query('preco > 1000000')
    print(imoveis_caros)
    ```

## 2. Tratamento de Valores Nulos e Registros Inconsistentes

### isnull()
- O método `isnull()` verifica a presença de valores nulos em um DataFrame.
- **Exemplo:** Identificar colunas com valores nulos.
    ```python
    valores_nulos = df.isnull().sum()
    print(valores_nulos)
    ```

### fillna()
- O método `fillna()` substitui valores nulos por um valor especificado.
- **Exemplo:** Substituir valores nulos na coluna `preco` pela média dos preços.
    ```python
    df['preco'].fillna(df['preco'].mean(), inplace=True)
    ```

### drop()
- O método `drop()` remove linhas ou colunas especificadas.
- **Exemplo:** Remover registros que têm valores nulos em qualquer coluna.
    ```python
    df.dropna(inplace=True)
    ```

## 3. Criação de Novas Colunas

### Lambda e apply()
- Funções lambda são funções anônimas e podem ser usadas com `apply()` para criar ou modificar colunas.
- **Exemplo:** Criar uma coluna `preco_milhares` que converte o preço para milhares.
    ```python
    df['preco_milhares'] = df['preco'].apply(lambda x: x / 1000)
    ```

## Exemplo Prático Completo

1. Calcular a média de preços por tipo de imóvel.
2. Contar a distribuição dos tipos de imóveis.
3. Tratar valores nulos na coluna `preco`.
4. Criar uma nova coluna `preco_milhares`.

```python
import pandas as pd

# Supondo que df é o DataFrame com os dados dos imóveis
df = pd.DataFrame({
    'tipo_imovel': ['casa', 'apartamento', 'casa', 'apartamento', 'casa'],
    'preco': [500000, 300000, None, 400000, 600000]
})

# 1. Média de preços por tipo de imóvel
media_precos_por_tipo = df.groupby('tipo_imovel')['preco'].mean()
print("Média de preços por tipo de imóvel:")
print(media_precos_por_tipo)

# 2. Distribuição dos tipos de imóveis
distribuicao_tipos_imoveis = df['tipo_imovel'].value_counts()
print("\nDistribuição dos tipos de imóveis:")
print(distribuicao_tipos_imoveis)

# 3. Tratar valores nulos na coluna preco
df['preco'].fillna(df['preco'].mean(), inplace=True)
print("\nDados após tratar valores nulos:")
print(df)

# 4. Criar uma nova coluna preco_milhares
df['preco_milhares'] = df['preco'].apply(lambda x: x / 1000)
print("\nDados com a nova coluna preco_milhares:")
print(df)
