Projeto Individual: Marketing_campaign
Dataset Concedido pelo professor: https://drive.google.com/file/d/1BS46ogaV9XH1fuYrPpvsEk84NcQ3MY62/view?usp=drive_web&authuser=0

📗 **Diretrizes do Projeto:**
>Nivel Infra

- O Dataset deve ser salvo em ambiente cloud(Cloud Storage)
- O arquivo original e tratado deve ser salvo em MongoDB Atlas em coleções diferentes
- O Dataset devem ser obrigatoriamente salvos em uma bucket do CloudStorage
>Nivel Pandas

- O arquivo está em outra linguagem e deve ter seus dados traduzidos para Português-BR
- Realizar a extração corretamente para um dataframe
- Verificar a existência de dados inconsistentes e realizar a limpeza para NaN ou NA explicando o porque da decisão
- Realizar o drop(se necessário) de colunas do dataframe realizando o comentário do porque da exclusão
>Nivel PySpark

- Deverá ser montada a estrutura do DataFrame utilizando o StructType.
- Verificar a existência de dados inconsistentes, nulos e realizar a limpeza.
- Verificar a necessidade de drop em colunas ou linhas. Caso seja necessário, fazer comentário do porque.
- Realizar a mudança de nome de pelo menos 2 colunas
- Deverá criar pelo menos duas novas colunas contendo alguma informação relevante sobre as outras colunas já existentes (Funções de Agrupamento, Agregação ou Joins). (Use a sua capacidade analítica)
- Deverá utilizar filtros, ordenação e agrupamento, trazendo dados relevantes para o negócio em questão. (Use a sua capacidade analítica)
- Utilizar pelo menos duas Window Functions
