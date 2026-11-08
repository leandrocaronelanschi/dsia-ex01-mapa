# dsia-ex01-mapa

Exercício 1 — Seu tema no mapa do campo e um fichamento
Curso: Desenvolvimento de Software Suportado por IA · LEDS Academy / IFES Colatina

> **Nota sobre o tema.** Ainda não tenho um tema de dissertação definido. Conforme o enunciado permite,
> uso aqui o **Lavra**, o projeto-guia do curso, como tema de trabalho.

## Tema da pesquisa

A equipe de TI da Cooperativa Vale do Cedro mantém o **Colheita**, um sistema legado com centenas de
issues abertas e pouca cobertura de testes. O volume de issues é maior do que a equipe consegue
absorver, e boa parte delas descreve defeitos concretos em produção — datas gravadas com o fuso
errado, pesos arredondados no pagamento ao cooperado. O artefato proposto é o **Lavra**, um agente de
IA que recebe uma issue que relata um defeito, localiza no código o trecho responsável, propõe um
patch e submete esse patch à revisão humana antes do merge. O objeto da pesquisa não é o modelo de
linguagem em si, e sim o laço completo — issue, localização, edição, verificação e decisão humana —
medido em um repositório real de porte médio e com histórico próprio.

## Fase do processo

**Depuração e reparo.**

O teste de decisão da fase pergunta: *existe um defeito concreto como ponto de partida e uma correção
como ponto de chegada?* No Lavra a resposta é sim nos dois extremos: a entrada é uma issue que relata
um comportamento errado observado em produção, e a saída é um patch que corrige esse comportamento.
A avaliação do trabalho também se concentra aí — o que será medido é a proporção de patches corretos
sobre issues reais do Colheita, e não a qualidade de código gerado do zero nem a organização da fila
de trabalho.

## Fronteira descartada

**Manutenção.**

Manutenção é a fase vizinha mais próxima, porque o mecanismo técnico é o mesmo: um agente que lê
código existente e o transforma. O codebook, porém, separa as duas fases pela **motivação**, não pela
técnica. O teste de decisão de manutenção pergunta se o trabalho transforma código existente *por
razão que não é um defeito*. No Lavra a razão é sempre um defeito relatado: o agente não é acionado
para migrar o Colheita para uma versão nova de biblioteca, nem para pagar dívida técnica, nem para
refatorar por legibilidade. Se a motivação fosse essa, o mesmo mecanismo cairia em manutenção.

Vale registrar uma segunda fronteira próxima, **gestão de projeto**: se o Lavra apenas triasse,
classificasse e atribuísse issues sem resolvê-las, o trabalho seria de organização do trabalho, e não
de reparo. Como o agente chega ao patch e é por ele que a avaliação mede, a fase predominante
continua sendo depuração e reparo.

## Segurança

**Grau: secundário.**

Teste da dimensão de segurança: *se o trabalho fosse reescrito sem nenhuma menção a vulnerabilidade,
ataque ou ameaça, ele ainda teria contribuição?* Sim — a contribuição central (resolver issues de
defeito com verificação humana no portão) continua de pé. Mas o trabalho **perderia uma seção de
resultados**, por dois motivos concretos:

1. Os patches do Lavra são código gerado por IA e podem introduzir vulnerabilidades enquanto fecham o
   defeito — por exemplo, trocar uma validação de entrada por outra mais curta e passar nos testes
   existentes do Colheita, que são poucos.
2. O próprio agente é alvo. Uma issue do Colheita é texto escrito por terceiros; uma issue
   mal-intencionada pode conter instruções que o agente leia como se fossem da equipe (injeção de
   prompt), num sistema que tem permissão de escrita no repositório.

Logo, não é "ausente": a dissertação precisa medir o que os patches fazem com a segurança do
Colheita, além de medir se eles fecham a issue.

## Evidência

Três obras da fase **depuração e reparo**, da base de leituras da disciplina:

| Obra | Link | Tipo de estudo | Sede | O que sustenta para o Lavra |
| --- | --- | --- | --- | --- |
| Zhang et al., *A Critical Review of Large Language Model on Software Engineering: An Example from ChatGPT and Automated Program Repair* (2023) | [arXiv:2310.08879](https://arxiv.org/abs/2310.08879) | Revisão crítica / survey narrativo | Preprint (arXiv) | Sustenta que o desempenho de um LLM em reparo depende fortemente do que entra no prompt — descrição do problema, mensagem de erro e localização do bug — e que o ganho vem do fluxo interativo, não do modelo sozinho. Alerta para vazamento de dados de benchmark, o que justifica avaliar o Lavra em issues do próprio Colheita. |
| Zhang et al., *AutoCodeRover: Autonomous Program Improvement* (2024) | [arXiv:2404.05427](https://arxiv.org/abs/2404.05427) | Ferramenta / sistema | ISSTA 2024 (trilha principal) | Sustenta que localizar o código antes de editar — por busca na estrutura do programa e, havendo testes, por localização de falhas baseada em espectro — melhora a resolução autônoma de issues reais do GitHub. É o desenho de referência do laço do Lavra. |
| Feng & Chen, *Prompting Is All You Need: Automated Android Bug Replay with Large Language Models* (2023) | [arXiv:2306.01987](https://arxiv.org/abs/2306.01987) | Ferramenta / sistema | ICSE 2023 (trilha principal) | Sustenta que o texto de um relato de bug, escrito por humano e incompleto, pode ser convertido por LLM em passos de reprodução executáveis. Para o Lavra, sustenta a etapa anterior ao patch: reproduzir o defeito antes de tentar corrigi-lo. |

**O que estas obras não sustentam.** Nenhuma delas sustenta que os números medidos em seus benchmarks
se repitam no Colheita, que tem outro tamanho, outra história e poucos testes automatizados. Os seis
artigos anexados ao e-mail da Profa. Lúcia também não cobrem esta fase: quatro são de processo
transversal (Hou et al., Fan et al., Dong et al., He et al.) e um é de verificação (Wang et al.);
apenas Feng & Chen cai em depuração e reparo. Eles dão o vocabulário do campo, não a evidência do
tema.

---

## Arquivos deste repositório

- `README.md` — este arquivo: tema, fase, fronteira, segurança e evidência.
- `fichamento.md` — fichamento de AutoCodeRover nos seis campos do modelo da disciplina.
- `USO-DE-IA.md` — declaração de uso de IA.
