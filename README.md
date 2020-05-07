# TesteLopesLAB
Análise dos dados de vinho português
a) Como foi a definição da sua estratégia de modelagem? 
O objetivo dessa análise é classificar a qualidade do vinho (variável resposta), numa escala de 3 a 9, dadas as seguintes variáveis independentes:
-Type; Ácido fixo; volatildade da acidez; Ácido Cítrico; Açucar residual; Cloretos; dioxido de Enxofre Livre; Dióxido de Enxofre Total; Densidade; ph;Sulfatos e Álcool. 
Após a análise exploratória de dados, pode-se identificar algumas relações entre as variáveis independentes e a qualidade do vinho (quality). Com isso, podemos pensar a princípio em um modelo de regressão mútipla, com resposta normal ou binária. No modelo binário, a variável resposta poderia ser categorizada apenas em dois níveis (0-baixa qualidade, 1 - alta qualdiade).  No modelo normal, a resposta não segue distribuição normal. Como a variável resposta é categórica e ordinal, um modelo proposto é o Modelo de Regressão Logística Ordinal. 
b) Como foi definida a função de custo utilizada?
O modelo de regressão ordinal pode ser representado da seguinte forma:
Log(oddsY) = ai + b1X1 + b2X2 +...+ bpXn ,
onde
Y é a variável resposta ordinal (3,4,5,6,7,8,9);
i é o número de categorias
X1, X2, .... Xn são variáveis independentes (categoricas ou contínuas)
ai,b1,b2,...,bp são parâmetros estimados
No R: model1 <- polr(qualidade ~ type+fixed.acidity+volatile.acidity+citric.acid+residual.sugar+chlorides+free.sulfur.dioxide+total.sulfur.dioxide+density+pH+sulphates +alcohol, Hess=TRUE).
Para interpretar as estimativas dos coeficientes da regressão, foi calculada a razão de chances (odds ratio).
c)Qual foi o critério utilizado na seleção do modelo final?
Após o ajuste do modelo completo, as variáveis independentes não significativas foram: Ácido fixo,  Ácido Cítrico e Densidade. Retirando essas variáveis, o novo modelo é:
model2 <- polr(y ~ type+volatile.acidity+residual.sugar+chlorides+total.sulfur.dioxide+free.sulfur.dioxide +pH+sulphates+alcohol, Hess=TRUE)
Para verificar o melhor modelo foi ultilizado o critério AIC, onde
AIC(model1)=14131 > AIC(model2)=14128.
Então o modelo selecionado foi o "model2".
d)Qual foi o critério utilizado para validação do modelo? Por que escolheu utilizar este método?
Para analisar a validação do modelo, construiu-se uma tabela da matriz de confusão, onde podemos observar o nível de acerto entre a classificação predita pelo modelo(coluna) e o observado, porém nos níveis 3,4,8 e 9 podemos notar má predição, no qual pode indicar problemas na classificação nesses determinados grupos.
 Quais evidências você possui de que seu modelo é suficientemente bom?
 Usando a matriz de confusão, o erro de classificação incorreta para o nosso modelo é de 45,27%. Porém,  a regressão logística ordinal é útil ao lidar com uma variável dependente que pode ser ordenada. 
