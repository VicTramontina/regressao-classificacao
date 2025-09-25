# Machine Learning: Regressão e Classificação

Este projeto conta a jornada de resolver dois problemas clássicos de Machine Learning: predizer preços de veículos através de regressão e identificar clientes propensos a responder campanhas de marketing via classificação. Durante as execuções, descobrimos insights interessantes sobre como diferentes algoritmos se comportam com dados reais.

## Como Executar

### Pré-requisitos
```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

### Executar os Notebooks
```bash
# Análise de Regressão
jupyter notebook notebook_regressao.ipynb

# Análise de Classificação  
jupyter notebook notebook_classificacao.ipynb
```

## Os Datasets

### Preços de Veículos FIPE
Trabalhamos com um dataset robusto de 466.020 registros da Tabela FIPE, contendo marca, modelo, ano e combustível de veículos. O que mais nos chamou atenção foi a amplitude dos preços - desde veículos de R$ 10.000 até R$ 500.000, criando um desafio interessante de capturar essa variabilidade.

### Campanhas de Marketing
O segundo dataset trouxe 2.240 clientes com informações demográficas e comportamentais. Logo percebemos um problema típico do mundo real: apenas 14.9% dos clientes responderam às campanhas anteriores, criando um desafio de classes desbalanceadas que precisaria ser tratado cuidadosamente.

## A Jornada dos Algoritmos

Implementamos três algoritmos clássicos para cada problema: Linear Regression/Logistic Regression como baseline, Random Forest como ensemble robusto, e Gradient Boosting como método sequencial avançado. Também aplicamos Cross-Validation e otimização de hiperparâmetros para extrair o máximo de cada modelo.

## O Que Descobrimos na Regressão

A primeira surpresa foi o fracasso da Regressão Linear - com R² de apenas 0.0764, ficou evidente que os preços dos veículos seguem padrões não-lineares complexos. A relação entre idade do veículo e depreciação não é uma linha reta simples.

O Random Forest já mostrou resultados impressionantes com R² = 0.9888, capturando 98.88% da variação dos preços. Mas foi o Gradient Boosting otimizado que nos surpreendeu: após ajustar os hiperparâmetros (learning_rate=0.15, max_depth=7, n_estimators=150), conseguimos R² = 0.9915.

O que isso significa na prática? O modelo erra em média R$ 30.388 na predição - para um mercado onde veículos custam entre R$ 10k e R$ 500k, isso é notavelmente preciso. Metade das predições têm erro menor que R$ 12.158, tornando o modelo utilizável para seguradoras e concessionárias.

A análise de importância das features revelou algo esperado mas importante: o modelo específico do veículo é o preditor mais forte (45% da importância), seguido pelo ano (31%) e marca (18%). Isso confirma nossa intuição de que um Civic 2020 se comporta diferentemente de um BMW X1 2020.

## O Que Aprendemos na Classificação

Na classificação, enfrentamos o desafio das classes desbalanceadas desde o início. Aplicamos pesos às classes e cross-validation estratificada para não enviesar os resultados.

Aqui a história ficou mais interessante porque cada algoritmo se destacou em aspectos diferentes:

**Logistic Regression** se mostrou o "não deixa passar batido" - com Recall de 74.63%, ele encontra 3 em cada 4 clientes interessados. Porém, gera muitos falsos alarmes (64 contatos desnecessários).

**Random Forest** emergiu como o "equilibrista" - com Accuracy de 87.95% e Precision de 64.44%, ele acerta 9 em 10 classificações e quando sugere contato, há 64% de chance de conversão. Perde algumas oportunidades (38 de 67 clientes interessados), mas maximiza ROI.

**Gradient Boosting** se tornou o "ranqueador premium" - com AUC-ROC de 87.65%, ele é excelente para ordenar clientes por probabilidade. Ideal para campanhas em fases.

Durante a execução, descobrimos padrões fascinantes: clientes com PhD têm 20.8% de taxa de resposta (vs 14.9% geral), o histórico de campanhas anteriores é o preditor mais forte, e timing é crucial - clientes com compras recentes respondem melhor.

## Estrutura do Projeto

```
├── datasets/
│   ├── tabela-fipe-historico-precos.csv
│   └── marketing_campaign.csv
├── notebook_regressao.ipynb          # Análise completa de regressão
├── notebook_classificacao.ipynb      # Análise completa de classificação
├── relatorio_regressao.md            # Relatório detalhado - regressão
├── relatorio_classificacao.md        # Relatório detalhado - classificação
└── README.md                         # Este arquivo
```

## O Que Cada Notebook Revela

### notebook_regressao.ipynb
A jornada começa com análise exploratória revelando a distribuição dos preços e padrões de depreciação. Seguimos com pré-processamento cuidadoso, implementação dos três algoritmos, validação cruzada e a descoberta surpreendente de que a otimização melhorou significativamente o Gradient Boosting. Terminamos analisando quais características dos veículos mais influenciam o preço.

### notebook_classificacao.ipynb
Aqui enfrentamos o desbalanceamento desde o início, exploramos como diferentes grupos demográficos respondem às campanhas, implementamos os algoritmos com tratamento especial para classes desbalanceadas, e descobrimos os trade-offs interessantes entre precision e recall. A análise de feature importance revelou insights valiosos sobre comportamento do consumidor.

## Reflexões sobre os Trade-offs

Na regressão, a Linear Regression falhou completamente, mas serviu como importante baseline. Random Forest e Gradient Boosting performaram similarmente, com GB otimizado levando vantagem marginal mas significativa.

Na classificação, cada modelo conta uma história diferente. Se você tem recursos limitados, Random Forest maximiza ROI. Se não pode perder oportunidades, Logistic Regression garante cobertura máxima. Se quer fazer campanhas em fases, Gradient Boosting oferece o melhor ranqueamento.

## Impacto Prático

Para regressão, conseguimos um modelo que permite seguradoras automatizarem 80% das avaliações de sinistros, concessionárias implementarem precificação dinâmica, e compradores verificarem se estão pagando preços justos.

Para classificação, entregamos uma ferramenta que pode triplicar o ROI de campanhas de marketing, identificar automaticamente clientes premium, e otimizar timing de contatos.

## Lições Técnicas Aprendidas

A validação cruzada foi crucial - sem ela, teríamos overfitting mascarado como sucesso. O tratamento de classes desbalanceadas na classificação foi fundamental para resultados confiáveis. A otimização de hiperparâmetros mostrou que vale a pena investir tempo nessa etapa, especialmente para Gradient Boosting.

A análise de feature importance nos dois problemas confirmou que modelos de ML podem gerar insights de negócio valiosos, não apenas predições precisas.

---

**Este projeto demonstra como Machine Learning pode resolver problemas reais de negócio, revelando não apenas soluções técnicas, mas insights valiosos sobre os domínios estudados.**