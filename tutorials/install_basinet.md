# BASiNET - Tutorial de instalação

BASiNET é um pacote em R disponível no repositório CRAN destinado inicialmente para a classificação de sequências biológicas de RNA. Através do pacote BASiNET é possível realizar a classificação de sequências de RNA codificante (mRNA), longo não codificante (lncRNA) e curto não codificante (sncRNA). Além da classificação também é possível realizar o treinamento e salvar o modelo para análises/classificação posteriores.  
A instalação do pacote é feita através do comando 
`install.packages` no próprio console do R. Um dos desafios da instalação são as depências necessárias para a instalação/utilização do pacote BASiNET.  
Este tutorial traz um guia amigável para iniciantes, com informaçõs detalhadas sobre como instalar o pacote BASiNET sem ter qualquer conhecimento técnico.  

__Este tutorial foi desenvolvido para o sistema operacional Linux, em particular distribuições Ubuntu 22.04, além do usuário necessitar privelégios de administrador para a instalação dos pacotes__ 

## Instalação do R
### Etapa 1: Atualização do sistema
Abra o terminal e digite os seguintes comandos:

```{bash}
sudo apt update
sudo apt -y upgrade
```

### Etapa 2: Instalação do R
Ainda no terminal, digite o seguinte comando para a realizar a instalação da versão `base` do R. Essa versão contém as bibliotecas fundamentais para o desenvolvimento das atividades.

```{bash}
sudo apt -y install r-base
```

### Etapa 3: Abrindo o console do R
Após a instalação do pacote `r-base` é possível acessar o console do R digitando no terminal o comando
```{bash}
R
```
Dessa forma é esperado que a seguinte tela apareça
```{bash}
R version 4.1.2 (2021-11-01) -- "Bird Hippie"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R é um software livre e vem sem GARANTIA ALGUMA.
Você pode redistribuí-lo sob certas circunstâncias.
Digite 'license()' ou 'licence()' para detalhes de distribuição.

R é um projeto colaborativo com muitos contribuidores.
Digite 'contributors()' para obter mais informações e
'citation()' para saber como citar o R ou pacotes do R em publicações.

Digite 'demo()' para demonstrações, 'help()' para o sistema on-line de ajuda,
ou 'help.start()' para abrir o sistema de ajuda em HTML no seu navegador.
Digite 'q()' para sair do R.
```

### Etapa 4: Utilizando o R
Agora é possível digitar comandos e obter saídas através do console R. Para sair e fechar basta digitar `quit()` e confirmar se deseja salvar o workspace, caso não queira digite `n`.

## Instalação das dependência do BASiNET

O BASiNET depende de diversos pacotes, alguns já estão instalados juntamente com a versão `base` do R, outros precisamos realizar a instalação separadamente. Dentre os pacotes necessários para o funcionamento do BASiNET está o pacote [`rJava`](https://cran.r-project.org/web/packages/rJava/index.html) que depende da instalação da biblioteca de desenvolvedor do Java, o [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/downloads/). Para isso precisamos voltar ao nosso terminal para realizar a instalação (se necessário) do pacote em nosso sistema operacional.  
__Nota: Em alguns casos não é necessário a instalação do JDK, necessitando somente a instalação do [Java Runtime Environment (JRE)](https://www.java.com/pt-BR/download/manual.jsp)__  

### Instalação do Java

Para a instalação do JDK/JRE no sistema operacional precisamos abrir o terminal e digitar os comandos para realizar a atualização dos repositórios do sistema e atualizar pacotes (se necessário)

```{bash}
sudo apt update
sudo apt -y upgrade
```  

Após a execução dos comandos acima, verificamos se possuímos o Java instalado.

```{bash}
java -version
```

Se o Java não estiver instalado, uma mensagem parecida com essa será exibida.
```{bash}
Command 'java' not found, but can be installed with:

sudo apt install default-jre              # version 2:1.11-72build1, or
sudo apt install openjdk-11-jre-headless  # version 11.0.14+9-0ubuntu2
sudo apt install openjdk-17-jre-headless  # version 17.0.2+8-1
sudo apt install openjdk-18-jre-headless  # version 18~36ea-1
sudo apt install openjdk-8-jre-headless   # version 8u312-b07-0ubuntu1
```


Execute os seguintes comandos para realizar a instalação das biblitecas Java

```{bash}
sudo apt -y install default-jre
```

Verifique se a instalação ocorreu corretamente através do comando

```{bash}
java -version
```

É esperado uma mensagem similar a

```{bash}
openjdk version "11.0.15" 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1, mixed mode, sharing)
```

Para realizar a instalação do JDK digite

```{bash}
sudo apt -y install default-jdk
```

Verifique se a instalação ocorreu corretamente através do comando

```{bash}
javac -version
```

É esperado uma mensagem similar a

```{bash}
javac 11.0.15
```

Parabéns! O Java foi instalado corretamente.

### Instalação do BiocManager (Bioconductor)

Para a leitura dos arquivos FASTA o pacote BASiNET tem como depência o pacote [biostrings](https://bioconductor.org/packages/release/bioc/html/Biostrings.html), que é disponibilizado pelo [Bioconductor](https://bioconductor.org/).  
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

### Instalação das demais dependências

As demais depências são instaladas diretamente no console R através dos comandos abaixo

```{R}
install.packages("RWeka")
install.packages("rJava")
install.packages("igraph")
install.packages("randomForest")
install.packages("rmcfs")
```

__Esta etapa pode levar um tempo devido a instalação dos pacotes__

## Instalação do BASiNET

Após a instalação de todas as depências, ainda no console R digite

```{R}
install.packages("BASiNET")
```

## Utilização do BASiNET
Para carregar o pacote BASiNET no console do R digite
```{R}
library("BASiNET")
```

A função principal é a `classification` que aplica a metodologia proposta no artigo para a classificação das sequências de RNA. Ao fim da execução o resultado da classificação é obtido.  
Os parâmetros da função são os seguintes:  
* word: Define o número de bases nitrogenadas que formarão uma palavra. Por padrão o parâmetro word é definido como 3;  
* step: Define a distância que será percorrida na sequência para a formação de uma nova conexão, em outras palavras é o tamanho da janela deslizante. Por padrão o parâmetro step é definido como 1;
* mRNA: Diretório do arquivo FASTA contendo sequências de mRNA;  
* lncRNA: Diretório do arquivo FASTA contendo sequências de lncRNA;  
* sncRNA: Diretório do arquivo FASTA contendo sequências de sncRNA;  
* graphic: Se `TRUE` é considerado para a geração dos gráficos em relação aos valores de threshold e as medidas. Requer tempo de processamento e dependências internas do `igraph`;  
* classifier: O classificador `J48` (árvore de decisão) é definido por padrão, caso o usuário opte por utilizar o classificador `randomForest` deve-se utilizar o parâmetro definido como `classifier = "RF"`. A predição com um modelo já treinado funciona somente com o parâmetro definido como `J48`, isto é, em sua definição padrão;  
* load: Nome do arquivo `.dat` que será carregado como modelo para a predição de novas sequências de RNA. Por padrão é definido como `NULL`;  
* save: Nome do arquivo `.dat` no qual o modelo treinado do classificador será salvo. O arquivo gerado poderá ser utilizado pelo parâmetro `load` para a predição de novas entradas. Por padrão é definido como `NULL`.

```{R}
classification(mRNA, lncRNA, word = 3, step = 1, sncRNA, graphic, classifier = c("J48", "RF"), load, save)
```

Um exemplo básico de utilização do pacote é dado através dos comandos:
```{R}
mRNA <- system.file("extdata", "sequences2.fasta", package = "BASiNET")
lncRNA <- system.file("extdata", "sequences.fasta", package = "BASiNET")
classification(mRNA,lncRNA)
``` 

A saída esperado do comando é a seguinte:
```{R}
Analyzing mRNA from number: 
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
Analyzing lncRNA from number: 
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
11
Rescaling values
Creating data frame
Sorting the data with the J48
J48 pruned tree
------------------

MAX.6 <= 0: lncRNA (11.0)
MAX.6 > 0: mRNA (10.0)

Number of Leaves  : 	2

Size of the tree : 	3

=== 10 Fold Cross Validation ===

=== Summary ===

Correctly Classified Instances          20               95.2381 %
Incorrectly Classified Instances         1                4.7619 %
Kappa statistic                          0.9041
K&B Relative Info Score                 90.474  %
K&B Information Score                   19.0262 bits      0.906  bits/instance
Class complexity | order 0              21.0295 bits      1.0014 bits/instance
Class complexity | scheme             1074      bits     51.1429 bits/instance
Complexity improvement     (Sf)      -1052.9705 bits    -50.1415 bits/instance
Mean absolute error                      0.0476
Root mean squared error                  0.2182
Relative absolute error                  9.5238 %
Root relative squared error             43.6012 %
Total Number of Instances               21     

=== Detailed Accuracy By Class ===

                 TP Rate  FP Rate  Precision  Recall   F-Measure  MCC      ROC Area  PRC Area  Class
                 0,900    0,000    1,000      0,900    0,947      0,908    0,950     0,948     mRNA
                 1,000    0,100    0,917      1,000    0,957      0,908    0,950     0,917     lncRNA
Weighted Avg.    0,952    0,052    0,956      0,952    0,952      0,908    0,950     0,931     

=== Confusion Matrix ===

  a  b   <-- classified as
  9  1 |  a = mRNA
  0 11 |  b = lncRNA
```

Um outro exemplo de aplicação é quando um modelo já treinado é salvo, podendo ser utilizado através do parâmetro `load`. O exemplo abaixo ilustra uma aplicação e está disponível no pacote.

```{R}
mRNApredict <- system.file("extdata", "sequences2-predict.fasta", package = "BASiNET")
lncRNApredict <- system.file("extdata", "sequences-predict.fasta", package = "BASiNET")
modelPredict <- system.file("extdata", "modelPredict.dat", package = "BASiNET")
classification(mRNApredict,lncRNApredict,load=modelPredict)
```

Uma saída similar a essa é esperada:
```{R}
Analyzing
Rescaling values
Creating data frame
Results
 [1] mRNA   mRNA   mRNA   mRNA   mRNA   lncRNA mRNA   mRNA   mRNA   mRNA  
[11] mRNA   lncRNA lncRNA lncRNA lncRNA lncRNA lncRNA lncRNA lncRNA lncRNA
[21] lncRNA lncRNA
Levels: mRNA lncRNA
```

---
Outras aplicações são possíveis utilizando o pacote, sinta-se livre para explora-lo :smile:.