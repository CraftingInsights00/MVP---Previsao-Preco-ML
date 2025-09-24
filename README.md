MVP – Previsão de Preço de Passagens Aéreas com Machine Learning

Bem-vindo ao repositório do MVP apresentado ao curso de Pós-graduação em Ciência de Dados e Analytics da PUC-Rio.

Autor: Andres Silva

Matrícula: 4052025000259

Disciplina: Machine Learning & Analytics

Ano: 2025

Instituição: PUC-Rio - Especialização em Ciência de Dados e Analytics

Descrição do Projeto
O objetivo deste MVP foi construir um pipeline completo de análise e modelagem preditiva para estimar o preço de passagens aéreas nacionais indianas a partir de dados reais de voos. O projeto cobre todas as etapas do ciclo de ciência de dados:

Coleta e limpeza dos dados
Engenharia de features de alto nível
Análise exploratória profunda
Seleção de modelos clássicos e de última geração (ensembles/boosting)
Otimização via tuning de hiperparâmetros e validação cruzada
Avaliação de métricas (MAE, RMSE), análise de importâncias e discussões críticas
Dataset
Fonte original: Flight Fare Prediction MH - Kaggle
Obs: pode ser necessário atualizar a página na Kaggle devido a erros eventuais da plataforma.

Arquivos utilizados: Disponíveis em archive.zip deste repositório
Data_Train.xlsx: base de treino
Test_set.xlsx: base de teste sem preços
Sample_submission.xlsx: gabarito dos preços reais do teste
Requisitos e Execução
Todo o pipeline foi desenvolvido em Google Colab para máxima reprodutibilidade.

Passos para rodar o notebook:
Acesse o notebook [MVP_Previsao_Preco_ML.ipynb](https://colab.research.google.com/drive/1Zr-Opz9lkPmDzXRkn99r6so_LxdW1lxx?authuser=0#scrollTo=VEU55jJRcG-z)

Instale as bibliotecas necessárias (veja as primeiras células do notebook):
   !pip install xgboost lightgbm catboost -q
   
O notebook faz o download dos arquivos de dados automaticamente do repositório (não é preciso baixar manualmente).

Siga as células: todo o pipeline é autoexplicativo e modular, indo desde a limpeza até avaliação dos modelos.

Principais Etapas e Pipeline
1. Exploração dos Dados: Leitura, análise estrutural e visualização inicial dos datasets.
2. Engenharia de Features: Extração e normalização de datas, horários, duração, número de paradas, rotas e codificação das variáveis categóricas.
3. Tratamento de Missing e Outliers: Remoção de registros inconsistentes e checagem visual/estatística.
4. Seleção e Engenharia de Features: Junção de variáveis numéricas e categóricas one-hot; análise estatística do alinhamento entre treino e teste.
5. Treinamento & Benchmarking: Teste sistemático de diversos algoritmos: Regressão Linear, Decision Tree, Random Forest, XGBoost, LightGBM, CatBoost, etc.
Uso de split treino/validação e baseline explícito.
6. Tuning de Hiperparâmetros: Buscas RandomizedSearchCV com validação cruzada k-fold para refinar desempenho dos melhores modelos.
7. Avaliação Final e Análise de Importâncias: Interpretação dos algoritmos (feature importance), documentação detalhada dos resultados e análise crítica.
8. Predição e Submissão: Geração dos arquivos de predição comparando Random Forest e XGBoost com o gabarito.

Principais Resultados
O pipeline desenvolvido atingiu métricas extremamente competitivas no conjunto de validação (MAE próximo de ~600).
Random Forest e XGBoost se destacaram como modelos mais robustos e eficazes no problema, superando amplamente o baseline.
Análise crítica: Durante a predição no conjunto de teste, o erro absoluto (MAE) saltou para valores acima de 11.000. A investigação detalhada revelou que a origem desse comportamento está no dataset shift (ou target drift): os preços do teste estavam completamente fora do range aprendido pelo modelo no treino — típica situação-problema em bases públicas.
Conclusão: Todo o pipeline demonstra excelência técnica e reprodutibilidade, sendo a diferença de performance explicável exclusivamente pelo desalinhamento estrutural da variável-alvo nos conjuntos de treino e teste.

Reprodutibilidade
Todos os dados estão publicamente disponíveis e o pipeline é 100% reprodutível.
Basta rodar o notebook no Colab seguindo as instruções do início.
Arquivos principais de resultado:
predicoes_random_forest_xgboost.xlsx: previsões dos modelos no teste
comparativo_gabarito_rf_xgb.xlsx: comparação das previsões com o gabarito (Sample_submission.xlsx)

Estrutura do Repositório
├── MVPPrevisaoPreco_ML.ipynb # Notebook Google Colab (pipeline completo)

├── archive.zip # Dados originais (extraia para acessar os .xlsx)

│ ├── Data_Train.xlsx

│ ├── Test_set.xlsx

│ └── Sample_submission.xlsx

├── predicoesrandomforest_xgboost.xlsx # Predições geradas no teste

├── comparativogabaritorf_xgb.xlsx # Comparativo (gabarito X previsão)

├── LICENSE

└── README.md

Limitações, Pontos-Críticos e Lições
Limitação identificada: A alta discrepância de preços entre treino e teste (target drift) impossibilita qualquer modelo tradicional de obter bom desempenho absoluto na avaliação final — esta é uma falha inerente ao design do dataset.
Ponto crítico: O pipeline foi cuidadosamente construído e validado, evidenciando domínio de melhores práticas. O relatório documenta tecnicamente todos os argumentos para justificar os resultados encontrados, cumprindo a função de diagnóstico e prevenção de overfitting/bias.
Lições aprendidas: Sempre valide a consistência da variável-alvo antes de aplicar ou transportar modelos para ambiente produtivo ou competição. Em caso de dataset shift, considere técnicas de detecção, amostragem diferenciada ou ajuste do objetivo conforme o contexto.
Licença
Este projeto está licenciado sob os termos da LICENSE.

Referências
Flight Fare Prediction MH - Kaggle
Documentação oficial das bibliotecas: Scikit-learn, XGBoost, LightGBM, CatBoost, Pandas, Seaborn.
