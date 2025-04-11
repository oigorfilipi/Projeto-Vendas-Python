Abaixo, meu primeiro estudo de Python. Iniciando com a criação de uma simples tabela de faturamento, preço, lojas e quantidade. Criado no Colab do Google.

-------------------
# Lógica de Programação

  # Passo 0 - Entender o desafio que você quer resolver;

  # Passo 1 - Percorrer todos os arquivos da pasta base de dados (Pasta Vendas);

import os - É uma Biblioteca dentro do Python (Nesse caso a biblioteca OS)
import pandas as pd #Uma biblioteca para trabalhar com base de dados dentro do Python. O "as pd" = Um apelido dado a biblioteca pandas (Para não precisar escrever: "pandas ---" toda vez. e no lugar eu colocar só "pd ---")

lista_arquivo = os.listdir("/content/drive/MyDrive/Curso de Python/Curso Básico de Python/Vendas") 
 - O "lista arquivos" = O nome da variável. 
 - Já "os.listdir()" = Um método dentro da biblioteca OS para listar os arquivos de um determinado diretório colocado no parênteses

print(lista_arquivo) 
 - print() = Exibir na tela (horizontal) oque vc pedir dentro dos parênteses. 
 - display = Faz o mesmo que o print porem na vertical.

  
tabela_total = pd.DataFrame() - SÓ CRIADO CASO FOR USAR APPEND POREM O APPEND É SÓ EM VERSÕES ANTIGAS DO PANDA ANTES DA 2.0
 - Criar uma tabela vazia - SÓ CRIADO CASO FOR USAR APPEND POREM O APPEND É SÓ EM VERSÕES ANTIGAS DO PANDA ANTES DA 2.0
 - pd.DataFrame() = Uma tabela no Python - SÓ CRIADO CASO FOR USAR APPEND POREM O APPEND É SÓ EM VERSÕES ANTIGAS DO PANDA ANTES DA 2.0

tabelas = []
 - Cria uma lista vazia para guardar as tabelas

 # Passo 2 - Importar as bases de dados vendas;
 # Passo 3 - Tratar / Compilar as bases de dados;

for arquivo in lista_arquivo: 
 - for = Para. Um modulo de repetição, onde o "for" Funciona da seguinte forma: Para cada arquivo em "lista_arquivo" fazer algo
if "Vendas" in arquivo: 
 - if = Se. Uma condição. Funciona da seguinte forma: Se "Vendas" (Nome do arquivo) está dentro de arquivo (variável do repositório) ele fará algo 
 - Outro modo de usar: if "vendas" in arquivo.lower(): = Se vendas (Em letras minúsculas) está dentro de arquivo (em letra minúscula).
 - Outro modo de usar: if not "Vendas" in arquivo: = Se Vendas NÃO está dentro de arquivo (variável do repositório) ele fará algo 
    
	print(f"/content/drive/MyDrive/Curso de Python/Curso Básico de Python/Vendas/{arquivo}") 
	 - O "f" Fala pro Python que o texto em sua frente aceita formatações dinâmicas. 
	 - As "{}" dento do texto = Indicam para o Python que não é para escrever a palavra "arquivo", mas sim o valor da variável arquivo
  - else: #Caso contrário. if é falso? Então executa o else.
    
# Importar o Arquivo
	tabela = pd.read_csv(f"/content/drive/MyDrive/Curso de Python/Curso Basico de Python/Vendas/{arquivo}")
 	 - "tabela" = o nome da váriavel que se encontra o pd...
 	 - pd.read_csv() = Fala para o Python que é para ele ler os arquivos do tipo "csv" dentro do diretório em que se localiza os arquivos.
	print(arquivo)
    	display(tabela)
	 - print =  Mostrar o arquivo
    	 - display = Mostrar a tabela do arquivo
	tabela_total = tabela_total.append(tabela) - SÓ USADO EM VERSÕES ANTIGAS DO PANDA ANTES DA 2.0
	 - .append = Indica que ocorrerá uma adição das infomações da tabela dentro da tabela total.  - SÓ USADO EM VERSÕES ANTIGAS DO PANDA ANTES DA 2.0
	tabelas.append(tabela)
	 - .append(tabela) = Adiciona cada tabela lida do CSV na lista
    	tabela_total = pd.concat(tabelas)
	 - ps.concat = Junta todas as tabelas da lista em uma só


 # Passo 4 - Calcular o produto mais vendido (Em quantidade);
	tabela_produtos = tabela_total.groupby("Produto").sum(numeric_only=True)
	 - .groupby("Produto") = Agrupar todos os itens iguais na coluna Produto.
	 - .sum = somar as colunas
	 - numeric_only=True = Indica a soma somente dos numeros
	tabela_produtos = tabela_produtos[["Quantidade Vendida", "Preco Unitario"]].sort_values(by="Quantidade Vendida",ascending=True)
	 - [[]] = Indica quais colunas eu quero que me mostre
	 - [] = Caso eu queira ver somente uma coluna (Porem o formato da tabela fica menos formatada)
	 - [[]] = Caso eu queira ver mais de uma coluna
	 -.sort_values = Ordenas Valores
	 - by="" = Indica qual a coluna que eu quero ordenar.
	 - Ascending=True = Crescente ou Decrescente (True= Crescente (Do maior para o menor)) (False= Descrescente (Do menor para o Maior))

display(tabela_produtos)


# Passo 5 - Calcular o produto que mais faturou (Em faturamento);
	tabela_total["Faturamento"] = tabela_total["Quantidade Vendida"] * tabela_total["Preco Unitario"]
	 - * = Multiplica os valores de uma coluna com os valores de outra coluna
	tabela_faturamento = tabela_total.groupby("Produto").sum()
	tabela_faturamento = tabela_faturamento[["Faturamento", "Quantidade Vendida", "Preco Unitario"]].sort_values(by="Faturamento", ascending=False)
	display(tabela_faturamento)

# Passo 6 - Calcular a loja / cidade que mais vendeu (Em faturamento) - Criar um gráfico / dashboard.
	tabela_lojas = tabela_total.groupby("Loja").sum()
	tabela_lojas = tabela_lojas[["Faturamento"]]
	display(tabela_lojas)

import plotly.express as px
 - plotly.express = Biblioteca de gráficos
 - as px = Apelido para não precisar escrever: plotly.express toda vez.

grafico = px.scatter(tabela_lojas, x=tabela_lojas.index, y="Faturamento")
 - px. = Define qual o tipo de tabela vc vai escolher (Bar, Line, Scatter etc).
 - x=, y= = Define as métricas da tabela: X e Y, horizontal e vertical da tabela
 - .index = Indica para o gráfico qual é o indexe do meu gráfico. (A parte importante)
grafico.show()
 - Mostra o gráfico.

------------------------------------------------------------------ FICANDO ------------------------------------------------------------------

import os
import pandas as pd

lista_arquivo = os.listdir("/content/drive/MyDrive/Curso de Python/Curso Básico de Python/Vendas")
print(lista_arquivo)

for arquivo in lista_arquivo: 
	if "Vendas" in arquivo:
		tabela = pd.read_csv(f"/content/drive/MyDrive/Curso de Python/Curso Básico de Python/Vendas/{arquivo}")
    		tabelas.append(tabela)
    		tabela_total = pd.concat(tabelas)

display(tabela_total)

tabela_produtos = tabela_total.groupby("Produto").sum(numeric_only=True)
tabela_produtos = tabela_produtos[["Quantidade Vendida", "Preco Unitario"]].sort_values(by="Quantidade Vendida",ascending=True)

display(tabela_produtos)

tabela_total["Faturamento"] = tabela_total["Quantidade Vendida"] * tabela_total["Preco Unitario"]
tabela_faturamento = tabela_total.groupby("Produto").sum()
tabela_faturamento = tabela_faturamento[["Faturamento", "Quantidade Vendida", "Preco Unitario"]].sort_values(by="Faturamento", ascending=False)
display(tabela_faturamento)

tabela_lojas = tabela_total.groupby("Loja").sum()
tabela_lojas = tabela_lojas[["Faturamento"]]
display(tabela_lojas)

import plotly.express as px

grafico = px.bar(tabela_lojas, x=tabela_lojas.index, y="Faturamento")
grafico.show()
