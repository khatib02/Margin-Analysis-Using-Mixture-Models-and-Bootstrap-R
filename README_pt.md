# Segmentação de Rentabilidade e Risco no Varejo

## Visão Geral

Este projeto analisa pedidos de um conjunto de dados de vendas no varejo. O objetivo é entender o que influencia a margem de lucro e separar pedidos de alto risco dos mais estáveis.

## Por que isso importa

Negócios do varejo perdem dinheiro ao aplicar descontos ou políticas de envio sem conhecer o impacto. Este projeto mostra padrões que ajudam a reduzir perdas e melhorar a margem.

## O que foi feito

- Limpeza e estruturação do conjunto de dados  
- Criação de variáveis relacionadas a localização, categoria, envio e descontos  
- Testes com múltiplos modelos:  
  - Lasso/Ridge (modelo base, ajuste ruim)  
  - GAMLSS com distribuição t (melhor ajuste, mas resíduos bimodais)  
  - XGBoost / LightGBM (alta acurácia, baixa interpretabilidade)  
  - Modelo final: Mistura de Regressões Lineares Gaussianas com modelo concomitante  

## Principais Resultados

Dois grupos claros de pedidos:

- **Cluster 1 (Alto Risco)**: Margens baixas, perdas frequentes  
  - Participação nos pedidos: 31,4%  
  - Participação nas margens negativas: 40%  
  - Margem média: -13,2%  

- **Cluster 2 (Estável)**: Margens mais altas e consistentes  
  - Participação nos pedidos: 68,6%  
  - Margem média: 23,5%  

Esses grupos ajudam a empresa a entender onde está perdendo dinheiro e onde está indo bem.

## Impacto no Negócio

- Os pedidos do Cluster 1 geram um total de **R$ 677** em perdas no período.  
- Uma mudança de política direcionada a esse grupo poderia reduzir as perdas em aproximadamente **67,86%**.  
- Os principais fatores de custo no Cluster 1 são:  
  ![Gráfico de Drivers Cluster 1](https://github.com/user-attachments/assets/77b90099-1e1a-48c0-b982-cf5410c14274)

## O que fazer com isso

- Revisar todas as regras de desconto  
- Reavaliar a estratégia de precificação para Mesas, Estantes, Suprimentos e Máquinas  
- Marcar pedidos de risco antecipadamente usando as probabilidades do modelo  

## Validação do Modelo

- O algoritmo EM foi estável após cerca de 10 reinicializações aleatórias  
- Validação via bootstrap com 1000 reamostragens  
- Métricas de desempenho:  
  - RMSE (fora da amostra): 0.06713472  
  - R² (fora da amostra): 0.9786957  

## Ferramentas Utilizadas

- Linguagem: R  
- Modelagem: flexmix, gamlss, xgboost, lightgbm, glmnet  
- Visualização: ggplot2  
- Computação paralela: foreach, doParallel  

## Visualizações

**1. Trade-off risco vs. retorno entre clusters**  
Mostra a diferença entre a margem esperada e a probabilidade de perda entre os dois clusters.  
![Risk vs Margin](https://github.com/user-attachments/assets/a5e49e1f-9626-4335-a656-da1c601d3495)

**2. Fatores operacionais de alta performance**  
Mostra as variáveis mais associadas ao cluster estável e de alta margem.  
![Variable Importance](https://github.com/user-attachments/assets/d2cfe6df-1e74-463e-9f5a-f202b0a6645b)

**3. 10 níveis mais impactantes por cluster**  
Mostra os níveis de variáveis com maior impacto na performance de margem por cluster.  
![Top 10 Levels](https://github.com/user-attachments/assets/8c4b4905-fea5-45c6-8ab4-57ea3ef7bd52)

**4. Comparação de resíduos entre modelos**  
Mostra como o modelo misto lida melhor com caudas da distribuição do que um modelo linear padrão.  
![Residuals](https://github.com/user-attachments/assets/d7c83df4-82e9-4a70-8e0d-146c371fc4f6)

**5. Validação via bootstrap**  
Mostra a estabilidade do modelo em diferentes subconjuntos de dados.  
![Bootstrap RMSE](https://github.com/user-attachments/assets/9dfbd59b-5bec-4e46-861d-c75ad4a9ab53)

## Considerações Finais

Este projeto mostra como a modelagem estatística pode apoiar decisões reais de negócio. O foco está em clareza, confiabilidade e ação.
