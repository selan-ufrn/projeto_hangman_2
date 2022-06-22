# Projeto de Programação **Jogo da Forca** (_Hangman_), versão 2.0

## 1. Introdução
Nesse projeto de programação você vai retomar o desenvolvimento do [Projeto Hangman](https://github.com/selan-ufrn/projeto_hangman) realizado anteriormente para incluir novas _features_ (**funcionalidades**).

O desenvolvimento desse projeto lhe proporcionará a oportunidade de experimentar um dos aspectos mais "motivantes" na vida de um desenvolvedor de _software_: **manter** e **estender** código já existente 😞. Será uma ótima oportunidade para avaliar até que ponto sua equipe foi bem sucedida em desenvolver um código **limpo**, **bem documentado** e com um bom **design**, capaz (ou não) de facilitar a incorporação de novas funcionalidades ao jogo. Se você realizou sua tarefa de forma bem feita ("_if you did a good job, my friend_"), acomodar novas características não deveria ser um processo muito **"doloroso"**.

Entre as novas _features_ que devem ser incorporadas estão leitura e gravação de arquivos, uso de **tipos abstratos de dados** (como listas e dicionários), internacionalização do código (com suporte a acentos em Português), suporte a diferentes níveis de dificuldades de jogo, dentre outras.

Outra característica nova desse projeto é que muitas das funcionalidades que serão solicitadas poderão ser desenvolvidas da forma que a equipe decidir. Isso quer dizer que esse documento não vai especificar, em detalhes, o que deverá ser feito. As _feaures_ necessárias serão descritas a seguir de forma geral, mas caberá a cada equipe decidir qual a melhor estratégia de incorporar as novas funcionalidades ao jogo. Dessa forma, esse projeto pode proporcionar uma boa oportunidade de desenvolver e praticar suas próprias ideias da forma que lhe parecer mais eficiente/interessante, bem como colocar em prática suas habilidades recém adquiridas em outros componentes, como **Estruturas de Dados Básicas I**, por exemplo.


## 2. Novas Funcionalidades para Hangman 2.0


### 2.1 Classificação de palavras

O novo _Hangman_ deve prover um mecanismo para **classificar** ou atribuir uma **índice** (ou nota) a uma palavra. Esse índice deve procurar refletir o nível de dificuldade para se adivinhar essa palavra, em comparação a outras palavras ou de forma absoluta (se possível). Ou seja, esse índice deve ajudar a identificar se uma palavra é mais difícil/fácil do que outra E/OU classificar uma palavra como difícil, fácil, etc.

Para definir esse mecanismo ou **função**, seu programa deve utilizar um arquivo contendo um estudo do _"Corpus da Língua Portuguesa Brasileira"_, disponível [aqui](https://www.linguateca.pt/acesso/tokens/formas.cbras.txt).

Confira abaixo as 20 primeiras linhas desse arquivo:
```
68633421	,
43779099	de
40188428	.
23513526	a
21525861	e
17648478	o
16450939	que
14955929	do
13535685	da
10396570	em
10084974	)
9315106	(
7958410	para
7049297	com
6840306	:
6353143	no
5917493	os
5873518	um
5555507	na
5527340	é
```

Cada linha contém uma contagem, seguido da palavra, que pode ou não conter hífen e ser acentuada. Esse _corpus_ contém um total de 5867825 linhas diferentes. Quanto maior o número associado a uma palavra maior será sua frequência de uso na língua portuguesa. O arquivo está ordenado por contagem de uso.

Sua equipe deverá determinar de que forma esse esse arquivo com a contagem de uso das palavras deve ser usado para classificar quantitativamente uma palavra como fácil ou difícil. Uma estratégia pode ser calcular a **frequência media das palavras**. Assim, palavras cuja frequência esteja abaixo da média podem ser consideradas _difíceis_, por exemplo. Já palavras mais frequentes podem ser consideradas mais fáceis.

Outros aspectos, além da frequência de ocorrência, que podem ser levados em consideração para determinar o **índice** de dificuldade são:
+ quantidade de consoantes;
+ quantidade de vogais;
+ razão entre consoantes e vogais;
+ repetição de letras na palavra;
+ comprimento da palavra; e,
+ presença ou não de acentuação.

O seu trabalho **deve** levar em consideração, pelo menos, a frequência de uso das palavras para determinar o grau de dificuldade de uma palavras.

Uma possibilidade alternativa é que uma palavra receba uma classificação qualitativa ou invés de quantitativa. Isso quer dizer que seu método de avaliação de uma palavra pode classificar uma palavra em, digamos, **fácil**, **médio**, ou **difícil**, ao invés de gerar um valor numérico arbitrário.


### 2.2 Categorias de palavras

Todas as palavras candidatas devem pertencer a pelo menos uma **categoria**.
Ao iniciar uma partida, o jogador poderá escolher uma categoria (ou mais, se optar pelo nível _hard_) de palavra. A partir dessa escolha as palavras secretas devem ser sorteadas apenas se pertencerem à(s) categoria(s) selecionada(s).

São exemplos de possíveis categorias:

+ profissões
+ filmes (vencedores de Oscar, de décadas específicas, atores, etc.)
+ comidas (doces, legumes, pizzas, verduras, etc.)
+ cores
+ animais (domésticos, mamíferos, aves, etc.)
+ signos do zodíaco
+ objetos/utensílios cozinha
+ palavras raras
+ peças de roupa
+ séries de TV, novelas
+ times de futebol (nacionais, de ligas específicas, etc.)
+ estados do Brasil
+ países do mundo (ou de um continente em particular)
+ modalidades esportivas (olímpicas, individuais, coletivas, etc.)
+ instrumentos musicais (corda, sopro, percussão, etc.)
+ órgãos humanos
+ elementos químicos

Claro, não é necessário suportar todas as categorias aqui listadas. Seu programa deverá, contudo, oferecer o mínimo de **3 categorias**.

Note que o aspecto categoria deve influenciar diretamente a forma escolhida para armazenar as palavras lidas do arquivo na memória. É necessário pensar em uma boa e eficiente estrutura de dados que permita recuperar eficientemente uma lista de palavras em uma ou mais categorias (pode imaginar que categorias são equivalentes a _hashtags_ em redes sociais). Ou seja, a partir de um banco de dados "central" de palavras o programa precisará gerar/recuperar listas com subconjunto de palavras, de acordo com as categorias selecionadas.

### 2.3 Níveis de dificuldade

A nova versão do jogo deverá suportar, pelo menos, dois níveis de dificuldade.
Caberá a cada equipe definir qual o impacto de cada nível de dificuldade sobra a **jogabilidade** (_gameplay_) do Hangman.

Por exemplo:
1. **Nível fácil**
    - 40% das letras já são reveladas logo de início.
    - jogador pode escolher 1 (ou mais) letras para revelar.
    - quantidade de erros para perder é 10.
    - somente palavras "fáceis" são sorteadas (ver Seção 2.1)
    - 60% das palavras sorteadas devem ser "fáceis", 40% devem ser "médias".
    - chute de uma letra sem acento funciona como um "curinga", ou seja, podem corresponder a mesma letra com acentos. Por exemplo, `a` pode corresponder a `ã`, ou `à` ou `á`.


2. **Nível médio**
    - 15% das letras já são reveladas logo de início.
    - jogador pode escolher apenas 1 letras para revelar.
    - quantidade de erros para perder é 8.
    - 30% das palavras sorteadas devem ser "fáceis", 50% devem ser "médias" e 20% devem ser "difíceis".

3. **Nível difícil**
    - 0% das letras já são reveladas logo de início.
    - jogador **não** pode escolher letras para serem revelada.
    - quantidade de erros para perder é 6.
    - 10% das palavras sorteadas devem ser "fáceis", 40% devem ser "médias" e 50% devem ser "difíceis".

A sugestão acima é apenas um exemplo e não precisa ser implementada dessa forma.
Cabe a cada equipe definir como vai caracterizar cada nível de dificuldade que o jogo suportará.

### 2.4. Novo sistema de pontuação

O novo Hangman deve prever uma nova forma de pontuar a atuação de cada jogador.
Jogadores que preferem atuar nos níveis mais difíceis devem ser recompensados com uma pontuação mais generosa; em contrapartida, perder no nível mais difícil pode implicar em perder mais pontos.

O novo sistema de pontuação também deve levar em consideração, por exemplo, que acertar palavras mais difíceis vale mais do que acertar palavras mais fáceis.

Outro fator a considerar é a **taxa de eficiência** do jogador. Suponha que um jogador A e um jogador B atualmente possuam 500 pontos cada. Se o jogador A costuma acertar mais do que errar ela(e) deveria ser "ranqueado" acima do jogador B. Pode ser que o jogador B tenha conseguido os 500 pontos porque joga muitas vezes mas erra mutas vezes, mas o volume total de participações fez com que ele obtivesse 500 pontos também.

O objetivo importante, na verdade, é produzir um sistema de pontuação que seja o mais **justo** possível, de maneira a valorizar mais o jogador mais efetivo.

### 2.5. Quadro de pontuação permanente

O jogo deverá salvar e ler de arquivo o **quadro geral de pontuação** (_Score Board_) contendo informações sobre o desempenho de todos os jogadores que já participaram. O quadro geral deve estar ordenado ("ranqueado") do melhor jogador ao pior jogador, podendo exibir apenas os 7 primeiros classificados, por exemplo.

Esse arquivo deverá conter (pelo menos):
+ Nome jogador.
+ Pontuação do jogador.
+ Lista de palavras que já foram jogadas (para evitar repetição).
+ Taxa de eficiência do jogador (quantidade de acertos sobre erros).

A sugestão aqui é salvar os dados no formato `csv` ([_comma-separated values_](https://en.wikipedia.org/wiki/Comma-separated_values)), para facilitar a leitura e "tokenização" das informações.

### 2.6. Arquivo de configuração

Toda e qualquer aspecto configurável do jogo deverá ser lido a partir de um arquivo de configuração `config.ini` especificado no [formato `INI`](https://en.wikipedia.org/wiki/INI_file) (extensão `.ini`).

Confira a seguir um exemplo de arquivo de configuração contendo informações sobre algumas das funcionalidades descritas nesse documento.

```ini
[global]
; Interface colorida ou não.
enable_colors = true
; Indicação da língua usada no jogo.
language = pt_br ; en_us
; Permite que o cliente possa "chutar" uma palavra de uma vez (sem precisar ser letra a letra)
enable_word_guess = true

[settings]
; Nome do arquivo com a pontuação
score_file = "score.csv"
; Nome do arquivo com as palavras
words_file = "words.csv"


[Level-easy]
; Indica qual o tamanho mínimo para uma palavra secreta nesse nível
min_len = 8
; Indica qual o tamanho máximo para uma palavra secreta nesse nível
max_len = 12
; Indica a porcentagem da palavra secreta que deve ser revelada nesse nível.
reveal = 0.4 ; reverlar 40% das letras logo de início.
; Especifica quantos erros podem ser cometidos antes de perder uma partida.
n_mistakes = 10
; Aceitação de letras sem acentos como curinga de letras acentuadas.
accents_treatment = permissive  ; letras sem acentos podem substituir letras acentuadas.
; Probabilidade de sortear palavras por categoria.
easy_word_probability = 0.6
medium_word_probability = 0.4
hard_word_probability = 0

[Level-medium]
min_len = 5
reveal = 0.2
n_mistakes = 9
accents_treatmen = strict
easy_word_probability = 0.3
medium_word_probability = 0.5
hard_word_probability = 0.2

[Level-hard]
min_len = 3
reveal = 0
n_mistakes = 6
accents_treatmen = strict
easy_word_probability = 0.1
medium_word_probability = 0.4
hard_word_probability = 0.5

```
Seu programa deve ser capaz de identificar erros de sintaxe no arquivo de configuração, podendo assumir valores padrão (_default_) caso algum item fundamental não seja informado no arquivo. 

Alternativamente, seu programa pode optar por não aceitar que itens essenciais não estejam especificados no arquivo e, se for o caso, emitir uma mensagem de erro destacando o problema.


### 2.7. Internacionalização

A nova versão do Hangman deverá suportar o uso de palavras acentuadas em Português.

**Opcionalmente**, seu jogo pode aceitar uma configuração de língua.
Isso quer dizer que se no arquivo de configuração o usuário escolher a língua Portuguesa, tanto a interface quanto as palavras secretas serão escritas em Português. Por outro lado, se o cliente escolher Inglês no mesmo arquivo de configuração, então tanto a interface quanto as palavras secretas serão escritas em Inglês.

Claro, no caso de usar a língua Inglesa, será necessário conseguir um arquivo contendo a avaliação do "_corpus_" em Inglês, de maneira que a mesma estratégia de qualificação de uma palavras que considere a frequência de uso da palavra também seja aplicável. Para mais informações sobre _corpus_ em Inglês visite esse [site](https://www.english-corpora.org/).

## 3. Nova interface

Tendo em vistas as incorporaçao das _features_ descritas nesse documento,  a interface do Hangman precisa ser modificada para acomodar as novas funcionalidades.

Fica a cargo de cada equipe decidir como modificar a interface do jogo para incluir as novas _features_. Sejam criativos e, mais importante, procurem produzir uma interface **consistente**.

## 6. Software design tips

Alguns pontos importante desse projeto merecem destaque:

+ Comece o seu projeto **modificando** o diagrama de estados, caso sua equipe tenha adotada a arquitetura _game loop_ no projeto original. A inclusão de novas etapas no processo de interação implicará, provavelmente, na criação de novos estados.
+ Pense com cuidado sobre quais estrutura de dados e estratégias devem ser escolhidas para melhor gerenciar o armazenamento e recuperação de palavras.
+ Procure desenvolver o projeto em etapas. Sempre que possível tente desenvolver uma _feature_ de cada vez (claro, nem sempre isso é possível) e teste bem antes de seguir para a próxima funcionalidade. Nesse caso vale a pena manter no repositório a versão _master_ sempre funcionando e cada nova funcionalidade seria um novo _branch_ do projeto que será incorporado ao _master_ apenas depois de pronto, testado e aprovado pelo **gerente** do projeto.
Vale a pena conferir esse capítulo sobre [branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell).
Essa é uma excelente oportunidade de aprender na prática o uso de _workflows_ com o `git`. Para uma visão introdutória consulte [esse capítulo](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows) e para uma visão mais profissional acesse esse [site](https://martinfowler.com/articles/branching-patterns.html).
+ Produza uma documentação adequada do projeto. Pode ser que no futuro você precise voltar para ele mais uma vez!!! 😱

## 5. Avaliação

A avaliação do trabalho será feita levando em consideração:

1. Entrega de um documento indicando como cada equipe pretende implementar as funcionalidades descritas nesse documento. **[2 pts]**
2. Nível de complexidade e qualidade de cada funcionalidade implementada. **[14 pts]**
3. Qualidade geral do jogo, ou seja: interface consistente, robustez (não quebra com entradas erradas), qualidade do código, vazamento de memória, uso de estruturas de dados de forma eficiente. **[8 pts]**
4. Jogabilidade: o quão interessante (criativo) ficou o jogo, ou seja, se é divertido interagir com o jogo e se ele consegue proporcionar um nível adequado de desafio que consiga manter o jogador engajado. **[6 pts]**

Portanto, são necessários 30 pontos para alcançar a nota máxima. Cada projeto será avaliado por meio de uma entrevista, dado o caráter subjetivo de cada um dos itens acima.

Como sempre a ausência do arquivo `autor.md` pode implicar na perda de 1 ponto na nota final (de zero a 10), bem como surgimento de erros de compilação, de execução ou presença de vazamento de memória.

Opcionalmente poderemos fazer uma sessão de **demos**, onde cada equipe poderá orgulhosamente 🤩 apresentar aos demais participantes como ficou seu projeto.
