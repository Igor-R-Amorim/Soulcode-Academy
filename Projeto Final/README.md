# Projeto Final - Bootcamp Engenharia de Dados

Formado pela equipe: Felipe Campelo, Igor Rocha, Madson Cordeiro e Livia Matsumoto 
<br>
O tema que nos foi atribuído era: Mercado Farmacêutico

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
<img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/d58c3b8a8a0aa58400e42ab8d6a6dada39ac36fe/Projeto%20Final/Imagens/imagem_2022-09-23_143450592.png">

De acordo com nossas fontes, São Paulo é o estado com maior uso de antibióticos e antiinflamatórios e com um crescimento grande de uso de medicamentos psicolépticos e psicoanalépticos, principalmente durante a pandemia.

Tendo isso em base queremos responder a pergunta do nosso cliente: Compensa investir no mercado farmacêutico do estado de SP?
onde investir? capital ou interior?
Qual o perfil dos consumidores?
Quanto mais UBS's (unidades Básica de Saúde) Maior ou menor o numero de vendas?

##
<h3 align=center> Requisitos do Projeto </h3>
- Requisitos Obrigatórios
<img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/84f97e5665569dc4238ca725eeb3806d7d5bbc7d/Projeto%20Final/Imagens/Requisitos%20Obrigat%C3%B3rios.png">
- Requisitos Complementares
<img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/84f97e5665569dc4238ca725eeb3806d7d5bbc7d/Projeto%20Final/Imagens/Requisitos%20Complementares.png">

##
<h3 align=center> Execução do projeto </h3>
Para responder a pergunta do nosso cliente foram utilizados 7 datasets, sendo eles em distintos formatos como CSV, XLS, XLSX e uma extração diretamente de um banco de dados via BigQuery.
<img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/914f0d37a5b890eb65ee43135dc4def7844c169d/Projeto%20Final/Imagens/Uniao%20Datasets.png">
O dataset referente as vendas de medicamentos em SP era demasiadamente grande, visto que nosso cliente deseja atuar em SP, e que os anos de relevancia são 2019( pandemia) e 2020(pós-pandemia). extraimos do BigQuery apenas estes anos, deste UF.
<br>
Os dados separadamente não respondiam as perguntas levantadas pelo cliente, sendo necessário uni-los a fim de extrair as comparações necessarias
<p> </p>
<br>

Abaixo foi montado o Workflow do nosso projeto de ETL 
<img src="https://github.com/Igor-R-Amorim/Soulcode-Academy/blob/914f0d37a5b890eb65ee43135dc4def7844c169d/Projeto%20Final/Imagens/WorkFlow%20-%20Projeto%20Final.png">
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


​
