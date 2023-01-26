# Formacao-Engenharia-de-Dados-Projeto-2
https://itau.udemy.com/course/engenheiro-de-dados

O projeto consiste em 3 aplicações Python que simulam produção destes dados.

# Schema

![image](https://user-images.githubusercontent.com/74573131/214825774-6c36d105-38af-4069-b515-451fb691299b.png)


1. Kinesis Data Stream
- O Kinesis Data Stream recebe esses dados
![image](https://user-images.githubusercontent.com/74573131/214834550-0dd53d8b-f381-472c-99b2-7256652bc31c.png)


2. Criar Aplicações geradoras de Dados
- Fazer a lógica das três aplicações conectadas com o Glue
- Todos os sensores devem gerar o mesmo formato  
`idtemp`  
`Data`  
`Type: powerfactor, temperature, hydraulicpressure`  
`Timestamp`  
![image](https://user-images.githubusercontent.com/74573131/214836017-7a62454a-a828-40e8-9f69-74d7e8a25179.png)


3. Bucket
- Criar os buckets no S3
![image](https://user-images.githubusercontent.com/74573131/214838570-d37034ff-c911-421f-a873-9f291cf584b9.png)


4. Kinesis Data Firehouse
- Deverá produzir dados particionados por data
- Dados de todos os sensores no mesmo arquivo
- Kinesis Data Firehouse faz a entrega armazenando em um bucket S3 (a cada 60s para não gera latência muito alta)

5. Crawler, Catalog
- Criar função (Role) para permitir acesso ao Glue
![image](https://user-images.githubusercontent.com/74573131/214839641-2f5564ab-c914-469e-86f2-85aea0757262.png)

- Criar um database no Glue

![image](https://user-images.githubusercontent.com/74573131/214840467-211c49fc-9502-489e-ad06-17fb790d7d52.png)


- Criar Crawler apontando para o S3 contendo os dados e rodar para gerar as tabelas(schema)

- Criar um Job apontando para o S3 criado conforme abaixo, e executa Glue Calalog para se gerar o catalogo
![image](https://user-images.githubusercontent.com/74573131/214842703-9a87d396-0798-4b1d-8b21-8870e1e41665.png)

6. Job para gerar parquet
- A partir deste catalogo e dados do S3 o Glue Job cria um banco de dados (tabela) que salva em outro bucket S3

7. Athena
- Utilizando o Athena será consultados esses dados neste bucket S3 (formato parquet)
- definir um bucket qualquer para ser utilizado como bufer
- exemplo de uma consulta pelo Athena
![image](https://user-images.githubusercontent.com/74573131/214844958-47a7a88f-32ba-4a50-a946-dda2c91cadeb.png)



