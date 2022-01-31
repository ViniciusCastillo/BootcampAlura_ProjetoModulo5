# BootcampAlura_ProjetoModulo5
## Previsão quais pacientes precissarão ser admitidos na UTI devido a Covid-19
![image](https://torresvedrasweb.pt/abc/uploads/2021/10/20200319-114657-covid192.jpg)

Este projeto teve o objetivo de encontrar o modelo que melhor preve quem precisará de UTI com base nos dados no desafio do [Kaggle do Sírio Libanes](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19). Conseguir prever com antecedência é muito importante, por isso o foco foi conseguir ter uma boa previsibilidade logo no primeiro atendimento, com base nas medições da primeira janela horária do paciente no hospital.

Testei alguns modelos de Regressão Logística, Random Forest e ..... Também testei qual seria o melhor filtro na seleção de dados, bem como a melhor forma de reescalar os dados.

**Após diversos teste, vou recomendar o modelo que obteve os resultados abaixo:**

AUC (Area Under the Curve) da curva ROC (Receiver Operating Characteristic). Uma acurácia de .... e um FPR de ....

Agora irei detalhar um pouco mais como cheguei nesse modelo.

### Tratamento de dados
Os dados utilizados foram os disponibilizados no desafio do [Kaggle do Sírio Libanes](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19). 

Ao analisar esses dados identifiquei a necessidade de alguns tratamentos dos dados:
* Retirar as linhas com marcação de UTI = 1
* Remarcar a coluna ICU (UTI em inglês), com a informação se o paciente visitante (PATIENT_VISIT_IDENTIFIER) chegou na UTI, independente da janela (campo WINDOW)
* Tratando os dados que não estão disponíveis com base na medição anterior ou posterior
  * Caso ainda sobre dados indisponível, as linhas serão excluídas
* Remover as colunas que tem o mesmo valor em todas as linhas da base
* Transformar o campo demográfico 'AGE PERCENTIL' que está em formato de texto
  * Aqui trabalhei com 2 formas diferentes e criei 2 bases para testes:
    * dados_LE utilizando o método  LabelEncoder() do scikit-learn. 
    * dados_OHE utilizando o método  OneHotEncoder() do scikit-learn. 

### Testes para a criação do Pipeline
Nesta parte eu testei alguns formatos, percebi por exemplo que fazer a eliminação das variáveis com alta correlação entre si (mantendo apenas uma delas), bem como retirar as que possuem baixa correlação com a váriavel alvo de UTI, antes de mais nada já melhorava as previsões.

Após isso, normalmente colocar mais uma seleção de dados, utilizando o modelo SelectFromModel, também melhorava as estimativas. Sendo que aqui um dos testes também foi encontrar o melhor paramêtro para o threshold desse modelo.

Outo teste interezande foi se era necessário reescalar os números. Logo de cara eu desonsiderei a função Normalizer por ser evidente que piorava os indicadores,desta forma o teste ficou entre não fazer nada (a base de certa forma já estava ajustada) ou utilizar o modelo StandardScaler.

Por fim o modelo a ser utilizado, testei tanto o Logistic Regression quanto o Random Forest, sendo que em ambos qual a parametrização que melhorava o resultado.

### Contrução do Pipeline
Com o resultado dos testes eu crio o pipeline de melhor perfomance, sendo que considerei o limite inferior do intervalo de confiança de 95% (media - 2 desvios padrões) do ROC AUC como referência.

Com o pipeline criado rodo para uma amostra de teste aleatória os resultados para ter uma referência do resultado. Fora isso, podemos salvar o modelo em um arquivo.
[Aqui você pode encontrar os arquivos criados]().

### Conclusões
Esses testes todos foram feitos tanto na janela de 0-2 quanto na janela de 2-4. 

O melhor modelo da janela de 0-2 foi o ....

Já na janela de 2-4 foi....

As colunas utilizadas foram....

### Próximos passos
Acredito que seria possível testar outros modelos de classificação, dado que só utilizei 2 nos meus testes.

Além disso, na parametrização do modelo acabei utilizando um métrica diferente da comparação dos pipelines, teria que fazer alguns ajustes nos códigos para que ela também fosse utilizada na parte de parametrização, deixando de ser o valor médio e sim o valor inferiro do intervalo de confiança.

Outro ponto que poderia ser melhorado é na hora de retirar as variáveis que tem alta correlação entre si, o certo era manter a que tem maior correlação com a variável y e atualmente está escolhendo conforme a ordem das colunas.

Acredito que esses são os principais pontos e até uma próxima!

### Principais Referências
[Bootcamp Alura](https://bootcamps.alura.com.br/)

[scikit-learn user guide](https://scikit-learn.org/stable/user_guide.html)

[Implementando um Modelo de Classificação no Scikit-Learn](https://tatianaesc.medium.com/implementando-um-modelo-de-classifica%C3%A7%C3%A3o-no-scikit-learn-6206d684b377) - Tatiana Escovedo
