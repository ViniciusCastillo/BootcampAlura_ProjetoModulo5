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
1. Existe um campo demográfico 

Como a função Normalizer tinha resultados piores em todos os modelos, eu desconsiderei ela nos testes apresentados


