# Regressão OLS com Variáveis Categóricas

Este projeto apresenta um exemplo didático de aplicação de **Regressão Linear OLS** com variável explicativa qualitativa, utilizando o processo de **One-Hot Encoding** para representar categorias dentro do modelo.

O objetivo é mostrar, de forma prática e interpretável, por que variáveis categóricas não devem ser tratadas diretamente como números contínuos e como a criação de variáveis dummy permite estimar corretamente o efeito médio de cada categoria em relação a uma categoria de referência.

---

## Objetivo do projeto

O projeto tem como objetivo demonstrar:

* como identificar uma variável explicativa categórica;
* por que a codificação numérica simples pode gerar ponderação arbitrária;
* como aplicar One-Hot Encoding em variáveis qualitativas;
* como estimar um modelo OLS com variáveis dummy;
* como interpretar o intercepto e os coeficientes beta;
* como calcular os valores previstos para cada categoria.

---

## Contexto do exemplo

O dataset utilizado é um exemplo didático sobre gastos de clientes conforme o tipo de refeição.

A variável resposta é:

```text
gasto
```

A variável explicativa categórica é:

```text
refeicao
```

Categorias analisadas:

```text
Cafe
Almoco
Jantar
```

A categoria `Cafe` foi utilizada como referência.

---

## Técnica utilizada

A técnica principal aplicada neste projeto é a **Regressão Linear por Mínimos Quadrados Ordinários**, conhecida como:

```text
OLS - Ordinary Least Squares
```

Além disso, o projeto utiliza:

* análise descritiva;
* tabela de frequências;
* codificação numérica com LabelEncoder para demonstrar o erro conceitual;
* One-Hot Encoding com `pd.get_dummies`;
* estimação de modelo OLS com `statsmodels`;
* interpretação dos coeficientes;
* comparação entre valores observados e valores ajustados.

---

## Por que não transformar categorias diretamente em números?

Uma variável qualitativa, como `Cafe`, `Almoco` e `Jantar`, não possui naturalmente uma ordem ou distância matemática entre suas categorias.

Transformar essas categorias em números, por exemplo:

```text
Cafe = 1
Almoco = 2
Jantar = 3
```

pode fazer com que o modelo interprete essas categorias como se fossem uma escala contínua.

Esse procedimento cria uma **ponderação arbitrária**, pois os números atribuídos às categorias são apenas códigos, e não valores quantitativos reais.

---

## Forma correta: One-Hot Encoding

Para representar corretamente uma variável categórica em um modelo OLS, utilizamos variáveis dummy.

Como existem três categorias e o modelo possui intercepto, usamos:

```text
k - 1 dummies
```

Neste caso:

```text
3 - 1 = 2 dummies
```

Com `Cafe` como categoria de referência:

| Categoria | D_Almoco | D_Jantar |
| --------- | -------: | -------: |
| Cafe      |        0 |        0 |
| Almoco    |        1 |        0 |
| Jantar    |        0 |        1 |

---

## Modelo estimado

O modelo OLS com variáveis dummy pode ser representado por:

```text
Gasto = α + β1 · D_Almoco + β2 · D_Jantar + ε
```

No exemplo didático, o modelo estimado fica próximo de:

```text
Gasto = 20 + 15 · D_Almoco + 30 · D_Jantar
```

---

## Interpretação dos coeficientes

### Intercepto α

O intercepto representa a média da variável resposta na categoria de referência.

Como `Cafe` é a referência:

```text
α = média do gasto no Cafe
```

Neste exemplo:

```text
α = 20
```

Portanto, o gasto médio estimado para clientes no Café é de R$ 20.

---

### Coeficiente β1: Almoço

O coeficiente da dummy `D_Almoco` representa a diferença média entre `Almoco` e a categoria de referência `Cafe`.

```text
β1 = média do Almoço - média do Café
```

Neste exemplo:

```text
β1 = 35 - 20 = 15
```

Portanto, o gasto médio no Almoço é R$ 15 maior que no Café.

---

### Coeficiente β2: Jantar

O coeficiente da dummy `D_Jantar` representa a diferença média entre `Jantar` e `Cafe`.

```text
β2 = média do Jantar - média do Café
```

Neste exemplo:

```text
β2 = 50 - 20 = 30
```

Portanto, o gasto médio no Jantar é R$ 30 maior que no Café.

---

## Exemplo de cálculo dos valores previstos

Para a categoria `Cafe`:

```text
D_Almoco = 0
D_Jantar = 0

Gasto = 20 + 15 · 0 + 30 · 0 = 20
```

Para a categoria `Almoco`:

```text
D_Almoco = 1
D_Jantar = 0

Gasto = 20 + 15 · 1 + 30 · 0 = 35
```

Para a categoria `Jantar`:

```text
D_Almoco = 0
D_Jantar = 1

Gasto = 20 + 15 · 0 + 30 · 1 = 50
```

---

## Principal aprendizado

O processo de **One-Hot Encoding** permite representar variáveis qualitativas dentro de um modelo regressivo, preservando as particularidades contextuais de cada categoria.

Em uma regressão OLS, os coeficientes beta associados às dummies indicam a diferença média de cada categoria em relação à categoria de referência.

Assim, o modelo consegue comparar grupos sem impor uma ordem numérica artificial entre as categorias.

---

## Estrutura do repositório

```text
.
├── ols_variavel_categorica_dummies_refeicao.ipynb
└── README.md
```

---

## Bibliotecas utilizadas

```text
pandas
numpy
statsmodels
matplotlib
seaborn
scikit-learn
```

---

## Como executar

Clone o repositório:

```bash
git clone https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git
```

Acesse a pasta do projeto:

```bash
cd NOME-DO-REPOSITORIO
```

Instale as dependências principais:

```bash
pip install pandas numpy statsmodels matplotlib seaborn scikit-learn
```

Abra o notebook:

```bash
jupyter notebook ols_variavel_categorica_dummies_refeicao.ipynb
```

---

## Possíveis próximos passos

Este projeto pode ser expandido futuramente com:

* regressão OLS com variáveis quantitativas e qualitativas no mesmo modelo;
* análise de significância estatística dos coeficientes;
* interpretação de p-valores e intervalos de confiança;
* comparação entre modelos com e sem variáveis dummy;
* diagnóstico de resíduos;
* validação do modelo;
* aplicação em uma base de dados real.

---

## Conceitos abordados

* Regressão Linear OLS
* Variável categórica
* Variável dummy
* One-Hot Encoding
* Categoria de referência
* Intercepto
* Coeficientes beta
* Ponderação arbitrária
* Interpretação de modelos regressivos

---

## Autora

Projeto desenvolvido por **Samanta Lekecinskas** como parte dos estudos em Data Science, Machine Learning e modelos estatísticos interpretáveis.
