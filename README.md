![EPB](/img/EPB_1.png)
# III Escola Paranaense de Bioinformática

## Curso: Extração de características e classificação de sequências de RNAs

### Descrição:
> Nos últimos anos, devido ao surgimento de sequenciadores de alta performance, ocorreu um grande avanço no volume de dados de DNA e RNA. Isso fez com que as ciências “ômicas” entrassem na era do “BIG Data” ou “e-Science”. Atualmente, um enorme volume dados estão disponíveis para análises genômicas (de DNA) e transcriptômicas (de RNA) com aplicações diversas em áreas de conhecimento como melhoramento genético, fitopatologia e fisiologia vegetal. Trabalhos de Associação e/ou Seleção Genômica, transformação genética ou edição genômica, rastreamento e certificação, vem a cada dia utilizando mais e mais as informações “omicas” que despertam novas estratégias, inovadoras e precisas em pesquisa. Entretanto as ferramentas de análise desses dados "ômicos" ainda carecem de uma maior atenção, sendo necessário o desenvolvimento de métodos computacionais que possam selecionar, extrair e classificar as informações para a descoberta de conhecimento.
Este curso irá apresentar este contexto e aplicação do método BASiNET que diferente de vários programas baseados em métodos de alinhamento de sequências, essa metodologia é baseada em modelos de reconhecimento de padrões e extração de características por meio de redes complexas para melhor sintetizar e selecionar as informações relevantes contidas nos dados de RNA-seq. Utiliza o princípio de machine learning, no qual o método, através de um set inicial de dados aprende automaticamente a reconhecer padrões de RNAs e usa esse aprendizado para melhorar a análise e o reconhecimento das carcaterísticas que identificam a classe a que pertence a sequência. Isso permite que tenhamos informações com uma maior precisão e acurácia dos dados gerados, como indicado no artigo publicado na revista Nucleic Acids Research (Ito et al. 2019 doi: [10.1093/nar/gky462](https://doi.org/10.1093/nar/gky462)). O BASiNET apresentou uma assertividade superior a outros programas na identificação e classificação de RNAs (codantes e não codantes) em dados de 13 espécies diferentes, incluindo plantas e animais. Algumas análises comparativas a performance foi superior a 10% na identificação de RNAs. Portanto a utilização do método representa um importante avanço na análise de dados de RNA, auxiliando trabalhos de transcriptoma para identificação de novos genes, análise de expressão gênica, identificação de regiões codantes e não codantes e por consequência estudos epigenéticos. Outro fator importante é a abrangência do método, podendo ser aplicado tanto em dados de RNA de animais como de vegetais. O método BASiNET é de livre acesso estando disponível a todos interessados no site do [CRAN](https://cran.r-project.org/package=BASiNET).

---
## Conteúdo programático
### 08/08/2022
* Apresentação dos conceitos de extração de características de RNA;
* Apresentação do método [BASiNET](https://doi.org/10.1093/nar/gky462)
* Hands on! Instalação e classificação de sequências biológicas utilizando o pacote [BASiNET](https://cran.r-project.org/package=BASiNET)

### 09/08/2022
* Avanços na extração de características de RNA;
* Apresentação do método [BASiNETEntropy](https://arxiv.org/abs/2203.15635)
* Hands on! Instalação e classificação de sequências biológicas utilizando o pacote [BASiNETEntropy](https://CRAN.R-project.org/package=BASiNETEntropy)

### 10/08/2022
* Aplicação dos conceitos de classificação de sequências biológicas
* Avaliação de outros métodos de extração de características e classificação de sequências biológicas

---
## Tutoriais
* Instalação do pacote [BASiNET](/tutorials/install_basinet.md)
* Instalação do pacote [BASiNETEntropy](/tutorials/install_basinetentropy.md)
* Processamento de arquivos [FASTA](/tutorials/fasta_process.md)

---
## Métodos
Abaixo alguns métodos disponíveis para a classificação de RNA. Sinta-se livre para utiliza-los e complementar essa lista com novos métodos :smile: .
* [RNAcon](https://bmcgenomics.biomedcentral.com/articles/10.1186/1471-2164-15-127): Método disponível para a classificação de RNA codificante e não-codificante. Além da classificação binária é possível classificar o tipo de RNA pequeno não codificante. As características selecionadas para o classificador SVM são referentes a composição dos nucleotideos. Disponível em [`/methods/RNAcon/`](/methods/RNAcon/). Execução direta utilizando o guia de uso disponível no arquivo. 
* [PLEK](http://www.biomedcentral.com/1471-2105/15/311): Método disponível para a classificação de RNA codificante e não-codificante. As características selecionadas para o classificador SVM são referentes ao ```k-mers```. Disponível para download em: [https://sourceforge.net/projects/plek/files/](https://sourceforge.net/projects/plek/files/). Tutorial para uso e instalação disponível em: [http://202.200.112.245/plek/installation.html](http://202.200.112.245/plek/installation.html).  
**Etapa de treinamento pode levar tempo segundo autores**
* [CPC2](https://academic.oup.com/nar/article-lookup/doi/10.1093/nar/gkx428): Método disponível para a classificação de RNA codificante e não-codificante. As características selecionadas para o classificador SVM são referentes a ORF (tamanho e integridade). Documentação e download disponível em: [http://cpc2.gao-lab.org/download.php](http://cpc2.gao-lab.org/download.php). Uma versão também está disponível em [`/methods/CPC2/`](/methods/CPC2/).
* [CPPred](https://doi.org/10.1093/nar/gkz087): Método disponível para a classificação de RNA codificante e não-codificante. As características selecionadas para o classificador SVM são referentes a ORF (tamanho, cobertura e integridade). Documentação e download disponível em: [http://www.rnabinding.com/CPPred/](http://www.rnabinding.com/CPPred/). Uma versão também está disponível em [`/methods/CPPred/`](/methods/CPPred/).
* [lncFinder](https://doi.org/10.1093/bib/bby065): Método disponível para a classificação de RNA codificante e não-codificante. As características selecionadas para o classificador SVM são referentes a ORF (tamanho e cobertura). Disponível no CRAN: [https://cran.r-project.org/web/packages/LncFinder/](https://cran.r-project.org/web/packages/LncFinder/). Possui etapa de treinamento através da função ```build_model```.
* [CNIT](https://doi.org/10.1093/nar/gkz400): Método disponível para a classificação de RNA codificante e não-codificante. As características selecionadas para o classificador XGBoost são referentes as triplas de nucleotideos adjacentes. Documentação e download disponível em: [http://cnit.noncode.org/CNIT/download](http://cnit.noncode.org/CNIT/download). Uma versão também está disponível em [`/methods/CNIT/`](/methods/CNIT/).
* [Lncident](https://doi.org/10.1155/2016/9185496): Método disponível para a classificação de RNA codificante e não-codificante. As características selecionadas para o classificador SVM são referentes a ORF (tamanho e cobertura). Documentação e download disponível em: [http://csbl.bmb.uga.edu/mirrors/JLU/Lncident/index.php](http://csbl.bmb.uga.edu/mirrors/JLU/Lncident/index.php). Uma versão também está disponível em [`/methods/Lncident/`](/methods/Lncident/).
---
## Datasets
* [human_gencodev32](https://www.gencodegenes.org/human/release_32.html): Dataset completo contendo todas as sequências de transcritos e de RNA longo não codificante. Disponível em: [`/dataset/HA1/`](/dataset/HA1/)
* [human_gencodev32_process](dataset/preprocessed/): Dataset ```human_gencodev32``` processado e selecionadas algumas sequências para dataset balanceado.
* [human_gencodev38](https://www.gencodegenes.org/human/release_38.html): Dataset completo contendo todas as sequências de transcritos e de RNA longo não codificante. Disponível em: [`/dataset/human_r38/`](/dataset/human_r38/)
* [mouse_gencodev27](https://www.gencodegenes.org/mouse/release_M27.html): Dataset completo contendo todas as sequências de transcritos e de RNA longo não codificante. Disponível em: [`/dataset/mouse_m27/`](/dataset/mouse_m27/)
### Autores
[Fabrício Martins Lopes](https://github.com/fabriciomlopes)  
[Matheus Pimenta](https://github.com/omatheuspimenta)