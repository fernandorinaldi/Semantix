# Semantix

#Teste Semantix - Líder Técnico

**Qual o objetivo do comando cache em Spark?

Esse comando tem como objetivo disponibilizar os dados em memória na primeira execução, permitindo que as próximas execuções que necessitarem desses dados sejam bem mais rápidas, otimizando o resultado.


**O mesmo código implementado em Spark é normalmente mais rápido que a implementação equivalente em
MapReduce. Por quê?

Quando um job é executado via Spark, os dados são armazenados em memória o que otimiza muito a execução comparado com o MapReduce que faz a gravação em disco após cada execução. Porém é necessário avaliar cada necessidade pois, dependendo do volume de dados que precisam ser processados, pode acontecer do cluster não suportar a gravação em memória e, para essa situação, o MapReduce é o mais adequado.


**Qual é a função do SparkContext ?

É o principal ponto de entrada para utilizar o Spark. O SparkContext representa a conexão com o cluster Spark e pode ser usado para criar RDDs, acumuladores, variáveis, etc.


**Explique com suas palavras o que é Resilient Distributed Datasets (RDD).

É uma representação dos dados distribuídos pelos nodes de um cluster, permitindo operá-los em paralelo. É a primeira maneira com Spark de abstrair os dados e manipulá-los.



**GroupByKey é menos eficiente que reduceByKey em grandes dataset. Por quê?

O GroupByKey realiza um suffle dos dados para formar o par de chave/valor. Porém isso acaba "custando caro" ao se tratar de grandes datasets pois o tamanho dessa lista pode ultrapassar o espaço em uma partição. Já o reduceByKey retorna um conjunto de dados em pares, sendo que os valores já são agregados por chave, utilizando a função de redução.



**Explique o que o código Scala abaixo faz.

1- val textFile = sc . textFile ( "hdfs://..." )
2- val counts = textFile . flatMap ( line => line . split ( " " ))
3- . map ( word => ( word , 1 ))
4- . reduceByKey ( _ + _ )
5- counts . saveAsTextFile ( "hdfs://..." )

1- Lê um arquivo no HDFS
2- Divide o arquivo por palavras, utilizando o <espaço> (" ") como separador
3- Realizada o mapeamento de cada palavra armazenando 1 para cada palavra encontrada
4- Faz a redução realizando a contagem de todas as palavras
5- Grava no HDFS um arquivo com o resultado da contagem
