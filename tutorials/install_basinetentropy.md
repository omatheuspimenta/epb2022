# BASiNETEntropy - Tutorial de instalação

BASiNETEntropy é um pacote em R disponível no repositório CRAN destinado inicialmente para a classificação de sequências biológicas de RNA, sendo uma versão atualizada do pacote BASiNET, com o diferencial de não possuir thresholds para a obtenção das medidas topológicas das redes complexas geradas a partir das sequências biológicas de entrada.  
Através do pacote BASiNETEntropy é possível realizar a classificação de sequências de RNA codificante (mRNA), longo não-codificante (lncRNA) e curto não-codificante (sncRNA). Além da classificação também é possível realizar o treinamento e salvar o modelo para análises/classificação posteriores.  
A instalação do pacote é feita através do comando 
`install.packages` no próprio console do R.  
Este tutorial traz um guia amigável para iniciantes, com informaçõs detalhadas sobre como instalar o pacote BASiNET sem ter qualquer conhecimento técnico.  

__Este tutorial foi desenvolvido para o sistema operacional Linux, em particular, distribuições Ubuntu 22.04, além do usuário necessitar de privelégios de administrador para a instalação dos pacotes__ 

*O pacote BASiNETEntropy necessita do R versão igual ou superior a 4.1*

Para a instalação do R acesse [tutorial de instalação do R](install_basinet.md#etapa-2-instalação-do-r)

## Instalação do BiocManager (Bioconductor)

Para a leitura dos arquivos FASTA o pacote BASiNETEntropy tem como depência o pacote [biostrings](https://bioconductor.org/packages/release/bioc/html/Biostrings.html), que é disponibilizado pelo [Bioconductor](https://bioconductor.org/).  
A instalação pode ser feita dentro do console do R. Após abrir o console R utilizando o comando
```{bash}
R
```
digite os seguintes comandos
```{R}
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("Biostrings")
```
Caso a versão do R seja mais antiga, consulte a documentação disponível no [Bioconductor](https://bioconductor.org/about/release-announcements/).

## Instalação das dependências

As dependências são instaladas diretamente no console R através dos comandos abaixo

```{R}
install.packages("igraph")
install.packages("randomForest")
```

__Esta etapa pode levar um tempo devido a instalação dos pacotes__

## Instalação do BASiNETEntropy

Após a instalação de todas as dependências, ainda no console R digite

```{R}
install.packages("BASiNETEntropy")
```

## Utilização do BASiNETEntropy
Para carregar o pacote BASiNETEntropy no console do R digite
```{R}
library("BASiNETEntropy")
```

A função principal é a `classify` que aplica a metodologia proposta no artigo para a classificação das sequências de RNA. Ao fim da execução o resultado da classificação é obtido.  
Os parâmetros da função são os seguintes:  
* mRNA: Diretório do arquivo FASTA contendo sequências de mRNA;  
* lncRNA: Diretório do arquivo FASTA contendo sequências de lncRNA;  
* sncRNA: Diretório do arquivo FASTA contendo sequências de sncRNA;  
* trainingResult: Resultado da etapa de treinamento, usualmente duas (ou três) matrizes armazenadas em uma lista. Este argumento pode ser implementado caso o usuário tenha domínio da linguagem R, sendo um parâmetro totalmente opcional e avançado do pacote;  
* save_dataframe: Se `TRUE` salva as características extraídas em um arquivo `.csv` no diretório atual. Por padrão, nenhum arquivo é criado;  
* save_model: Se `TRUE` salva o modelo treinado para a classificação em formato `.rds` no diretório atual. Por padrão, nenhum arquivo é criado.

```{R}
classify(mRNA,lncRNA,sncRNA = NULL,trainingResult,save_dataframe = NULL,save_model = NULL)
```

Um exemplo básico de utilização do pacote é dado através dos comandos:
```{R}
mRNA <- system.file("extdata", "mRNA.fasta", package = "BASiNETEntropy")
lncRNA <- system.file("extdata", "ncRNA.fasta", package = "BASiNETEntropy")
result <- classify(mRNA=mRNA, lncRNA=lncRNA)
``` 

Uma saída esperada do comando é a seguinte:
```{R}
[INFO] Analyzing mRNA:
1
2
3
4
5
6
7
8
9
10
[INFO] Analyzing lncRNA:
1
2
3
4
5
6
7
8
9
10
[INFO] Analyzing entropy
[INFO] Selecting the edges by the maximum entropy method
[INFO] Classifying mRNA:
1
2
3
4
5
6
7
8
9
10
[INFO] Classifying lncRNA:
1
2
3
4
5
6
7
8
9
10
[INFO] Filtering the graphs
[INFO] Extracting measurements from graphs
[INFO] Building the dataframes
[INFO] Sorting with Randomforest

Call:
 randomForest(x = DF, y = as.factor(data[, 11])) 
               Type of random forest: classification
                     Number of trees: 500
No. of variables tried at each split: 3

        OOB estimate of  error rate: 20%
Confusion matrix:
       lncRNA mRNA class.error
lncRNA      9    1         0.1
mRNA        3    7         0.3
``` 

Além da classificação das sequências de RNA, é possível obter a curva da entropia e verificar onde ocorre o valor de corte entre as arestas. O exemplo abaixo ilustra essa aplicação:

```{R}
mRNA <- system.file("extdata", "mRNA.fasta", package = "BASiNETEntropy")
lncRNA <- system.file("extdata", "ncRNA.fasta", package = "BASiNETEntropy")

trainingresult <- BASiNETEntropy::training(mRNA, lncRNA)

n_mRNA <- 4; n_lncRNA <- 5; n_treshold <- 2
entropymeasures<-trainingresult[[4]][4]
entropythreshold<-trainingresult[[4]][2]

BASiNETEntropy::curveofentropy(entropymeasures,entropythreshold)
``` 

A seguinte saída é esperada

![CE](/img/entropy.png)

A curva de soma de entropia refere-se a classe de mRNA, o threshold no ponto 986 é encontrado. Portanto, as arestas referentes aos pontos de 1 a 986 serão selecionadas e o restante será descartado.

---
Outras aplicações são possíveis utilizando o pacote, sinta-se livre para explorá-lo :smile:.
