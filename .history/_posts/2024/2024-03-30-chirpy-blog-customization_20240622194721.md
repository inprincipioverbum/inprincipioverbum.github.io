---
title:      "Chirpy Blog Customization"
date:       2024-03-30
categories: [HTML and CSS]
tag: [HTML, CSS]
math: true
pin: true
media_subpath : /assets/img/in-post/2024/2024-03-30/
description: "Introdução à personalização baseada no Jekyll-Theme-Chirpy v7.0.0: configuração do MathJax, estilos da barra lateral, estatísticas do site do rodapé, animações de fundo, novos estilos de elementos personalizados e de detalhes, implementação Python de LQIP e imagens invertidas, etc."
---

Introdução à personalização baseada no Jekyll-Theme-Chirpy v7.0.0: configuração do MathJax, estilos da barra lateral, estatísticas do site do rodapé, animações de fundo, novos estilos de elementos personalizados e de detalhes, implementação Python de LQIP e imagens invertidas, etc.

 
1\. Introdução[](#1-简介)
-----------------------

No ano passado eu implantei um site de blog estático no GitHub com Jekyll e funcionou ao meu gosto.

Mas eu estava originalmente usando [Huxpro](https://github.com/Huxpro/huxpro.github.io) como um modelo, e recentemente passei um pouco de tempo mudando o modelo para [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/)。 No passado, Jekyll misturou estilos de tema com conteúdo de blog, o que não era bom para edição, mas após a versão 3.2.0, Jekyll introduziu , que encapsula o estilo do site em um pacote gem, que separa o estilo do tema do conteúdo do blog (que é um pouco semelhante ao HTML e CSS). O modelo Chirpy é exatamente o mesmo, então o blog gerado pelo Chirpy Starter contém apenas o arquivo de conteúdo e, para personalizar o modelo Quirpy, você deve encontrar seu arquivo de estilo.`gem-based theme``gem-based theme`

Há dois métodos para escolher. A primeira maneira é ir diretamente para a página do projeto github Chirpy e extrair os arquivos de estilo e código de seu código-fonte. A segunda é usar o git para obter o endereço do arquivo de estilo encapsulado através do comando, como mostra a figura abaixo`bundle info --path jekyll-theme-chirpy`

[![arquivo de tema](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/theme-file.PNG)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/theme-file.PNG) _O endereço do arquivo de estilo encapsulado_

Depois de encontrar o arquivo de estilo correspondente nele, coloque-o no arquivo correspondente do seu blog e você poderá personalizá-lo.

> A imagem está presa na versão 6.5.5, mas a nova versão é semelhante e não será atualizada.

Observe que, ao gerar um blog, o arquivo de estilo colocado em sua própria pasta substituirá o arquivo com o mesmo nome no pacote gem original, enquanto o arquivo de estilo não modificado ainda será lido do pacote gem, portanto, o arquivo de estilo não modificado não precisa ser importado, o que também é conveniente para seguir o autor do modelo para atualizações subsequentes. Este artigo é apenas para documentar algumas das alterações que fiz no Chirpy (não vou escrever sobre algumas pequenas alterações).`.github.io`

2\. Modifique a configuração do MathJax[](#2-修改-mathjax-配置)
-----------------------------------------------------------

Desde que o MathJax entrou na era 3.x, a velocidade de renderização de fórmulas matemáticas é quase tão rápida quanto o KaTeX, e considerando que o MathJax suporta pacotes de expansão ricos e tem funções mais poderosas do que o KaTeX, o MathJax é uma prioridade. As configurações do autor do modelo para MathJax podem ser modificadas no arquivo e encontrando o código correspondente no pacote de gemas ocultas.`assets/js/data/mathjax.js`

### 2.1. MathJax adiciona pacotes de expansão[](#21-mathjax-添加拓展包)

Adicionadas algumas extensões, como , bem como macros personalizadas (entrada de fórmula simplificada) e ativado o modo de carregamento lento (que acelera o carregamento de páginas da Web). As mudanças de código são as seguintes (mais podem ser encontradas na documentação oficial do MathJax):`physics`

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34  --- layout: compress # WARNING: Don't use '//' to comment out code, use '{% comment %}' and '{% endcomment %}' instead. ---  {%- comment -%}   See: <https://docs.mathjax.org/en/latest/options/input/tex.html#tex-options> {%- endcomment -%}  MathJax = {   loader: { load: ['[tex]/physics','ui/lazy',] },   tex: {     inlineMath: [       ['$', '$'],       ['\\(', '\\)']     ],     displayMath: [       ['$$', '$$'],       ['\\[', '\\]']     ],     packages: {'[+]': ['physics']},     tags: 'ams',     macros: {         'e': '\\mathrm{e}',         'RR': '\\mathbb{R}',         'ZZ': '\\mathbb{Z}',         'QQ': '\\mathbb{Q}',       },   }   options: {     lazyMargin: '200px',   },   svg: { fontCache: 'global'}, };`

### 2.2. Adicionar visualização da fórmula de visualização da página inicial[](#22-增加主页-preview-公式预览)

Na página inicial do blog, o código matemático será exibido diretamente na seção de visualização de cada postagem e, se você quiser visualizar a fórmula na página inicial, consulte o [problema-1140](https://github.com/cotes2020/jekyll-theme-chirpy/issues/1140).

> Não há essa intenção por enquanto, e essa característica parece ser relativamente frívola. Vamos abri-lo novamente se você precisar fazê-lo no futuro.

3\. Modifique o estilo da barra lateral[](#3-修改侧边栏样式)
-----------------------------------------------------

### 3.1. Adicionar uma imagem de fundo à barra lateral[](#31-侧边栏增加背景图片)

No arquivo, adicione o código CSS para o estilo da barra lateral, que é o comando básico usado para adicionar a imagem de fundo, basta adicionar a URL da imagem no final, da seguinte maneira:`assets/css/jekyll-theme-chirpy.scss``background-image`

`1 2 3 4 5 6  #sidebar {     background-image: url(https://cdn.jsdelivr.net/gh/huanyushi/Blog-Image-Bed@main/assets/img/background.jpg); /* <- change background image */     background-size: cover; /* <- customize the image size */     background-repeat: no-repeat; /* <- no-repeat */     background-position: top; /* <- image position */ }`

Também preste atenção para modificar a cor do texto correspondente, eu escolhi um fundo escuro aqui, para que o texto correspondente é branco,

`1 2 3 4 5 6 7 8 9 10 11 12 13 14  #sidebar .site-title a {     color: #ffffff;      text-shadow: 5px 5px 10px rgba(0,0,0,0.5); } #sidebar .site-subtitle {     color: #ffffff;     text-shadow: 2px 2px 3px rgba(0,0,0, 0.7); } #sidebar .sidebar-bottom .mode-toggle, #sidebar a {     color: #ffffff; } #sidebar .sidebar-bottom .btn {     color: var(--sidebar-btn-color); }`

### 3.2. 侧边栏增加友链[](#32-侧边栏增加友链)

在隐藏的 gem 包里找到 文件，在其中添加以下代码（当有友链时，则插入 文件）：`_includes/sidebar.html``friends.html`

`1 2 3 4    <!-- Friends link -->   {% if site.data.friends %}       {% include friends.html %}   {% endif %}`

新建一个 文件，将友链设置放入其中（这样模板更新时可以尽可能减少对模板代码的修改）：`_includes/friends.html`

`1 2 3 4 5 6 7 8 9 10  <!-- 友链设置，在 sidebar.html 中插入 --> <div class="friends">     <hr style="color:white;border: 1px solid ">     <p><i class="fas fa-user-friends"></i><span>FRIENDS</span></p>     <ul>       {% for friend in site.data.friends %}       <li><a href="{{friend.href}}">{{friend.title}}</a></li>       {% endfor %}     </ul> </div>`

而相关的样式设置添加到了 中，如下：`assets/css/jekyll-theme-chirpy.scss`

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31  /* 侧边栏友链样式设置 */ #sidebar .friends {     padding-left: 2.5rem;     padding-right: 1.25rem;     width: 100%;     margin-bottom: 1.5rem; } #sidebar .friends p {     color: rgb(255,255,255,0.95);     font-family: inherit;     font-weight:600;     font-size: 95%; } #sidebar .friends p i {     opacity: 0.8;     margin-right: 1.5rem; } #sidebar .friends p span {     letter-spacing: 0.2px;     opacity: 0.9; } #sidebar .friends ul {     color:white;     font-size:95%;     opacity: 0.95;     margin-bottom: 0rem; } #sidebar .friends ul li {     margin-bottom: 0.4rem;     opacity: 0.9; }`

已成功封装，只需要在 里添加以下设置即可（可以一直往后叠加）：`_data/friends.yml`

`1 2 3 4 5 6  - title: "Title1"   href: "https://example.com" - title: "Title2"   href: "https://example.com" - title: "Title3"   href: "https://example.com"`

[![friend example1](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/friend1.png)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/friend1.png)

[![friend example2](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/friend2.png)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/friend2.png)

[![friend example3](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/friend3.png)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/friend3.png)

注意

1.  友链不能加太多，容易挤占底部社交平台的空间，让它跑到屏幕外面去了（不过这也和系统分辨率有关系）。如果友链太多建议在侧边栏新开一个选项卡，也就是新建一个 。`_tabs/friends.md`
2.  我这里设置的是友链沉底，保持在底部社交平台上方。如果分辨率拉大，会发现它和上面侧边栏选项卡之间有很大间距。如果想调整友链位置紧跟选项卡之后，可以在 中修改选项卡的样式，将 中的 删除；并加入到友链样式中原先的 修改为 。同时 中 里的 修改为上间距 , ? 的值可以自己选定。`_includes/sidebar.html``<nav class="flex-column flex-grow-1 w-100 ps-0">``flex-grow-1``<div class="friends">``<div class="friends flex-grow-1">``assets/css/jekyll-theme-chirpy.scss``#sidebar .friends``margin-bottom: 2rem``margin-top: ? rem`

4\. 修改 further reading 的文章顺序[](#4--修改-further-reading-的文章顺序)
------------------------------------------------------------

按我的理解这应该是模板的一个 bug，所以我把这部分更新写成一个 PR 提交给原作者了，请见 [refactor: make Further Reading display the latest posts.](https://github.com/cotes2020/jekyll-theme-chirpy/pull/1699)。

> Este PR foi **mesclado** pelos autores e não precisará ser alterado no Chirpy 7.0.0 e posterior, ignore esta seção.

Vamos começar descrevendo o problema, digamos que temos 5 artigos diferentes, em ordem de tempo de publicação do anterior para o mais recente, , , , ou seja:`Post1``Post2``Post3``Post4``Post5`

`1 2 3 4 5 6  _posts ├─ Post1.md ├─ Post2.md ├─ Post3.md ├─ Post4.md └─ Post5.md`

Ao abrir cada artigo, a parte inferior sugere os 3 artigos que melhor correspondem a ele (o algoritmo para correspondência de pontuações está em ). Mas agora o problema é que quando esses artigos têm as mesmas pontuações correspondentes, a Leitura Adicional na parte inferior sempre recomendará apenas os 3 artigos mais antigos e não os mais recentes, não importa qual artigo eu abra.`_includes/related-posts.html`

Por exemplo, quando abro , a parte inferior mostra , , em vez dos últimos 3 artigos. Da mesma forma, quando eu abro, ele também mostra , em vez de , , . Isso significa que não importa quantos artigos eu escreva depois, ele sempre mostrará apenas os 3 primeiros artigos.`Post4``Post1``Post2``Post3``Post2``Post3``Post5``Post5``Post1``Post2``Post3``Post2``Post3``Post4`

No caso da mesma pontuação de partida, podemos preferir recomendar os 3 artigos atualizados mais recentemente em vez dos mais antigos (é claro, você também pode definir um número aleatório para corresponder a artigos aleatórios). Então eu fiz as seguintes alterações, no (este arquivo também está no pacote gem),`_includes/related-posts.html`

`1 2 3 4 5 6 7 8 9 10 11  {% for category in page.categories %}   {% assign match_posts = match_posts | push: site.categories[category] | uniq %} {% endfor %} {% for tag in page.tags %}   {% assign match_posts = match_posts | push: site.tags[tag] | uniq %} {% endfor %} + {% assign match_posts = match_posts | reverse %} {% assign last_index = match_posts.size | minus: 1 %} {% assign score_list = '' | split: '' %}`

5\. Adicionar seções de comentários[](#5-增加评论区)
-----------------------------------------------

A seção de comentários usa giscus, e o autor do modelo já encapsula as opções relevantes, e pode preencher as informações pessoais no arquivo.`_config.yml`

Para obter um tutorial, consulte o projeto [giscus](https://giscus.app/) e, para obter mais informações sobre como configurar seus recursos avançados, consulte [Uso avançado](https://github.com/giscus/giscus/blob/main/ADVANCED-USAGE.md).

6\. Aumente as estatísticas do site[](#6-增加站点统计)
------------------------------------------------

O autor do modelo usa cuidadosamente o formato flex no rodapé, encontrar diretamente o arquivo (este arquivo está no pacote de gemas), e inserir nenhum [alho](https://busuanzi.ibruce.info/) no meio depois de copiar para exibir com sucesso as estatísticas do site no rodapé, e são os dois algoritmos estatísticos de visitas, consulte o [tutorial](https://ibruce.info/2015/04/04/busuanzi/) para explicações específicas.`_includes/footer.html``uv``pv`

`1 2 3 4  <!-- 站点统计 --> <p>    {% include footer-busuanzi.html %} </p>`

O código para não alho é definido em:`_includes/footer-busuanzi.html`

`1 2 3 4  <!-- 不蒜子站点统计，放在页脚处 (footer.html 中插入) --> <script async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script> <i class="fa fa-user" aria-hidden="true"></i> <span id="busuanzi_value_site_uv"></span> | <i class="fa fa-eye" aria-hidden="true"></i> <span id="busuanzi_value_site_pv"></span>`

Além disso, estatísticas mais detalhadas do site (como o número de usuários, regiões de usuários, quais páginas os usuários visitam, etc.) podem ser obtidas usando o [Google Analytics](https://analytics.google.com/analytics/web/#/provision), que pode ser obtido adicionando o ID no .`_config.yml`

7\. Adicionar animação de fundo[](#7-增加背景动画)
--------------------------------------------

Referindo-se ao design do blog de [@NichtsHsu](https://nihil.cc/), a função de animação em segundo plano foi adicionada. (Este arquivo também está incluído no pacote GEM).`_layouts/default.html`

`1 2 3  {% if site.backgroud_animation %}   {% include animated-background.html %} {% endif %}`

Criar um novo arquivo para animação é, na verdade, adicionar um monte de objetos que afetam o número de elementos que animam.`_includes/animated-background.html``animation-circle`

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52  <div id="animation">     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>     <div class="animation-circle"></div>   </div>`

E o design de estilo está em ,`assets/css/jekyll-theme-chirpy.scss`

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77  /* 生成动画 */ @keyframes infirot {     from {       -webkit-transform: rotate(0deg);     }        to {       -webkit-transform: rotate(360deg);     }   }      .icon-loading1 {     display: inline-block;     animation: infirot 1s linear infinite;     -webkit-animation: infirot 1s linear infinite;   }      @function random_range($min, $max) {     $rand: random();     $random_range: $min + floor($rand * (($max - $min) + 1));     @return $random_range;   }      #animation {     position: fixed;     top: 0;     left: 0;     width: 100%;     height: 100%;     overflow: hidden;     pointer-events: none;        @keyframes animate {       0% {         transform: translateY(0) rotate(0deg);         opacity: 1;         border-radius: 0;       }       100% {         transform: translateY(-1200px) rotate(720deg);         opacity: 0;         border-radius: 50%;       }     }        @media all and (min-width: 1200px) {       .animation-circle {         position: absolute;         left: var(--circle-left);         bottom: -300px;         display: block;         background: var(--circle-background);         width: var(--circle-side-length);         height: var(--circle-side-length);         animation: animate 25s linear infinite;         animation-duration: var(--circle-time);         animation-delay: var(--circle-delay);         pointer-events: none;            @for $i from 0 through 50 {           &:nth-child(#{$i}) {             --circle-left: #{random_range(0%, 100%)};             --circle-background: rgba(#{random_range(0, 255)}, #{random_range(0, 255)}, #{random_range(0, 255)}, 0.06); // 最后一个数为透明度             --circle-side-length: #{random_range(20px, 200px)};             --circle-time: #{random_range(10s, 45s)};             --circle-delay: #{random_range(0s, 25s)};           }         }       }     }        @media all and (max-width: 1199px) {       .animation-circle {         display: none;       }     }   }`

Defina para animar o efeito.`_config.yml``backgroud_animation: true`

Essa parte do código é usada para criar um efeito de animação e consiste nas seguintes partes:

1.  `@keyframes infirot` Uma animação de quadro-chave chamada é definida que gira o elemento de 0 graus a 360 graus.`infirot`
2.  `.icon-loading1` A animação é aplicada e definida como um loop infinito.`infirot`
3.  `@function random_range($min, $max)` Define uma função que gera um número aleatório dentro de um intervalo especificado.
4.  `#animation` é um contêiner com uma posição fixa que contém efeitos animados. Ele contém outra animação de quadro-chave que define a trajetória de movimento e as alterações de transparência do elemento na página. Essa animação faz com que o elemento se mova para cima e gire verticalmente, desaparecendo enquanto o raio da borda muda.`animate`
5.  `#animation` Contém duas consultas de mídia que aplicam estilos diferentes, dependendo da largura do visor. A 1200px ou maior, uma série de círculos coloridos são animados, cada um gerado aleatoriamente em termos de posição, cor, tamanho, duração e atraso. Em casos inferiores a 1200px, a animação circular fica oculta e não é exibida. Então você não pode ver animações no celular, mas você pode no PC.

8\. Adicionar gráfico de contribuição do GitHub[](#8-增加-github-贡献图)
-------------------------------------------------------------------

Usando um projeto no GitHub, [gh-contrib-graph](https://github.com/lengthylyova/gh-contrib-graph), adicione o seguinte código ao HTML:

`1 2 3 4 5 6 7 8  <!-- GOES INTO HEAD --> <link rel="stylesheet" href="http://lengthylyova.pythonanywhere.com/static/gh-contrib-graph/gh.css">  <!-- GOES INTO BODY --> <div id="gh" data-login="YOUR_GITHUB_LOGIN"></div>  <!-- GOES INTO THE END OF BODY --> <script src="http://lengthylyova.pythonanywhere.com/static/gh-contrib-graph/gh.js"></script>`

Altere o nome para seu nome de usuário do GitHub.`YOUR_GITHUB_LOGIN`

sugestão

Pessoalmente, recomendo importar um arquivo de estilo CSS externo no , ou seja, (abaixo está o código de estilo que eu mesmo defini)`assets/css/jekyll-theme-chirpy.scss`

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17  @import url('http://lengthylyova.pythonanywhere.com/static/gh-contrib-graph/gh.css');  .ghCalendarHeader {   margin-bottom: 1rem;   color:var(--text-color); } .ghThumbNail {   display: none; } #gh a {   text-decoration: none;   color: var(--link-color); } .ghCalendarCard {   border: var(--language-border-color) 1px solid;   border-radius: .5rem; }`

Em seguida, insira as duas linhas de código restantes onde você precisa adicionar (a linguagem HTML é suportada) e o efeito é mostrado na figura a seguir:`.md`

[![github-contrib](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/github-contrib.PNG)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/github-contrib.PNG) _Gráfico de contribuição do GitHub_

> Eu não adicionei porque era muito lento para carregar, então essa coisa é uma boa escolha em .`about.md`

9\. Adicionado 4 novos prompts[](#9-增加-4-个新的-prompt)
----------------------------------------------------

O autor do modelo configurou 4 prompts e o efeito é o seguinte:

> Ser ou não ser. Essa é uma questão.

> Ser ou não ser. Essa é uma questão.

> Ser ou não ser. Essa é uma questão.

> Ser ou não ser. Essa é uma questão.

Além disso, criei 4 novos prompts que se parecem com isto:

Shakespeare

Ser ou não ser. Essa é uma questão.

Shakespeare

Ser ou não ser. Essa é uma questão.

Shakespeare

Ser ou não ser. Essa é uma questão.

Shakespeare

> Ser ou não ser. Essa é uma questão.  
> — Shakespeare

x2+y2\=z2

Claro, você também pode deixá-lo sem um título, e o efeito é o seguinte:

Ser ou não ser. Essa é uma questão.

Ser ou não ser. Essa é uma questão.

Ser ou não ser. Essa é uma questão.

Ser ou não ser. Essa é uma questão.

Para fazer isso, basta adicionar o seguinte código ao :`assets/css/jekyll-theme-chirpy.scss`

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77  /* colorbox 样式设计 */ /* 定义了 box-info, box-tip, box-warning, box-danger 四种 colorbox */ @mixin colorbox($border-color, $icon-color, $icon-content, $bg-color, $fa-style: 'solid') {     border-left: .2rem solid $border-color;     border-radius: 0.25rem;     color: var(--text-color);     padding: .6rem 1rem .6rem 1.5rem;     box-shadow: var(--language-border-color) 1px 1px 2px 1px;     position: relative;     margin-bottom: 1rem;        > div.title::before {       content: $icon-content;       color: $icon-color;       font: var(--fa-font-#{$fa-style});       text-align: center;       width: 3rem;       position: absolute;       left: .2rem;       margin-top: .4rem;       text-rendering: auto;       -webkit-font-smoothing: antialiased;     }        > div.title {       background-color: $bg-color;       color: $icon-color;       padding: .5rem .6rem .5rem 3rem;        margin: -.6rem -1rem .6rem -1.5rem;       font-weight: 600;     }          > p:last-child{         margin-bottom: 0;     } }    /* box-info 蓝色 */ .box-info { @include colorbox(     var(--prompt-info-icon-color),     var(--prompt-info-icon-color),     "\f06a",     var(--prompt-info-bg) ); }  /* box-tip 绿色 */ .box-tip { @include colorbox(     var(--prompt-tip-icon-color),     var(--prompt-tip-icon-color),     "\f0eb",     var(--prompt-tip-bg),     'regular' ); }  /* box-warning 黄色 */ .box-warning { @include colorbox(     var(--prompt-warning-icon-color),     var(--prompt-warning-icon-color),     "\f06a",     var(--prompt-warning-bg) ); }  /* box-danger 红色 */ .box-danger { @include colorbox(     var(--prompt-danger-icon-color),     var(--prompt-danger-icon-color),     "\f071",     var(--prompt-danger-bg) ); }`

10\. Estilização dos elementos de detalhes[](#10-details-元素的样式设计)
-----------------------------------------------------------------

O elemento HTML pode criar um componente que só exibirá o conteúdo quando ele for alternado para um estado expandido, com os seguintes efeitos:`<details class="details-block">`

Detalhes

Suspeita-se que o luar brilhante em frente à cama seja geada no chão. Levante a cabeça para olhar para a lua brilhante e abaixe a cabeça para pensar em sua cidade natal.

Isso pode ser feito inserindo o seguinte código no arquivo Markdown, onde a sintaxe Markdown também pode ser usada dentro do elemento HTML e a adição de open a ele pode ser definida para o formulário de expansão padrão (caso contrário, ele é desabilitado por padrão):`markdown = "1"`

`1 2 3 4 5 6 7 8 9  <details class="details-block" markdown="1"> <summary>详细信息 </summary> 床前明月光，疑是地上霜。举头望明月，低头思故乡。  $$ x^2 + y^2 =z^2, \quad x_{1,2} = \frac{-b\pm\sqrt{b^2-4ac}}{2a} $$  </details>`

O design do estilo foi adicionado ao , basta adicionar o seguinte código (observe que meu estilo foi alterado com base no seguinte):`assets/css/jekyll-theme-chirpy.scss`

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69      // details 样式设计    details {        border-radius: .25rem;        border-left: .2rem solid var(--prompt-tip-icon-color);        box-shadow: var(--language-border-color) 1px 1px 2px 1px; /* 借用了代码框的边框颜色变量 */        margin-bottom: 1rem;        padding: .6rem 1rem .6rem 1.5rem;        > p:last-child{         margin-bottom: 0;     }    }      details > summary {         padding: .5rem 1.0rem .5rem 1.0rem;          margin: -.6rem -1rem -.6rem -1.5rem;         font-weight: 600;         background-color: var(--prompt-tip-bg);         color: var(--prompt-tip-icon-color);         text-decoration: underline;         position: relative;         list-style: none; /* 隐藏默认的箭头 */         transition: background-color 0.3s ease; /* 添加颜色过渡效果 */     }      details > summary::-webkit-details-marker {         display: none; /* 隐藏默认的箭头 */     }     details > summary::marker {         content: none; /* 隐藏默认的箭头 */     }      details > summary::before {         /* 关闭状态下 */         /* 也可以用其他符号或自定义图标，比如 Unicode 字符 */         // content: '🙈';          /* content:'\002B9A'; */         content: '😼';         margin-right: .5rem;         display: inline-block;     }     details[open] > summary::before {         /* 展开状态下 */         /* content: '🐵';*/           /* content: '\002B9B'; */         content: '🙀';         animation: my-cat .2s ease-in-out; /*  点击会有动画效果 */         margin-right: .5rem;     }      details > summary::after {         font-family: 'Font Awesome 6 Free';         content: "\f105"; /* Unicode for fa-angle-down */         display: inline-block;         transition: transform 0.2s ease; /* 添加旋转动画 */         position: absolute;         right: 1rem; /* 调整箭头在最右边的位置 */     }     details[open] > summary::after {         transform: rotate(90deg);     }      details[open] > summary{         // transition: margin 200ms ease-out; /* 展开会有动画效果 */         margin-bottom: .6rem;     }      @keyframes my-cat {         50%  { transform: scale(1.3); } /* 动画效果代码 */     }`

11\. Implementação Python do LQIP[](#11-lqip-的-python-实现)
---------------------------------------------------------

LQIP (Low Quality Image Placeholder) significa Low Quality Image Placeholder, que é uma técnica de otimização de desempenho de página da Web que carrega uma imagem leve, de baixa resolução e desfocada para fornecer uma visualização antes de carregar uma imagem de alta qualidade. Essa imagem de visualização pode ajudar a reduzir o tempo de carregamento da página e o consumo de largura de banda, melhorando a experiência visual dos visitantes.

[![LQIP](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/lqip.png)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/lqip.png) _Espaços reservados de imagem de baixa qualidade, da [daun](https://processwire.com/modules/image-placeholders/)._

O autor adicionou esse recurso ao modelo, basta definir o lqip no prefácio de cada documento. Eu escrevi um código Python que facilita compactar e desfocar a imagem, salvá-la e convertê-la em codificação base64. Isso é escrito de acordo com o caminho do meu arquivo, que pode ser ajustado se necessário.

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40  from PIL import Image, ImageFilter import base64 import pyperclip   def image_lqip(image_path,output_image_path,length=16,width=8,radius=2):     """     生成 LQIP（Low-Quality Image Placeholder）并保存到文件中，并返回base64编码的字符串。          参数：     - image_path：原始图像文件路径     - output_image_path：输出 LQIP 文件路径     - length：调整后图像的长度，默认为 16     - width：调整后图像的宽度，默认为 8     - radius：高斯模糊的半径，默认为 2          返回值：     - base64 编码的字符串     """     im = Image.open(image_path)     im = im.resize((length,width))     im = im.convert('RGB')     im2 = im.filter(ImageFilter.GaussianBlur(radius)) # 采用高斯模糊     im2.save(output_image_path)      # 转成 base64 编码     with open(output_image_path, "rb") as image_file:         encoded_string = base64.b64encode(image_file.read())         base64_string = encoded_string.decode('utf-8')          return base64_string  image_start = "../huanyushi.github.io" image_end = input() image_path = image_start + image_end   base64_image = image_lqip(image_path, "test.jpg")  pyperclip.copy('data:image/jpg;base64,'+ base64_image) # 将 print 结果导入粘贴里 print(base64_image) print(image_end) # 顺带输出一下导入的是什么文件`

Se você quiser converter cadeias de caracteres codificadas em base64 em imagens, você também pode usar o seguinte programa Python para convertê-las.

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21  import base64  def save_base64_image(base64_string, output_path):     """     将base64编码的字符串保存为图像文件。          参数：     - base64_string：base64编码的字符串     - output_path：输出图像文件路径     """      # 解码base64编码的字符串     decoded_data = base64.b64decode(base64_string)          # 将解码后的数据保存为图像文件     with open(output_path, 'wb') as image_file:         image_file.write(decoded_data)  # 这是模板作者里用的图片，当作例子来展示了。 base64_string = "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQgJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAAIABADASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwB1s4jcEmpLtg7ZU0UV9jb3rnwt/csf/9k=" save_base64_image(base64_string, "decoded_image.webp")`

12\. Implementação Python de imagens invertidas[](#12-反色图片的-python-实现)
----------------------------------------------------------------------

Blog suporta o modo escuro, e as imagens no artigo também podem ser convertidas para o modo escuro de acordo, para algumas imagens, você pode converter diretamente cores claras para cores escuras invertendo cores (mas não todas, note que cores invertidas não são iguais a cores escuras!). Eu escrevi um programa Python que pode converter imagens para o modo escuro, e você pode pegá-las se precisar. Da mesma forma, o caminho do arquivo também é definido de acordo com minha própria situação real e precisa ser modificado de acordo:

`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31  from PIL import Image, ImageChops import matplotlib.pyplot as plt    def invert_color(fname):     im = Image.open(fname)     if im.mode == "P":         im = im.convert('RGB')     im_inverted = ImageChops.invert(im)     # im.close()     return im, im_inverted  # 这部分是调整至图片文件路径 path_start = "../huanyushi.github.io/assets/img/in-post/" path_end = '2023-03-23/preface.PNG' image_path = path_start + path_end  image_origin, image_inverted = invert_color(image_path)  # 绘图对比，不想绘图可以直接去掉 plt.subplot(121)  plt.title('original')  plt.axis('off') plt.imshow(origin, cmap='gray', vmin=0, vmax=255)   plt.subplot(122)  plt.title('inverse')  plt.imshow(image_output, cmap='gray', vmin=0, vmax=255)  plt.axis('off') plt.show()  # 保存图片 image_output.save(image_start + image_end.replace('.', '-dark.')) # 如：test.PNG 生成的反色图片保存为 test-dark.PNG` 

[![comparação inversa](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/inverse.png)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/inverse.png) [![inverse comparison](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/inverse-dark.png)](https://cdn.jsdelivr.net/gh/huanyushi/huanyushi.github.io@main/assets/img/in-post/2024/2024-03-30/inverse-dark.png) _Comparação da imagem invertida com a imagem original_

13\. Disposições gerais[](#13-其他问题)
-----------------------------------

### 13.1. Falha no Git Push: Não foi possível fazer a rede ao servidor[](#131-git-push-失败-couldnt-connet-to-server)

Enviar arquivos locais para repositórios remotos do github geralmente causa erros, e não há uma maneira eficaz óbvia de consultá-los. Aqui está o que **pode funcionar** (o terceiro é o mais eficaz no momento):`couldn't connet to server`

1.  Desligue a escada (VPN) e tente empurrar novamente;
2.  Execute o código a seguir na linha de comando para cancelar o proxy.
    
    `1 2  git config --global --unset http.proxy  git config --global --unset https.proxy` 
    
3.  Abra o estojo da escada. Clique com o botão direito do mouse na rede no canto inferior direito, abra-a, clique em Proxy e exiba o endereço e o número da porta, como . Enter na linha de comando`网络和 Internet 设置``127.0.0.1:7890`
    
    `1  git config --global http.proxy http://127.0.0.1:7890`
    

Você pode verificar se a configuração foi bem-sucedida. Então você pode empurrar.`git config --global -l`

### 13.2. As visualizações do Jekyll Serve são mais lentas[](#132-jekyll-serve-预览速度较慢)

Há muitas maneiras de fazer isso, como reduzir o número de pastas, compactar o tamanho das imagens, etc. Aqui estão alguns dos métodos que descobri:

1.  Configurar uma compilação incremental para o seu blog (ou seja, reconstruir apenas os arquivos que foram alterados, em vez de reconstruir todo o site a cada vez) pode ser adicionado e o jekyll reconstruirá os arquivos alterados cada vez que você fizer isso. Claro, é mais apropriado usar ou construir um blog, para que o ajuste manual seja mais flexível.`_config.yml``incremental: true``bundle exec jekyll s --incremental``bundle exec jekyll s --I`
2.  Comprimir o tamanho da imagem, que também é uma maneira de acelerar a construção e navegação do blog.

### 13.3. Inserindo arquivos no blog[](#133-在-blog-中插入文件)

Use elementos como:`<iframe>`

`1  <iframe src="file path" width="100%" height='800'></iframe>`

Use este truque para inserir arquivos html, pdf, etc. no post para visualização.

advertir

Esse recurso funciona bem no Google Chrome, mas outros navegadores podem não suportá-lo, e o estouro não pode produzir barras de rolagem em terminais móveis, então use com cuidado!

### 13.4. Executando Python Online no blog[](#134-在-blog-中在线运行-python)

Adicione o seguinte código ao post para executar o Python online (embora pareça um pouco frango, mas ainda está documentado aqui)

`1 2 3 4 5  <iframe   src="https://jupyterlite.github.io/demo/repl/index.html?kernel=python&toolbar=1"   width="100%"   height="500px"> </iframe>`

### 13.5. Recursos que podem ser úteis[](#135-可能有用的资源)

Recursos que podem ser úteis

*   [TinyPNG](https://tinypng.com/): Um site de compressão de imagem on-line gratuito, embora seja dito ser compressão com perdas, quase não tem impacto visual, e a compressão de imagem pode chegar a 70%.
*   [PageSpeed Insights](https://pagespeed.web.dev/): a ferramenta de monitoramento de desempenho de sites do Google que fornece um relatório e um plano de otimização quando você insere um URL e, a propósito, vê onde ele está diminuindo sua velocidade de carregamento.
*   [Coolors](https://coolors.co/), [Color Hunt](https://www.colorhunt.co/): Um site de classificação de cores on-line que pode ser usado para fornecer correspondências de cores recomendadas.

[HTML e CSS](/categories/html-and-css/)

[Referência:](/tags/html/) [CSS](/tags/css/)

Este post está licenciado sob [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) pelo autor.

Compartilhar[](https://twitter.com/intent/tweet?text=Chirpy%20Blog%20Customization%20-%20Huanyu%20Shi&url=https%3A%2F%2Fhuanyushi.github.io%2Fposts%2Fchirpy-blog-customization%2F)[](https://www.facebook.com/sharer/sharer.php?title=Chirpy%20Blog%20Customization%20-%20Huanyu%20Shi&u=https%3A%2F%2Fhuanyushi.github.io%2Fposts%2Fchirpy-blog-customization%2F)[](https://service.weibo.com/share/share.php?title=Chirpy%20Blog%20Customization%20-%20Huanyu%20Shi&url=https%3A%2F%2Fhuanyushi.github.io%2Fposts%2Fchirpy-blog-customization%2F)[](https://connect.qq.com/widget/shareqq/index.html?title=Chirpy%20Blog%20Customization%20-%20Huanyu%20Shi&url=https%3A%2F%2Fhuanyushi.github.io%2Fposts%2Fchirpy-blog-customization%2F)
