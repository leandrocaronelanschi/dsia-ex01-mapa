# Fichamento

## Referência

ZHANG, Yuntong; RUAN, Haifeng; FAN, Zhiyu; ROYCHOUDHURY, Abhik. **AutoCodeRover: Autonomous Program
Improvement.** In: *Proceedings of the 33rd ACM SIGSOFT International Symposium on Software Testing
and Analysis (ISSTA 2024)*. Viena, 2024. Preprint disponível em:
[arXiv:2404.05427](https://arxiv.org/abs/2404.05427) (v1 de 8 abr. 2024; v3 de 25 jul. 2024).

## Tema

Resolução autônoma de issues de repositórios de software por um agente baseado em modelo de
linguagem, com ênfase em **como o agente encontra o trecho de código relevante** antes de escrever a
correção. A fase do codebook é depuração e reparo.

## Objetivo

Demonstrar que tratar a tarefa como problema de engenharia de software — e não apenas como geração de
texto sobre um conjunto de arquivos — aumenta a eficácia do reparo autônomo. Para isso, os autores
propõem um agente que navega a representação do programa em árvore sintática abstrata (AST), busca
por classes e métodos de forma iterativa e, quando há testes disponíveis, refina o contexto com
localização de falhas baseada em espectro.

## Resumo

Os autores partem de uma limitação dos agentes de código então disponíveis: eles tratam o projeto
como um amontoado de arquivos de texto e dependem do modelo para adivinhar onde está a causa raiz.
O AutoCodeRover substitui essa adivinhação por uma busca estruturada: a partir da issue, o agente
consulta a estrutura do programa (classes e métodos) em rodadas sucessivas, acumulando contexto até
conseguir caracterizar a causa do defeito; só então gera o patch. Quando o repositório oferece um
conjunto de testes, a localização de falhas baseada em espectro estreita ainda mais o conjunto de
candidatos. A avaliação é feita no SWE-bench-lite, recorte de 300 issues reais do GitHub, onde a
abordagem resolve cerca de 19% das issues a um custo médio aproximado de US$ 0,43 por issue,
superando o SWE-agent em eficácia e em custo. Os autores encerram defendendo que esse fluxo pode, no
limite, sustentar a melhoria autônoma de código gerado por LLM.

## Citação importante

> "Our code search exploits the program structure in the form of classes/methods"
>
> — ZHANG et al. (2024), *Abstract*, arXiv:2404.05427v3.

## Comentário

É a obra que mais se aproxima do desenho do Lavra, e serve de referência direta para a arquitetura do
agente. **O que ela sustenta:** que localizar antes de editar é uma decisão de projeto com efeito
medido, e não preferência de estilo; e que a estrutura do programa (AST, classes, métodos) é um sinal
melhor do que a similaridade textual sobre arquivos. Isso justifica, na minha dissertação, gastar uma
etapa inteira do laço com localização antes de chamar o modelo para escrever o patch, e justifica
medir separadamente acerto de localização e acerto de patch.

**O que ela não sustenta:** que o número de ~19% se repita no Colheita. O SWE-bench-lite é composto
por repositórios Python populares, com testes automatizados que servem de oráculo — e é exatamente o
oráculo que falta no Colheita, que tem poucos testes. Sem testes, a localização por espectro, que é
metade do mecanismo do artigo, simplesmente não roda; e sem oráculo não há como declarar um patch
correto sem revisão humana. Também não sustenta nada sobre segurança: o artigo mede correção
funcional, não o que o patch faz com a superfície de ataque do sistema, que é justamente a seção de
resultados que o Lavra precisa acrescentar.

**Onde entra no trabalho:** capítulo de trabalhos relacionados, como linha de base de arquitetura;
e no capítulo de avaliação, como referência de comparação — com a ressalva explícita de que o
ambiente de medição é diferente.
