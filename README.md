# Home Credit - Credit Risk Model Stability
**O objetivo desta competição é prever quais clientes são mais propensos a não pagarem seus empréstimos**

### Relatório Executivo (Insights e eficácia)
Neste gráfico podemos avaliar a importância de cada fator para a eficiência do modelo, de modo que fatores mais importantes podem ser melhor registrados, ou terem uma validação melhor de modo que futuros modelos tenham uma melhor eficácia

![image](https://github.com/user-attachments/assets/e3ed2f09-76e5-4dbd-96e8-25136d6e7b77)

Fiz um outro modelo utilizando apenas dados de treino e vemos como características que não estavam nos dados de teste podem fazer grande diferença no modelo, neste exemplo o fator district se mostrou ser um grande influenciador do modelo.

![image](https://github.com/user-attachments/assets/6e326859-d812-4df7-a7f3-3f00c6206a0b)


#### Métricas no conjunto de treino:

AUC: 0.7589

Accuracy: 0.9671

F1-score: 0.0115

Precision: 1.0000

Recall: 0.0058

#### Conclusões a partir das métricas:

**1. Desequilíbrio de classes é forte**
- O F1-score muito baixo (0.0115), mesmo com precisão perfeita (1.0000), indica que o modelo quase nunca acerta casos positivos (classe minoritária).

- O Recall muito baixo (0.0058) significa que praticamente todos os casos positivos são ignorados.

- A acurácia alta (0.9671) pode ser enganosa nesse cenário: provavelmente a classe negativa (maioritária) domina e o modelo acerta a maioria só por sempre prever "negativo".

- Reecomenda-se futuramente usar algum método para utilizar mais targets 1 e menos targets 0 de modo a balancear melhor os dados.

**2. O AUC (0.7589) é razoável**
- Isso sugere que o modelo consegue distinguir as classes até certo ponto, ou seja, o score de probabilidade tem alguma capacidade discriminativa.

- AUC mede separação, não decisão final. Isso mostra que talvez, ajustando o limiar de decisão, o modelo possa melhorar bastante, por padrão é 0.5.

![image](https://github.com/user-attachments/assets/e0662042-1f06-4fd5-a450-f67711534f1d)



### Relatório Técnico (Deciões e futuras melhorias do modelo)

- Os dados utilizados são provenientes de todas as bases com exceção da base debitcard, pois não encontrei informações relevantes para o modelo

- Utilizei apenas os case_ids que vão até o número 100 mil, de modo que fosse possível manipular as bases sem grandes problemas de uso de RAM

- Aplicar uma função que converta cada categoria para o menor tipo possível é uma boa prática, no entanto, esta função seria rodada após o carregamento da base, não fazendo tanta diferença para meu modelo

- Casos de um mesmo case_ids com diversas linhas referentes as mesmas características foram removidos, baseado na regra keep = 'first', isto é mantém-se o primeiro.

- Para uma melhor performance do modelo, utilizar agregações de modo que não se perca tanta informação. Em caso de dados numéricos pode-se usar: min, max, média, mediana, first, last.
  E em caso de dados categóricos usar: first, last, ou modo

- Remover categorias com poucas informações, ou seja algo em torno de 90% a 95% de dados faltantes, pode ser uma boa prática para aumentar a simplicidade e eficiência do modelo.

- Verifiquei que a base de treino e teste tinhas colunas desiguais, isto é, que existia em uma e não na outra, então removi-as de modo a ter dois datasets com as mesma colunas de características para utilizar o modelo.

- Ao fim utilizei random_search para otimizar meus paâmetros para o modelo Light GBM, em virtude de sua velocidade, utilizar outros modelos pode ser interessante.

- O modelo usado foi o Light GBM, em virtude dos seus grandes resultados com problemas de classificação, utilizar XGBoost ou CatBoost serias opções também com bom prospecto neqste tipo de problema.





