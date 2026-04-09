# Test A/Bn - Taxa de Cliques no Site

# Introdução
Esse é um projeto de Data Science, focado em Teste A/B, especificamente em Teste A/Bn no qual existem mais de 2 variantes para serem vericadas. No qual foi identificado qual a melhor variante do site
que trouxe mais clicks em determinada feature da página, mostradn oa importância de aplicar esse tipo de teste e suas diferentes vertentes.

## Planejamento
Para a resolução do problema foi utilizado a metodologia CRISP-DM. A metodologia CRISP-DM define o ciclo de vida do projeto, dividino-as nas seguintes etapas:
- Definição do Problema de Negócio
- Compreensão do Negócio
- Coleta de Dados
- Limpeza de Dados
- Análise Exploratória
- Modelagem dos Dados
- Treinamento de Algoritmos
- Avaliação de Desempenho
- Deploy da Solução
<img width="1080" height="1080" alt="crisp" src="https://github.com/user-attachments/assets/4b3ac642-4146-4496-b95d-56d3d25ff405" />

Observação: Como esse projeto não é um projeto com uso de Machine Learning, os ciclos do CRISP-DM foram adaptados para o contextro do Test A/Bn

# 1.0 Descrição e Problema de Negócio

## 1.1 Descrição
A universidade de Montada, nos Estados Unidos, possui vários serviços de apoio ao aluno, incluindo um biblioteca.

A biblioteca da universidade oferece vários serviços para os estudantes, como alocação de salas de estudos, livros, computadores, discussões em grupo, webnários e etc. Todos esses serviços e vários outros, ficam disponíveis dentro da página web da própria biblioteca e os alunos podem acessá-la para agendar algum dos serviços disponíveis.

A página possuí um banner da universidade, uma barra de busca, três principais categorias de acesso e um barra lateral direita que exibi as últimas notícias.

Durante o período de 3 de Abril de 2013 até 10 de Abril de 2013, a página “home” da biblioteca recebeu 10.819 visitantes. Ao analisar os dados de acesso da página, o time de TI da universidade percebeu uma grande diferença entre os acessos das categorias das páginas. A taxa de click da “Find” foi de 35%, “Request” foi de 6% e “Interact” foi de 2%.
![Heatmap Homepage Version 1 - Interact, 5-29-2013](https://github.com/user-attachments/assets/291dcd0b-8042-4809-9cc7-f072a2bf8933)
Olhando para as taxas de clicks, o time de TI se perguntou o motivo da conversão da categoria “Interact” estar tão baixa.

Uma das hipóteses do time de TI foi de que o nome “Interact” está confundindo os alunos, pois não deixa claro o propósito daquela categoria. Assim, quatro novos nomes foram propostos para substituir o nome atual da categoria: “Connect”, “Learn”, “Help” e “Service”.

## 1.2 Problema de Negócio
Você foi contratado como um freelancer pela universidade de Montana para ajudar o time de TI a avaliar os dados das variações da página home da biblioteca e dizer se alguma das variações é realmente melhor do que a atual. Em caso de resposta afirmativa, qual das variações seria a melhor e deveria substituir o nome da categoria atual. E os entregáveis são:

- Alguma das conversão é realmente melhor do que a atual? Qual seria o nome da variação?

# 2.0 Dados e Premissas de Negócio

## 2.1 Desrição dos dados
| Atributo | Descrição |
| -- | -- |
| variant | Variante do site |
| visits | Número de visitas no site |
| clicks_all | Total de cliques na página |
| clicks_link | Total de cliques no link |
| conversion | 	Proporção de cliques na variante sobre o total de cliques |

## 2.2 Premissas adotadas
Para realizar esse projeto as seguintes premissas foram adotas
- A métrica de conversão que foi considerada é a quantidade de cliques na variante sobre o total de cliques no site inteiro.
- Os dados foram retirados de maneira manual para fazer o dataframe final e aplicar o Teste A/Bn.
- Hipoteses definidas:
  - H0 - Não há nenhuma diferença entre o CTR das variantes da página
  - H1 - Há diferença entre os CTR das variantes da página

# 3.0 Estratégia de solução
- Passo 1: Coleta de dados
  
  Os dados vieram através de um csv exportado a partir do Google Analitics, o dataframe inicial foi feito de forma manual a partir desse csv. Pois o principal intuito é a aplicação e entendimento do tipo de teste.
- Passo 2: Design do Experimento
  
  Nesse momento foram definidas as hipóteses, seguindo as premissas da arvore de decisão de qual tipo de metodologia utilizar.
- Passo 3: Teste de Hipóteses
  
  A metodologia do teste de hipóteses foi aplicada.
- Passo 4: Teste de Post-Hoc
  
  Após a rejeição da hipótese nula, um outro teste é aplicado com o intuito de entender qual das variantes de fato foi a influenciadora para esse resultado.
- Passo 5: Resultado de Negócios
  
  Respondendo a pergunta de negócios com base nas informações obtidas através do teste.

# 4.0 Definição dos Parêmetros

## 4.1 Nível de Confiança
É a probabilidade de que o intervalo de confiança contenha o verdadeiro parâmetro da população. Nesse teste um valor padrão de 95% foi utilizado.

## 4.2 Nível de Significância
Pode ser definido como a probabilidade de rejeitar a hipótese nula quando ela é verdadeira, denotada por α (alfa), é o inverso do nível de confiência. Nesse projeto o valor foi de 5%

## 4.3 Tamanho do Efeito
Seria a magnitude da diferença entre grupos ou a força de uma relação entre variáveis, indicando a importância prática dos resultados. O tamanho do efeito nos diz que quando o efeito é facilmente detectável, o tamanho da amostra é menor, enquanto, quando o efeito é mínimo, é preciso de uma amostra bem maior para prová-lo.

Nesse teste a biblioteca do python statsmodels foi utilizada para definir esse parâmetro, e para isso foi usado o efeito esperado. Assim, o efeito que queremos provar é que a conversão de cliques na página é diferente da atual, que é 1,1%, assim será definido nosso Effect Size através da função chisquare_effectsize.

## 4.4 Pode Estatístico
É probabilidade de detectar um efeito, se ele realmente existir, denotado por 1 - β (beta), onde β é a taxa de falso negativo. Nesse projeto o valor padrão de 80% foi utilizado.

## 4.5 Tamanho da amostra
Com todos esse parâmetros encontramos o tamanho da amostra, que é a quantidade de observações ou indivíduos incluídos em um estudo ou experimento, essencial para garantir a validade e precisão dos resultados estatísticos.

Assim, foi encontrado que o tamanho de amostra para cada grupo é de 222 amostras, sendo no total (para os 5 grupos) 1.110. Como cada variante apresenta valores de cliques totais maiores que 1000, o tamanho da amostra não será um problema.

# 5.0 Teste de Hipóteses
O dataset criado inicialmente apresenta os valores das conversões dos cliques nas variantes, mas apenas comparar esses resultados não é o suficiente para provar que há uma diferença entre as variantes das páginas.
Para isso faremos um teste de hipóteses, onde o intuito é rejeitar a hipótese nula, ou seja, que há uma diferença entre o CTR das variantes das páginas.
Assim o valor encontrado foi de 2.09e-09, um valor muito próximo de 0, bem menor que o nível de significância, o que rejeita a hipótese nula, indicando então que existe uma diferença entre as conversões de cliques das variantes.

# 6.0 Post Hoc Testing
Contudo, isso ainda não prova o ponto principal do problema. Existe uma diferença de CTR entre a páginal atual e as novas variantes?.
Para isso, utilizaremos o Post Hoc Testing, que é usado após uma análise estatística, para identificar quais pares de grupos têm diferenças significativas entre si. Ele compara cada par de grupos para descobrir onde exatamente essas diferenças ocorrem, ajudando a entender quais grupos realmente se diferenciam.
Dessa forma, as 5 variantes foram comparadas entre elas como pares, realizando o teste de hipótoses para cada, tirando assim o p-valor de cada comparação, onde se esse valor é menor que o nível de significância definido, há uma diferença significativa entre as conversões desse par, os resultados podem ser vistos a seguir:
|Variante 1|	Variante 2|	P-Valor|
| -- | -- | -- |
|interect|	connect|	0.00000054|
|interect|	learn|	0.85|
|interect|	help|	0.0062|
|interect|	sevices|	0.0000009|
|connect|	learn	|0.00044|
|connect|	help|	0.088|
|connect|	sevices|	1.0|
|learn|	help|	0.085|
|learn|	sevices|	0.00051|
|help|	sevices|	0.091|

Com isso foi observado que as variantes *connect*, *help* e *services* apresentaram uma diferença significativa de CTR comparado com o atual *interect*
Para responder essa pergunta, observamos se há uma diferença estatística entre essas variantes. Contudo, o teste mostra que não hpa diferença, podendo assumir que qualquer uma dessas variantes teriam um efeito próximo ao serem escolhidas, mas estatísticamente melhores que o atual.
Na amostra coletada as conversões das páginas são:

# 7.0 Resultado de Negócios
- Alguma das conversão é realmente melhor do que a atual? Qual seria o nome da variação?
Através do teste de hipóteses podemos provar que as conversões das novas páginas são melhores que a atual. Assim, há variantes que performam melhor que o utilizado atualmente.
As variantes que performam melhor são: connet, help e sevices. Contudo não há uma diferença entre as conversões delas.
Sendo assim, é possível dizer que a utilização de qualquer uma delas traria uma conversão de cliques melhor que interect.

# 8.0 Conclusão

Nesse projeto, foram realizadas todas as etapas necessárias para a implementação de um projeto completo de Data Science focado na utilização do Teste A/Bn.
Foi utilizado o método de gerenciamento de projeto chamado CRISP-DM e obteve-se um desempenho satisfatório em compreender a utilização do teste A/Bn e aplicar em um problema real.
Tendo em vista os resultados, o projeto alcançou seu objetivo de fazer o teste e provar para a empresa de forma estatística que a utilização das novas variantes para o lugar de interect trariam uma conversão de cliques melhor para essa parte do site.

# 9.0 Aprendizados e Trabalhos Futuros
- Aprendizados
  - Compreensão e aplicação do Teste A/Bn com conversões.
  - Conceitos estatísticos e parâmetros com teste de hipóteses
- Trabalhos Futuos
  - Testar outros testes de hipóteses para esse problema para entender se há divergência no resultado



  
