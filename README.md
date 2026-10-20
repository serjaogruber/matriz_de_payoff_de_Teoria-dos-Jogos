# matriz_de_payoff_de_Teoria-dos-Jogos
Esse código é um aplicativo de desktop em Python (Tkinter + Matplotlib) que monta uma matriz de payoff de Teoria dos Jogos a partir da variação de preço de uma ação e procura o Equilíbrio de Nash dessa matriz.


O que ele faz, na prática

Entrada: você digita o preço inicial, o preço final/atual e o ticker (padrão: 36,60 → 48,20, PETR4). O ticker é só um rótulo, pois o código não busca nenhum dado de mercado.
Variação: calcula a diferença em reais e em percentual (var_pct). Com os valores padrão, dá cerca de +31,7%.
Matriz 2x2: define dois jogadores fictícios.
J1 (Institucional): Acumular (Comprar) ou Distribuir (Vender).
J2 (Especulador): Seguir Tendência ou Contra-Tendência.
Cada célula tem um payoff para cada jogador, calculado como var_pct vezes um coeficiente fixo escolhido pelo autor (1.5, 0.5, -1.2, -0.3 para J1; 1.0, -0.8, -0.5, 0.4 para J2).
Equilíbrio de Nash: a função calcular_equilibrio_nash encontra a melhor resposta de cada jogador para cada estratégia do outro. As células onde as duas melhores respostas coincidem são os equilíbrios em estratégias puras.
Exibição: mostra a tabela com Matplotlib, com a célula de equilíbrio em verde, e escreve o resultado no topo da janela.

O ponto mais importante: o resultado é circular

Como todos os payoffs são múltiplos do mesmo var_pct, só importa o sinal da variação, não o tamanho:

Preço subiu: o equilíbrio é sempre Acumular vs Seguir Tendência.
Preço caiu: o equilíbrio é sempre Distribuir vs Seguir Tendência.
Variação zero: todos os payoffs são 0, então as quatro células aparecem como equilíbrio.

Ou seja, o app “descobre” que, se o preço subiu, comprar e seguir a tendência era o melhor, o que já se sabia ao olhar o preço. A matriz é construída a partir do resultado observado, então não prevê nada.

Outros detalhes

Os payoffs (“J1: 47.5%”) não são retornos reais de investidores institucionais ou especuladores. São números inventados proporcionais à variação.
Os coeficientes são arbitrários e não vêm de dados ou de um modelo.
A mensagem “Sem Equilíbrio em Estratégias Puras” praticamente nunca aparece, porque a construção da matriz garante um equilíbrio puro.
Só calcula equilíbrios puros, sem estratégias mistas.
É um bom exercício didático de como implementar Nash em código e desenhar uma tabela no Matplotlib, mas não serve como ferramenta de análise de mercado.

Se quiser, posso mostrar como transformar isso num jogo de verdade, por exemplo com payoffs definidos por premissas explícitas (custos de transação, liquidez, informação) em vez de depender do resultado já ocorrido, ou incluir equilíbrio em estratégias mistas.
