![GitHub repo size](https://img.shields.io/github/repo-size/Igor-R-Amorim/README-template?style=for-the-badge)
![GitHub language count](https://img.shields.io/github/languages/count/Igor-R-Amorim/README-template?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/Igor-R-Amorim/README-template?style=for-the-badge)
![Bitbucket open issues](https://img.shields.io/bitbucket/issues/Igor-R-Amorim/README-template?style=for-the-badge)
![Bitbucket open pull requests](https://img.shields.io/bitbucket/pr-raw/Igor-R-Amorim/README-template?style=for-the-badge)

# Projeto Final - Bootcamp Engenharia de Dados

>Formado pela equipe: Felipe Campelo, Igor Rocha, Madson Cordeiro e Livia Matsumoto 
>
>O tema que nos foi atribuído era: Mercado Farmacêutico

Apresentação Dinamica: https://datastudio.google.com/s/mlTpyE8QvbY

Apresentação Estatica: https://drive.google.com/file/d/14UZ440DX8OcbYJp9bmW_zofUY8PZY_GB/view?usp=sharing
##

<h3 align=center> Fundamentação </h3>
A equipe definiu que nos portariamos como uma empresa de consultoria a fim de traçar a perfil mercadológico e descobrir as melhores opções para o negócio dentro do espaço solicitado.

De acordo com as materias coletadas na internet: 
<ul>
  <li>Segundo levantamento do IMS Institute for Healthcare Informatics, em 2010 o Brasil ocupava 10ª posição mundial no ranking que avalia o uso global de mercados, isto é, o consumo de fármacos pela população. Em 2015, o país subiu para a 7ª posição, e já em 2020 passou a ocupar o 5º lugar no ranking global no consumo de medicamentos.
  </li>
	<li>De acordo com a SINDUSFARMA em relatório da IQVIA, no ano de 2019 o mercado brasileiro de medicamentos teve uma movimentação de R$ 76,98 Bi, Com previsão de alcançar a marca dos 80 Bi em 2020.
  </li>
</ul>
Referencias: Slide 34 - Apresentação do Trabalho
<br>
<br>

Apenas 34% dos laboratorios em territorio brasileiro são empresas Multinacionais, ou seja, mais de 60% deles são empresas de capital nacional. Onde cerca de 45% dos laboratorios esta sediado no estado de SP.
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/d58c3b8a8a0aa58400e42ab8d6a6dada39ac36fe/Projeto%20Final/Imagens/imagem_2022-09-23_143450592.png" width=84%></p>

De acordo com nossas fontes, São Paulo é o estado com maior uso de antibióticos e antiinflamatórios e com um crescimento grande de uso de medicamentos psicolépticos e psicoanalépticos, principalmente durante a pandemia.

Tendo isso em base queremos responder a pergunta do nosso cliente: Compensa investir no mercado farmacêutico do estado de SP?
<br> Onde investir? capital ou interior?
<br> Qual o perfil dos consumidores?
<br> Quanto mais UBS's (Unidades Básica de Saúde) maior ou menor o numero de vendas?

##
<h3 align=center> Requisitos do Projeto </h3>
- Requisitos Obrigatórios
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/84f97e5665569dc4238ca725eeb3806d7d5bbc7d/Projeto%20Final/Imagens/Requisitos%20Obrigat%C3%B3rios.png" width=84%></p>
- Requisitos Complementares
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/84f97e5665569dc4238ca725eeb3806d7d5bbc7d/Projeto%20Final/Imagens/Requisitos%20Complementares.png" width=84%></p>

##
<h3 align=center> Execução do projeto </h3>
Para responder a pergunta do nosso cliente foram utilizados 7 datasets, sendo eles em distintos formatos como CSV, XLS, XLSX e uma extração diretamente de um banco de dados via BigQuery.
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/914f0d37a5b890eb65ee43135dc4def7844c169d/Projeto%20Final/Imagens/Uniao%20Datasets.png" width=84%></p>
O dataset referente as vendas de medicamentos em SP era demasiadamente grande, visto que nosso cliente deseja atuar em SP, e que os anos de relevancia são 2019( pandemia) e 2020(pós-pandemia). extraimos do BigQuery apenas estes anos, deste UF.
<br>
Os dados separadamente não respondiam as perguntas levantadas pelo cliente, sendo necessário uni-los a fim de extrair as comparações necessarias
<p> </p>
<br>

Abaixo foi montado o Workflow do nosso projeto de ETL 
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/914f0d37a5b890eb65ee43135dc4def7844c169d/Projeto%20Final/Imagens/WorkFlow%20-%20Projeto%20Final.png" width=84%></p>
Os dados brutos foram armazenados no Google Cloud Storage através do console do GCP. 
Ao extrair os dados no Google Colab via conector amazenou-se o DataFrame(DF) bruto no MySQL em Cloud com alta disponibilidade.

O tratamento foi realizado com o uso das bibliotecas PySpark e Pandas. 

O carregamento foi realizado com duas tratativas diferentes uma via pipeline e outra via conector:
<ul>
  <li> Via conector, os dados tratados foram enviados para o Google Cloud Storage;
  </li>
  <li> Via pipeline, Foi criado um modelo batch com o Apache Beam para o envio direto dos dados tratados do Google Cloud Storage para o BigQuery. E, através de um modelo pré-definido do Google Dataflow, realizamos o envio dos dados tratados do BigQuery para o MongoDB.
  </li>
</ul>
Por fim, inseriu-se os dados no Google DataStudio para análise dos dados.	
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/96b1d75c7d39e7de6e14680a75dc4fb00865086a/Projeto%20Final/Imagens/DataStudio.png" width=84%></p>
<p> </p>
<br>

##
<h3 align=center> Resultados Obtidos </h3>
Após todo o processo de ETL, com dos dados tratados em seus devidos lugares, seja na bucket tratada ou no BigQuery. Comecou-se a tentar responder as perguntas do cliente.

É melhor investir na capital ou interior?
<br>
Inicialmente a ideia seria comparar a quantidade de vendas por município. Porém, os municípios de maior densidade demográfica logicamente consumiam mais. Portanto levantamos a seguinte métrica. Dividimos o somatório de venda de cada cidade pela quantidade de habitantes daquela cidade a fim de obter o que chamamos de fator de venda.
Assim podemos comparar melhor quais cidades venderam mais independente do tamanho de sua população.
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/96b1d75c7d39e7de6e14680a75dc4fb00865086a/Projeto%20Final/Imagens/Fluxo%20de%20vendas.png"></p>
De acordo com o gráfico de 'Fator de vendas x Cidade' podemos observar que a cidade com o maior fator de vendas é Ubatuba, porém mais de 90% do seu fator de venda está concentrado em 2019. Já as cidades de Sabino e São José do Rio Preto têm um fator de vendas crescentes indicando possíveis oportunidades. Já a cidade de Borá apresenta uma linearidade com o passar dos anos, indicando uma boa previsibilidade de fluxo de vendas.

Qual o perfil dos consumidores?
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/96b1d75c7d39e7de6e14680a75dc4fb00865086a/Projeto%20Final/Imagens/Perfil%201.png" width=84%></p><br>
O gráfico de 'Quantidade de vendas x idade' nos mostra quais são as faixas de idade que mais consomem medicamento no estado.
Podemos notar que as pessoas de 40 a 45 anos e de 55 a 60 anos são o público de maior consumo.
<br>
Quando olhamos o gráfico de 'Vendas x Categoria Etária' podemos ver que de 2019 para 2020 o público adulto foi o único que teve um crescimento sobre o consumo de fármacos.
<br>
Dos 51,179 Mi de medicamentos vendidos no periodo, o público feminino consumiu pouco mais do que 55% dos medicamentos do período, não havendo grande distinção entre os sexos.
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/96b1d75c7d39e7de6e14680a75dc4fb00865086a/Projeto%20Final/Imagens/Perfil%202.png" width=84%></p><br>
Diferentemente da quantidade total de 51.179 Mi, o público adulto consumiu 32.848 Mi dessa quantia.
<br>
Ao listar os medicamentos mais consumidos por esse público, observa-se que os 8 mais vendidos são todos da categoria ATC 'J' classificados como antibióticos e anti-infecciosos gerais. Confirmando assim a reportagem na motivação desse projeto.
<br>
A quantidade distinta de medicamentos disponíveis no mercado é maior para genéricos do que para medicamentos similares ou "novos" (medicamentos de referência ex: aspirina®, viagra®, coristina®,...) como podemos confirmar no gráfico de 'Variedade de medicamentos x Tipo de medicamento'
Porém temos uma variedade muito maior de laboratórios que fabricam similares e referência do que genéricos, conforme o gráfico 'Quantidade de fabricantes x Tipo de medicamento'.
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/270dfcaf9cd4add96c2e04eb13201300fae5f526/Projeto%20Final/Imagens/Perfil%203.png" width=84%></p><br>
Fazendo uma tabela dinâmica com mapa de calor, podemos ver uma grande variedade de medicamentos psicolépticos(N05) e psicoanalépticos(N06) ocupando as 2ª e 4ª posição da tabela. 
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/270dfcaf9cd4add96c2e04eb13201300fae5f526/Projeto%20Final/Imagens/PsicoAtivos.png" width=84%></p><br>
Nesse slide, fica claro que para todas as idades os medicamentos "Psico-Ativos" (psicolépticos e psicoanalépticos) teve um aumento de consumo.
<br>
Ao listar os princípio ativos mais vendidos, vemos os 2 primeiros do quadro "Princípio ativo mais vendidos", oxalato de escitaloprám e cloridrato de sertralina são dois antidepressivos mais vendidos em SP.
<br>
Ao usar o checkbox filtrando apenas os anos de 2019 e posteriormente o de 2020 tivemos um aumento de quase 70mil unidades vendidas desses medicamentos com o passar do ano.
<br>
Diferentemente da visão geral, no caso dos medicamentos "Psico-Ativos" as mulheres têm participação maior um pouco. pouco mais de 60% de consumo em relação ao público masculino.
<br>
<br> Quanto mais UBS's (Unidades Básica de Saúde) maior ou menor o numero de vendas?
<p align=center><img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/270dfcaf9cd4add96c2e04eb13201300fae5f526/Projeto%20Final/Imagens/QtdUBS.png"></p><br>
Para responder essa pergunta, vamos resgatar o gráfico de 'Fator de vendas acumulado no período x Cidade' e compará-lo com o gráfico 'Cidade x Quantidade de UBS'.
<br> 
Observa-se que nenhuma das cidades com maior quantidade de UBS’s aparecem no gráfico de fator de vendas, causando na equipe a falsa esperança de que quantidade de UBS's seria inversamente proporcional ao fator de vendas. Porém ao comparar diretamente, a quantidade de UBS's pelo Fator de vendas, observa-se que não existe uma correlação clara entre as variáveis. Mas que cidades com menos de 35 UBS's são as que mais vendem.

##
<h3 align=center> Referencias e outros questinamentos </h3>

- Outras perguntas como os custos do projeto, Serviços mais usados em cloud, detalhes explicativos do codigo ou referencias bibliograficas das informaçoes e dos datasets usados estão na apresentação.


- Contatos podem ser obtidos no README do autor deste Repositório ou tambem na apresentação contendo todos os integrantes.


- A gravação original da apresentação pode ser obtidida através de solicitação com a soulcode. 
​
