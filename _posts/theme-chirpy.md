---
título: "Personalização do blog Chirpy"
data: 30/03/2024
categorias: [HTML e CSS]
etiqueta: [HTML, CSS]
matemática: verdade
pino: verdadeiro
media_subpath: /assets/img/in-post/2024/2024-03-30/
descrição: Jekyll-Theme-Chirpy v7.0.0 básico Esquema de personalização: arranjo MathJax, grade lado a lado, contagem de pontos da estação de pé, animação de fundo, prompt autodefinido Detalhes japoneses Grade de elementos, LQIP japonês e bloqueio de cores reverso Python real contente.
---
## 1. Resumo
No ano passado, comuniquei-me com jekyll no departamento do github, onde foram obtidos os resultados.

No entanto, o modelo de placa que uso primeiro é [Huxpro](https://github.com/Huxpro/huxpro.github.io), e recentemente revisei o modelo de placa em tempo hábil [Chirpy](https:// github.com/cotes2020/jekyll-theme-chirpy/). Anteriormente, Jekyll tinha o conteúdo japonês do formato do problema principal misturado, mas depois da versão 3.2.0, Jekyll instalou o `tema baseado em gemas` e teve o empacotamento do formato do problema principal concluído (isto é semelhante ao HTML e CSS). ). O modelo Chirpy está correto, é um `tema baseado em gemas`, então use o blog generativo Chirpy Starter, basta incluir a declaração do conteúdo, a ideia é realmente realizada. Material de personalização do modelo Chirpy, você precisa inserir a lista de texto.

Existem muitas maneiras de escolher. A primeira opção é ir diretamente para a página do github do Chirpy, onde você pode ler o código-fonte e o código-fonte. Segundo tipo de uso do git, passando o comando `bundle info --path jekyll-theme-chirpy`

![arquivo de tema](theme-file.PNG){: .shadow width="700"}
_Site de texto em estilo caixa fechada_

Depois de chegar ao nível local, decidi escrever meu próprio blog.

> 6.5.5 A versão impressa foi atualizada novamente, mas a nova versão também é semelhante e inconveniente.
{: .prompt-info}

Tempo de exibição de geração de atenção, libere-se `.github.io` 文品夹的样estilo 文品会encoberto da frase de mesmo nome da gema original 夹り, mas um item textual de estilo 样 não modificado 则光样从 gema 夹り读取、Portanto, um item textual de estilo 样 não modificado O autor do modelo de placa foi atualizado desde o início do projeto, e o método foi continuado desde então. Este artigo foi atualizado com algumas pequenas alterações (não copiadas).

## 2. Posicionamento modificado do MathJax
Após a introdução do MathJax 3.x, a velocidade das fórmulas matemáticas em comparação com o KaTeX foi reconsiderada, e o MathJax apoiou a expansão do desenvolvimento, e a proporção funcional do KaTeX foi ainda mais fortalecida, por isso foi melhor considerar o MathJax. O modelo foi criado por MathJax em `assets/js/data/mathjax.js`{: .filepath}.

### 2.1.
Adição de um pequeno pacote de desenvolvimento, ``física`, ao mesmo tempo e também autodeterminação (importação oficial simplificada); Leia abaixo (mais conteúdo disponível no site oficial do MathJax):

<!-- {% raw %} -->
```javascript
---
layout: compress
# WARNING: Don't use '//' to comment out code, use '{% comment %}' and '{% endcomment %}' instead.
---

{%- comment -%}
  See: <https://docs.mathjax.org/en/latest/options/input/tex.html#tex-options>
{%- endcomment -%}

MathJax = {
  loader: { load: ['[tex]/physics','ui/lazy',] },
  tex: {
    inlineMath: [
      ['$', '$'],
      ['\\(', '\\)']
    ],
    displayMath: [
      ['$$', '$$'],
      ['\\[', '\\]']
    ],
    packages: {'[+]': ['physics']},
    tags: 'ams',
    macros: {
        'e': '\\mathrm{e}',
        'RR': '\\mathbb{R}',
        'ZZ': '\\mathbb{Z}',
        'QQ': '\\mathbb{Q}',
      },
  }
  options: {
    lazyMargin: '200px',
  },
  svg: { fontCache: 'global'},
};
```
{: file="assets/js/data/mathjax.js"}
<!-- {% endraw %} -->

### 2.2. Versão oficial de visualização avançada
A página principal do Blog, a seção de texto da seção de texto mostra diretamente a expressão matemática, a página principal é a página principal, a fórmula está disponível para referência [edição-1140](https://github.com/cotes2020/ jekyll-theme-chirpy/issues/1140).
> No final das contas, os cálculos dessa pessoa são semelhantes aos de outras pessoas. Se precisar dele novamente, abra-o novamente.
{: .prompt-info}

## 3. Lado da modificação
### 3.1.
Há `assets/css/jekyll-theme-chirpy.scss`{: .filepath} no texto, adicionado adicionalmente à representação CSS, em que `background-image` é usado para adicionar comandos básicos do fragmento de fundo, logo após o demanda, adicione o seguinte URL:
```scs
#Barra Lateral {
imagem de fundo: url(https://cdn.jsdelivr.net/gh/huanyushi/Blog-Image-Bed@main/assets/img/background.jpg /* <- alterar imagem de fundo */);
background-size: cover /* <- personaliza o tamanho da imagem */
repetição em segundo plano: sem repetição; /* <- sem repetição */
posição de fundo: topo; /* <- posição da imagem */
}
````
{: file="assets/css/jekyll-theme-chirpy.scss"}

A cor das letras deve ser anotada, e a cor dos caracteres que escolhi deve ser escura, portanto a cor das letras deve ser branca.
```css
#barra lateral .site-title a {
cor: #ffffff;
sombra de texto: 5px 5px 10px rgba (0,0,0,0,5);
}
#barra lateral .site-subtitle {
cor: #ffffff;
sombra de texto: 2px 2px 3px rgba (0,0,0, 0,7);
}
#barra lateral .barra lateral-bottom .mode-toggle, #barra lateral a {
cor: #ffffff;
}
#barra lateral .barra lateral-bottom .btn {
cor: var(-barra lateral-btn-cor);
}
````
{: file="assets/css/jekyll-theme-chirpy.scss"}

###3.2.
A gem no pacote contém o item de texto `_includes/sidebar.html`{: .filepath}, e o seguinte texto está incluído no texto (com o item de texto friends.html`{: .filepath}):

<!-- {% raw %} -->
```html
  <!-- Friends link -->
  {% if site.data.friends %}
      {% include friends.html %}
  {% endif %}
```
{: file="_includes/sidebar.html"}
<!-- {% endraw %}) -->

Nova construção um texto `_includes/friends.html`{: .filepath}, instalação e lançamento do Shotomo dentro (isso pode ser reduzido ao atualizar a placa do modelo):

<!-- {% raw %} -->
```html
<!-- Instalação amigável, localizada em sidebar.html Entrada média -->
<div class="amigos">
<hr style="cor:branco;borda: 1px sólido ">
<p><i class="fas fa-user-friends"></i><span>AMIGOS</span></p>
<ul>
{% para amigo em site.data.friends %}
<li><a href="{{friend.href}}">{{friend.title}}</a></li>
{%endfor%}
</ul>
</div>
````
{: file="_includes/friends.html"}
<!-- {% endraw %}) -->

Concluída a adição da configuração sincronizada em `assets/css/jekyll-theme-chirpy.scss`{: .filepath}, conforme mostrado abaixo:
```css
/* Interface de usuário lado a lado */
#barra lateral .amigos {
preenchimento à esquerda: 2,5rem;
preenchimento à direita: 1,25rem;
largura: 100%;
margem inferior: 1,5rem;
}
#barra lateral .amigos p {
cor: rgb (255.255.255.0,95);
família de fontes: herdar;
peso da fonte: 600;
tamanho da fonte: 95%;
}
#barra lateral .amigos pi {
opacidade: 0,8;
margem direita: 1,5rem;
}
#barra lateral .amigos p span {
espaçamento entre letras: 0,2px;
opacidade: 0,9;
}
#barra lateral .amigos ul {
cor branca;
tamanho da fonte:95%;
opacidade: 0,95;
margem inferior: 0rem;
}
#barra lateral .amigos ul li {
margem inferior: 0,4rem;
opacidade: 0,9;
}
````
{: file="assets/css/jekyll-theme-chirpy.scss"}

Empacotamento bem-sucedido, disponível apenas `_data/friends.yml`{: .filepath} A adição das seguintes configurações pode ser feita imediatamente (pode ser adicionada diretamente):
```yml
- título: "Título1"
href: "https://example.com"
- título: "Título2"
href: "https://example.com"
- título: "Título3"
href: "https://example.com"
````
{: file="_data/friends.yml"}

<tabela>
<tr>
<td><img src="friend1.png" alt="friend example1"></td>
<td><img src="friend2.png" alt="friend example2"></td>
<td><img src="friend3.png" alt="friend example3"></td>
</tr>
</tabela>

<div class="box-warning" markdown="1">
<div class="title"> Nota </div>
1. É impossível comunicar-se com os amigos, é fácil ocupar a parte inferior do espaço da plataforma social e a tela fica fechada para o exterior. Se quiser criar um novo amigo, você também pode selecionar um novo em `_tabs/friends.md`{: .filepath}.
2. Nossa localização está localizada na parte inferior da plataforma, e a parte inferior da plataforma está acima da plataforma. Como resultado, a taxa de divisão é grande e a duração da seleção na parte superior da reunião é muito grande. Como resultado, é possível ajustar a posição do usuário após selecionar o cartão `_includes/sidebar.html`{: .filepath} ``<nav class="flex-column flex-grow-1 w- 100 ps- 0">` Neutro `flex-grow-1` 1">`. Ao mesmo tempo, `assets/css/jekyll-theme-chirpy.scss`{: .filepath} dentro da área `#sidebar .friends` `margin-bottom: 2rem` Modificação da distância superior `margin-top: ? ? Auto-seleção.
</div>

## 4. <del> Modificação da introdução do texto para leitura adicional</del>
<del>Entendo que este é um modelo de bug, então atualizei uma cópia parcial deste PR [refator: faça leituras adicionais exibir as postagens mais recentes.](https://github .com/cotes2020/jekyll- tema-chirpy/pull/1699). </del>

> Este é o autor de PR **Combined**, atualmente versão Chirpy 7.0.0 e conteúdo posteriormente revisado e revisado, esta é uma visão geral do conteúdo.
{: .prompt-perigo}

Descrevi anteriormente um problema, tenho 5 frases diferentes, o tempo para escrever a última dependência `Post1`, `Post2`, `Post3`, `Post4` soma `Post5`, imediatamente:

````
_Postagens
├─ Post1.md
├─ Post2.md
├─ Post3.md
├─ Post4.md
└─ Post5.md
````

Ao abrir cada artigo, o grupo inferior recomenda as três frases mais adequadas (em `_includes/related-posts.html`{: .filepath}). Porém, o problema atual é que o número de frases distribuídas é o mesmo no momento, então não há necessidade de limitar o número de artigos que posso escrever, e o final do artigo é para leitura posterior.

Aqui estão alguns exemplos, quando abri `Post4`, a parte inferior mostra `Post1`, `Post2`, `Post3`, e os três mais recentes `Post2`, `Post3`, `Post5`. É a mesma coisa, estou abrindo `Post5`, mas o tempo também é `Post1`, `Post2`, `Post3`, mas não `Post2`, `Post3`, `Post4`. Existem 3 artigos neste artigo, que escrevi várias vezes desde que nasci, e escrevi várias frases desde então.

Dadas as circunstâncias do número de animais atribuídos, esperamos que seja possível actualizar os três artigos recentemente, mas não é o mais antigo (claro, também é possível definir o número de animais, as sentenças dos animais atribuídos ). Portanto, atualizei o seguinte, em `_includes/related-posts.html`{: .filepath} (isso também está em gem Baoli),

<!-- {% raw %} -->
```diff
{% for category in page.categories %}
  {% assign match_posts = match_posts | push: site.categories[category] | uniq %}
{% endfor %}

{% for tag in page.tags %}
  {% assign match_posts = match_posts | push: site.tags[tag] | uniq %}
{% endfor %}

+ {% assign match_posts = match_posts | reverse %}
{% assign last_index = match_posts.size | minus: 1 %}
{% assign score_list = '' | split: '' %}
```
{: file='_includes/related-posts.html'}
<!-- {% endraw %} -->

## 5. Seção de teste de adição
A área de revisão é utilizada pelo giscus, o autor do modelo concluiu a seleção da seleção geral e as informações pessoais podem ser preenchidas em `_config.yml`{: .filepath}.

[Uso avançado](https://github.com/giscus/giscus/blob/main/ADVANCED-USAGE .md).

## 6. Aumento da contagem de estações
A preferência do criador do modelo é usar o formato flex, diretamente em `_includes/footer.html`{: .filepath} 文体（é aqui que está a gema bauri), após a impressão, insira o conteúdo no meio [fuurushi](https :/ /busuanzi.ibruce.info/)Sucesso imediato na lista de pernas, `uv` 和 `pv` é um método de cálculo detalhado, solução específica, consulte [Curso](https://ibruce.info/ 2015/04 /04/busuanzi/).

<!-- {% raw %} -->
```html
<!-- contagem estatisticas -->
<p> 
  {% include footer-busuanzi.html %}
</p>
```
{: file="_includes/footer.html"}
<!-- {% endraw %}) -->

Em `_includes/footer-busuanzi.html`{: .filepath}:
```html
<!-- Não é uma má ideia, é grátis (footer.html) -->
<script async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<i class="fa fa-user" aria-hidden="true"></i> <span id="busuanzi_value_site_uv"></span> |
<i class="fa fa-eye" aria-hidden="true"></i> <span id="busuanzi_value_site_pv"></span>
````
{: file="_includes/footer.html"}

Detalhes adicionais sobre as informações da conta da estação (conteúdos como quantidade de serviço, área de atendimento, detalhes da área de atendimento, etc.) podem ser usados [Google Analytics](https://analytics.google.com/analytics/web/#/provision) Obtenha-o em `_config.yml` ID de assinatura disponível agora.

## 7. Animação de fundo aprimorada
Referência [@NichtsHsu](https://nihil.cc/) Design do usuário, função de animação de fundo adicionada. Adicionado em `_layouts/default.html`{: .filepath}

<!-- {% raw %} -->
```html
{% if site.backgroud_animation %}
  {% include animated-background.html %}
{% endif %}
```
{: file="_layouts/default.html"}
<!-- {% endraw %}) -->

Novo item de construção `_includes/animated-background.html`{: .filepath} Use a animação de configuração, que é a adição do círculo de animação.

```html
<div id="animação">
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
<div class="animation-circle"></div>
</div>
````
{: file="_includes/animated-background.html"}

Em `assets/css/jekyll-theme-chirpy.scss`{: .filepath},
```scs
/* Animação de geração */
@keyframes infrarot {
de {
-webkit-transform: girar(0deg);
}
  
para {
-webkit-transform: girar (360 graus);
}
}
  
.icon-loading1 {
display: bloco embutido;
animação: infirot 1s linear infinito;
-webkit-animação: infirot 1s linear infinito;
}
  
@function intervalo_aleatório($min, $max) {
$rand: aleatório();
$random_range: $min + floor($rand * (($max - $min) + 1));
@return $random_range;
}
  
#animação {
posição: fixa;
superior: 0;
esquerda: 0;
largura: 100%;
altura: 100%;
estouro: oculto;
eventos de ponteiro: nenhum;
  
@keyframes animados {
0% {
transformar: traduzirY(0) girar(0deg);
opacidade: 1;
raio da borda: 0;
}
100% {
transformar: traduzirY(-1200px) girar(720deg);
opacidade: 0;
raio da fronteira: 50%;
}
}
  
@media todos e (largura mínima: 1200px) {
.círculo de animação {
posição: absoluta;
esquerda: var(--círculo-esquerda);
inferior: -300px;
exibição: bloco;
plano de fundo: var(--círculo-fundo);
largura: var(-comprimento do lado do círculo);
altura: var(--comprimento do lado do círculo);
animação: animar 25s linear infinito;
duração da animação: var(--circle-time);
atraso de animação: var(--círculo-atraso);
eventos de ponteiro: nenhum;
  
@for $i de 0 a 50 {
&:nésimo-filho(#{$i}) {
--círculo-esquerda: #{intervalo_aleatório(0%, 100%)};
--circle-background: rgba(#{random_range(0, 255)}, #{random_range(0, 255)}, #{random_range(0, 255)}, 0.06);
--circle-side-length: #{random_range(20px, 200px)};
--circle-time: #{random_range(10s, 45s)};
--circle-delay: #{random_range(0s, 25s)};
}
}
}
}
  
@media todos e (largura máxima: 1199px) {
.círculo de animação {
Mostrar nenhum;
}
}
}
````
{: file="assets/css/jekyll-theme-chirpy.scss"}

Na configuração `_config.yml`{: .filepath} `backgroud_animation: true` efeito de animação imediatamente disponível.

Esta parte será usada para criar um efeito de animação, que inclui as seguintes partes:

1. `@keyframes infirot` Definição de um nome de animação chave do `infirot`, rotação do elemento de 0 graus a 360 graus.
2. `.icon-loading1` para uso com animação `infirot`, que pode ser colocada em circulação ilimitada.
3. `@function random_range($min, $max)` é uma função fixa e é usada para gerar um número aleatório dentro do intervalo especificado.
4. `#animation` é um contêiner com posição fixa, que pode ser usado para conter efeitos de animação.它inclui uma parte da animação `animate`, que altera a transparência do movimento na superfície do elemento. À medida que esse movimento se move, o elemento se move na direção vertical, sobe, gira, desaparece e, ao mesmo tempo, o raio do quadro também muda.
5. `#animation` contém mídia e diferentes expressões para diferentes tipos de leitura e visualização. Nas circunstâncias de 1200px, o grupo gera uma série de círculos coloridos, o efeito de animação de cada círculo, a posição de cada círculo, a cor, o tamanho, o período de tempo e o período de tempo em que é gerado. Nas circunstâncias de um tamanho pequeno de 1200px, a imagem não foi produzida e não é mostrada. Portanto, o efeito de animação não pode ser visto no PC, mas ainda é possível.

## 8. Maior contribuição do GitHub

Use o item principal do GitHub [gh-contrib-graph](https://github.com/lengthylyova/gh-contrib-graph), assine o HTML abaixo:

```html
<!-- ENTRA NA CABEÇA -->
<link rel="stylesheet" href="http://lengthylyova.pythonanywhere.com/static/gh-contrib-graph/gh.css">

<!-- ENTRA NO CORPO -->
<div id="gh" data-login="YOUR_GITHUB_LOGIN"></div>

<!-- VAI PARA O FINAL DO CORPO -->
<script src="http://lengthylyova.pythonanywhere.com/static/gh-contrib-graph/gh.js"></script>
````

Geral `YOUR_GITHUB_LOGIN` Apelido revisado do github disponível imediatamente.

<div class="box-info" markdown="1">
<div class="title"> Construção </div>
Minha configuração pessoal é `assets/css/jekyll-theme-chirpy.scss`{: .filepath} Introduziu texto de estilo de bloco CSS externo, agora (o lado inferior é meu estilo de bloco autoconfigurado)

```scs
@importar url('http://lengthylyova.pythonanywhere.com/static/gh-contrib-graph/gh.css');

.ghCalendarHeader {
margem inferior: 1rem;
cor:var(--cor do texto);
}
.ghThumbNail{
Mostrar nenhum;
}
#gh a {
decoração de texto: nenhuma;
cor: var(--link-color);
}
.ghCalendarCard {
borda: var(--linguagem-borda-cor) 1px sólido;
raio da borda: 0,5rem;
}
````
{: file="assets/css/jekyll-theme-chirpy.scss"}

Depois disso, você pode transferir imediatamente para a área local para aderir à demanda (`.md` suporta linguagem HTML), o efeito é mostrado abaixo:

![github-contrib](github-contrib.PNG)
_Doação do GitHub_

> Eu não gosto disso, então não estou feliz com isso, então estou livre para brincar com isso `about.md`{:.filepath} Esta é uma escolha não trivial.
</div>

## 9. Adição de 4 novos prompts
4 peças de prompt, efeito abaixo:

> Ser ou não ser. Essa é uma questão.
{: .prompt-info}

> Ser ou não ser. Essa é uma questão.
{: .prompt-dica}

> Ser ou não ser. Essa é uma questão.
{: .aviso de prompt}

> Ser ou não ser. Essa é uma questão.
{: .prompt-perigo}

Com base nisso, construí um novo prompt, o efeito é o seguinte:

<div class="box-info" markdown="1">
<div class="title">Shakespeare</div>
Ser ou não ser. Essa é uma questão.
</div>

<div class="box-tip" markdown="1">
<div class="title">Shakespeare</div>
Ser ou não ser. Essa é uma questão.
</div>

<div class="box-warning" markdown="1">
<div class="title">Shakespeare</div>
Ser ou não ser. Essa é uma questão.
</div>

<div class="box-danger" markdown="1">
<div class="title">Shakespeare</div>
> Ser ou não ser. Essa é uma questão.
> ---Shakespeare

$$x^2 + y^2 =z^2$$

</div>


Claro, também é possível e o efeito é o seguinte:

<div class="box-info" markdown="1">
Ser ou não ser. Essa é uma questão.
</div>

<div class="box-tip" markdown="1">
Ser ou não ser. Essa é uma questão.
</div>

<div class="box-warning" markdown="1">
Ser ou não ser. Essa é uma questão.
</div>

<div class="box-danger" markdown="1">
Ser ou não ser. Essa é uma questão.
</div>

A ideia é que esta função esteja realmente disponível, mas apenas disponível em `assets/css/jekyll-theme-chirpy.scss`{: .filepath}.

```scs
/* design estilo colorbox */
/* definido box-info, box-tip, box-warning, box-danger 4 tipos colorbox */
@mixin colorbox($border-color, $icon-color, $icon-content, $bg-color, $fa-style: 'solid') {
borda esquerda: .2rem sólido $border-color;
raio da borda: 0,25rem;
cor: var(--cor do texto);
preenchimento: 0,6rem 1rem 0,6rem 1,5rem;
sombra da caixa: var(--linguagem-border-color) 1px 1px 2px 1px;
posição: relativa;
margem inferior: 1rem;
  
> div.title::before {
conteúdo: $ ícone-conteúdo;
cor: $ cor do ícone;
fonte: var(-fa-font-#{$fa-style});
alinhamento de texto: centro;
largura: 3rem;
posição: absoluta;
esquerda: .2rem;
margem superior: .4rem;
renderização de texto: automático;
-webkit-font-smoothing: suavizado;
}
  
> div.título {
cor de fundo: $bg-color;
cor: $ cor do ícone;
preenchimento: 0,5rem 0,6rem 0,5rem 3rem;
margem: -.6rem -1rem .6rem -1,5rem;
peso da fonte: 600;
}
    
>p:último-filho{
margem inferior: 0;
}
}
  
/* informações da caixa azul */
.box-info {
@incluir caixa de cores(
var(--prompt-info-icon-color),
var(--prompt-info-icon-color),
"\f06a",
var(--prompt-info-bg)
);
}

/* ponta da caixa verde */
.box-tip {
@incluir caixa de cores(
var(--prompt-tip-icon-color),
var(--prompt-tip-icon-color),
"\f0eb",
var(--prompt-tip-bg),
'regular'
);
}

/* caixa de aviso amarelo */
.box-warning {
@incluir caixa de cores(
var(--prompt-warning-icon-color),
var(--prompt-warning-icon-color),
"\f06a",
var(--prompt-warning-bg)
);
}

/* caixa-perigo vermelho */
.box-perigo {
@incluir caixa de cores(
var(--prompt-perigo-icon-cor),
var(--prompt-perigo-icon-cor),
"\f071",
var(--prompt-danger-bg)
);
}
````
{: file="assets/css/jekyll-theme-chirpy.scss"}

## 10. Detalhes do projeto do sistema elementar
HTML neutro `<details class="details-block">` Os elementos podem ser construídos como um único conjunto, mas quando a alteração for feita, o conteúdo da apresentação é o seguinte e o efeito é o seguinte:

<detalhes class="detalhes-block" markdown="1">
<summary>Detalhes</summary>
A luz brilhante da lua em frente à cama, duvido que haja geada no chão.举头 Wangmingyue, pensamento baixo era 乡.

$$
x^2 + y^2 =z^2, \quad x_{1,2} = \frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$

</detalhes>

Frase de redução 输 `` `` `` `` `码` `` `` `` `` `` `` `` `` `` ``设 设 设 设 设 设 设 设 设
```redução
<detalhes class="detalhes-block" markdown="1">
<summary>Detalhes</summary>
A luz brilhante da lua em frente à cama, duvido que haja geada no chão.举头 Wangmingyue, pensamento baixo era 乡.

$$
x^2 + y^2 =z^2, \quad x_{1,2} = \frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$

</detalhes>
````

A adição do design padrão foi concluída em `assets/css/jekyll-theme-chirpy.scss`{: .filepath}, e o seguinte pode ser adicionado imediatamente (observe que as seguintes alterações foram feitas com base no seguinte ):
```scs
// detalhes 样design de estilo
detalhes {
raio da fronteira: 0,25rem;
borda esquerda: .2rem solid var(--prompt-tip-icon-color);
box-shadow: var(--language-border-color) 1px 1px 2px 1px; /* Quantidade de mudança de cor do quadro emprestado */
margem inferior: 1rem;
preenchimento: 0,6rem 1rem 0,6rem 1,5rem;
>p:último-filho{
margem inferior: 0;
}
}

detalhes > resumo {
preenchimento: 0,5rem 1,0rem 0,5rem 1,0rem;
margem: -.6rem -1rem -.6rem -1,5rem;
peso da fonte: 600;
cor de fundo: var(--prompt-tip-bg);
cor: var(--prompt-tip-icon-color);
decoração de texto: sublinhado;
posição: relativa;
estilo de lista: nenhum; /* 蚐藏默认的训头 */
transição: facilidade de cor de fundo 0,3s /* Adicionado efeito de cor */
}

detalhes > resumo::-webkit-details-marker {
display: nenhum /* 蚐藏默认的训头 */
}
detalhes > resumo::marcador {
conteúdo: nenhum; /* 蚐藏默认的训头 */
}

detalhes > resumo::antes {
/* Estado fechado */
/* Também pode ser usado para outros símbolos ou símbolos autodefinidos, em comparação com caracteres Unicode */
// conteúdo: '🙈';
/* conteúdo:'\002B9A';
conteúdo: '😼';
margem direita: 0,5rem;
display: bloco embutido;
}
detalhes[abrir] > resumo::antes {
/* Estado de expansão */
/* conteúdo: '🐵';*/
/* conteúdo: '\002B9B';
conteúdo: '🙀';
animação: my-cat .2s easy-in-out /* Efeito de animação com animação */
margem direita: 0,5rem;
}

detalhes > resumo::depois {
família de fontes: 'Font Awesome 6 grátis';
content: "\f105" /* Unicode para fa-angle-down */
display: bloco embutido;
transição: facilidade de transformação de 0,2s /* Adicionada animação de rotação */
posição: absoluta;
right: 1rem; /* A posição de ajuste é a posição mais à direita */
}
detalhes[abrir] > resumo::depois {
transformar: girar (90 graus);
}

detalhes[abrir] > resumo{
// transição: margem 200ms de atenuação /* Exposição com efeito de animação */
margem inferior: 0,6rem;
}

@keyframes meu-gato {
50% { transform: scale(1.3 } /* efeito de animação */
}
````
{: file="assets/css/jekyll-theme-chirpy.scss" }



## 11. Implementação LQIP Python
LQIP (Low Quality Image Placeholder) O índice é um espaço reservado para imagem de baixa qualidade, este é um tipo de tecnologia de melhoria de desempenho, há uma imagem de alta qualidade antes, o primeiro é um espaço reservado para imagem de baixa qualidade e uma imagem de modelo de baixa taxa de distribuição foi fornecida desde então. Vários tipos de imagens podem ser usados para ajudar a reduzir o número de páginas, e o visualizador pode visualizá-las em alta velocidade.

![LQIP](lqip.png)
_Espaços reservados para imagens de baixa qualidade, de [daun](https://processwire.com/modules/image-placeholders/)._

O autor adicionou esse recurso e a seção de pré-palavra de cada texto pode ser colocada no lqip. Posso copiar uma cópia da versão Python, salvar a imagem do caractere geral e convertê-la para base64. Isso é basicamente baseado em meu próprio caminho de texto e posso ajustar minha própria direção se houver demanda.

```píton
da imagem de importação PIL, ImageFilter
importar base64
importar piperclip

def imagem_lqip(caminho_da_imagem,caminho_da_imagem_saída,comprimento=16,largura=8,raio=2):
"""
Gere LQIP (espaço reservado para imagem de baixa qualidade).
    
Número de referências:
- image_path: caminho do caminho da imagem original
- output_image_path: Caminho do documento LQIP de saída
- Comprimento: O comprimento da imagem após o ajuste, o comprimento da imagem 16
- largura: largura da imagem após ajuste, leitura em preto 8
- raio: raio do modelo de alta velocidade、默认为 2
    
Responder:
- espeto de caracteres base64
"""
im = Imagem.open(caminho_da_imagem)
im = im.resize((comprimento,largura))
im = im.convert('RGB')
im2 = im.filter(ImageFilter.GaussianBlur(raio))
im2.save(output_image_path)

# 转城 Base64 编码
com open(output_image_path, "rb") como image_file:
string_codificada = base64.b64encode(image_file.read())
base64_string=string_codificada.decode('utf-8')
    
retornar base64_string

image_start = "../huanyushi.github.io"
fim_imagem = entrada()
caminho_imagem = início_imagem + fim_imagem

base64_image = image_lqip(image_path, "test.jpg")

pyperclip.copy('data:image/jpg;base64,'+ base64_image) # imprime como resultado
imprimir(imagem_base64)
print(image_end) # Este é o artigo que você deseja enviar.
````

Como regra geral, base64, você pode usar a seguinte sequência de programa Python.

```píton
importar base64

def save_base64_image(base64_string, caminho_de_saída):
"""
Postado em base64 e salvo como personagem.
    
Número de referências:
- base64_string: sequência de caracteres base64
- output_path: caminho do caminho da imagem de saída
"""

# Espeto de código Base64
dados_decodificados = base64.b64decode(base64_string)
    
# O número de estátuas preservadas após a guerra
com open(output_path, 'wb') como image_file:
arquivo_de_imagem.write(dados_decodificados)

# Esta é uma peça do padrão do artista Riyo, e este exemplar está exposto desde então.
base64_string = "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQgJCQwLDBgNDRgyIRwh MjIyMJ IEAwUFBAQAAAF9A QIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl 5iZmqKjpKWmp6ipq rKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQE BAQAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAEC AxEEBSExBhJBUQdhcRMiMoEIFE KRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmq srO0tba3uLm6wsPExcbHyMnK0 tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwB1s4jcEmpLtg7ZU0UV9jb3rnwt/csf/9k="
save_base64_image(base64_string, "decoded_image.webp")
````

## 12. Implementação Anticolor Python
O blog suporta o modelo de cor escura, a mesma parte da peça da imagem também pode ser alterada para o modelo de cor escura. A peça da imagem da peça pode ser passada diretamente pelo método de cor oposta, mas não possui, observe que a cor oposta é diferente do escuro cor!），Peguei uma cópia de um programa Python que pode ser alterado para um modelo de cor escura e a demanda pode ser alterada por si só. No mesmo local, o caminho do artigo também é baseado em minhas próprias circunstâncias reais, e a demanda está relacionada à configuração:

```píton
da imagem de importação PIL, ImageChops
importar matplotlib.pyplot como plt

def cor_invertida(fnome):
im = Imagem.open(fname)
se im.mode == "P":
im = im.convert('RGB')
im_inverted=ImageChops.invert(im)
# Estou perto()
retorne eu, estou_invertido

# Esta parte é ajustada ao caminho da peça da imagem
path_start = "../huanyushi.github.io/assets/img/in-post/"
path_end = '2023-03-23/prefácio.PNG'
caminho_imagem = caminho_início + caminho_fim

origem_da_imagem, imagem_invertida = cor_invertida(caminho_da_imagem)

# Pode ser removido diretamente da lista
plt.subtrama(121)
plt.título('original')
plt.axis('desligado')
plt.imshow(origem, cmap='cinza', vmin=0, vmax=255)
plt.subtrama(122)
plt.title('inverso')
plt.imshow(image_output, cmap='cinza', vmin=0, vmax=255)
plt.axis('desligado')
plt.show()

# Fragmento de preservação
image_output.save(image_start + image_end.replace('.', '-dark.')) # Como: test.PNG Salvar imagem anticolor generativa test-dark.PNG
````
![comparação inversa](inverse.png){:.light}
![comparação inversa](inverse-dark.png){:.dark}
_Comparação da peça da imagem colorida reversa da peça da imagem Yohara_


## 13. Outras questões
### 13.1. falha no git push: não foi possível conectar ao servidor.
O item de texto principal foi enviado ao github até a distância, e a aparência de `não foi possível conectar ao servidor` foi alterada. As seguintes medidas são **possíveis e eficazes** (o terceiro tipo é mais eficaz):

1. Teste de reenvio VPN Ladder (VPN) abaixo;
2. Agente para cancelamento de pedidos atuais.
```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
````
1. Nas circunstâncias da escada de abertura. Clique no canto inferior direito para se conectar à Internet, clique aqui para acessar a Internet, clique aqui para ver a localização e clique em 127.0.0.1:7890. Importar enquanto estiver no comando
```concha
git config --global http.proxy http://127.0.0.1:7890
````

Você pode passar `git config --global -l` para ver se a instalação foi bem-sucedida. Depois disso, você pode prosseguir novamente com push.

### 13.2.
Quantos, quão pequenos, quantas peças, quantas peças, quantas peças, etc. Veja como posso explorá-lo:

1. 对洹客设设增设讞组(对对庹新构珄发发生的文本、因此每次次应新构组组结构个方),
É possível adicionar `_config.yml`{: .filepath} dentro de `incremental: true`, e depois disso, jekyll Toshoju novo texto de construção e renovação. Claro, o método apropriado é usar `bundle exec jekyll s --incremental` ou `bundle exec jekyll s --I`.
2. Independentemente do tamanho da imagem, é também uma espécie de esquema de aceleração.

### 13.3.
Use o elemento `<iframe>` pronto, como
```html
<iframe src="caminho do arquivo" width="100%" height='800'></iframe>
````
É possível utilizar a técnica em post, em HTML, PDF, etc.

<div class="box-danger" markdown="1">
<div class="title">Aviso</div>
É possível usar o dispositivo de medição normalmente, mas outros dispositivos de medição têm suporte indefinido e não há transbordamento, portanto, use com cuidado!
</div>

### 13.4. Blog no meio do tópico Python
O post está aqui e abaixo, é possível usar Python

```html
<iframe
src="https://jupyterlite.github.io/demo/repl/index.html?kernel=python&toolbar=1"
largura="100%"
altura="500px">
</iframe>
````

### 13.5. Possíveis recursos úteis.

<div class="box-tip" markdown="1">
<div class="title"> Possíveis recursos úteis </div>
- [TinyPNG](https://tinypng.com/): 1 download gratuito da imagem na tela, mas é possível ler o vídeo na tela, mas é 70% mais eficiente.
- [PageSpeed Insights](https://pagespeed.web.dev/): Uma ferramenta para verificar o desempenho da rede, fornecer um relatório sobre como melhorar a rede e melhorar a velocidade da rede.
- [Coolors](https://coolors.co/), [Color Hunt](https://www.colorhunt.co/): Estação de cores on-line disponível, esquemas de cores recomendados disponíveis desde então.
</div>
