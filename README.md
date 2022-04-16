# Cognitivo.ai
Desafio Cognitivo.ai do Airbnb

# a. Como foi a definição da sua estratégia de modelagem?
Analisando os dados, foi possível perceber que nas 74 colunas, as com o prefixo \_host são relacionado ao locador do imóvel, as com \_review pertencem aos reviews dos usuários em relação a locação e o resto são referentes ao imóvel em sí. Como a variável alvo 'room_type' é do domínio do imóvel, as variáveis que definem bem o imóvel eram as melhores candidatas para a modelagem. Especialmente a variável "property type" que possui valores categóricos muito semelhantes ao da variável alvo.

# b. Como foi definida a função de custo utilizada?
A função de custo utilizada foi a categorical_crossentropy, que é uma função que calcula a diferença entre 2  distribuições de probabilidade (o predito e o alvo). Cada categoria é expressa por um vetor das possíveis categorias e as probabilidades de pertencimentos da amostra em cada categoria é comparado (one_hot vector). Como nesse problema se trata de uma classificação múltipla, essa função de custo é recomendada. No caso foi utilizado a sparse_categorical_crossentropy que faz a mesma coisa só que espera as classes em inteiros ao invés de one-hot enconding como se é esperado na categorical_crossentropy. https://peltarion.com/knowledge-center/documentation/modeling-view/build-an-ai-model/loss-functions/categorical-crossentropy

# c. Qual foi o critério utilizado na seleção do modelo final?
Após a análise do MDI (importância das features) em um classificador de florestas randômicas demonstrar a excelente capacidade de separação dos dados pelas features selecionadas, em especial pela variável "property_type" e por ser um problema de classificação múltipla (1 para n), um modelo com base em rede neural possui menos chances de overfitting que modelos baseados em árvores. Após múltiplos testes com diferente arquiteturas de rede, a melhor arquitetura conseguiu atingir resultados satisfatórios.

# d. Qual foi o critério utilizado para validação do modelo? Por que escolheu utilizar este método?
O método utilizado foi a validação cruzada (10 fold). Esse método foi utilizado por ser capaz de verificar o quão acurado está o modelo de forma mais livre de viés. Também mostra a capacidade de generalização do modelo. Como cada partição do conjunto de dados é treinado e testado em partes diferentes.

# e. Quais evidências você possui de que seu modelo é suficientemente bom?
Depois que o modelo foi concluído, é preciso tirar todas as métricas pertinentes. Precision,Recall, Accuracy e F1-score. Essas métricas e outras como a curva ROC são facilmente calculadas através da matriz de confusão da classificação.

Acurácia média dos 10 folds (cross-validation 10 fold): 85.62% 

Matriz de confusão:
Confusion Matrix :
3688   69  346   18
  16 3392 1259  485
 333    8 2326   29
   1  616  200 3550
   
 Precision: 0.817682432996383
 Recall: 0.7930950048971597
 F1 score: 0.8052010637169696
 
 Como as classes foram balanceadas com o uso do algoritmo SMOTE, a acurácia é representativa. Como o F1-score está próximo da acurácia, a modelagem se mostra consistente.
