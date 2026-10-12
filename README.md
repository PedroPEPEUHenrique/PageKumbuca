# Kumbuca Natas de Belém, landing page

Página de vendas estática. Abra o `index.html` no navegador para ver. Não precisa
instalar nada, não precisa de servidor, não tem dependência de build.

```
knb/
├── index.html                      página inteira
├── styles.css                      todo o estilo
└── assets/
    ├── logo-kumbuca.png            logo (usada no topo, no hero e no rodapé)
    ├── referencia-wireframe.png    wireframe que serviu de base (não vai pro ar)
    └── fotos/                      coloque as fotos do produto aqui
```

---

## O que precisa ser trocado antes de publicar

Use **substituir todas** no editor (Ctrl+H no VS Code). Cada marcador aparece em
vários lugares do `index.html`:

| Procurar por | Trocar por | Ocorrências |
|---|---|---|
| `5562900000000` | seu WhatsApp com DDI + DDD, só números | 16 |
| `https://www.ifood.com.br/delivery/aparecida-de-goiania-go` | link direto da sua loja no iFood | 5 |
| `https://instagram.com/kumbucanatasdebelem` | seu perfil no Instagram | 1 |
| `(62) 90000-0000` | telefone exibido no rodapé | 1 |

### Preços

A página não mostra preço nenhum. A seção "Três formatos", que trazia os três
cartões com valor em reais, foi retirada enquanto a tabela de preços não estiver
fechada. O estilo dos cartões também já saiu do `styles.css`, então a volta da
seção significa reescrever o bloco inteiro.

Os formatos continuam acessíveis pela coluna "Formatos" do rodapé, onde cada item
abre o WhatsApp com a mensagem do produto correspondente já escrita.

---

## Fotos

A página espera quatro fotos. Enquanto elas não existirem, aparece uma moldura
reservada no lugar e nada quebra. **Basta salvar o arquivo com o nome exato abaixo
dentro de `assets/fotos/` que a foto entra sozinha**, sem mexer no código.

| Arquivo | Onde aparece | Sugestão de foto |
|---|---|---|
| `fornada.jpg` | seção "O que faz ser de Belém" | bandeja saindo do forno, vapor visível, luz natural |
| `embalagem.jpg` | seção "Entrega sem perder o ponto" | kit fechado na caixa kraft e no pote PET |
| `historia.jpg` | seção "A história" | mão trabalhando a massa, ou o preparo na cozinha |
| `empresas.jpg` | seção "Para empresas" | caixa de 12 montada para coffee break |

Formato recomendado: horizontal (4:3), no mínimo 1200 px de largura, comprimida
para menos de 300 KB. Use `.jpg` mesmo. Se preferir `.webp`, troque a extensão
no `src` da tag `<img>` correspondente.

---

## Como colocar no ar

Qualquer hospedagem de site estático serve, e as gratuitas dão conta:

- **Netlify Drop**: arraste a pasta inteira em app.netlify.com/drop. Leva um minuto.
- **Cloudflare Pages** ou **Vercel**: também aceitam upload direto da pasta.
- **GitHub Pages**: se preferir versionar o projeto.

Depois, aponte um domínio próprio (`kumbucanatasdebelem.com.br`) e atualize a linha
`<link rel="canonical">` no `index.html` com o endereço final.

---

## Decisões de design

- **Paleta tirada da logo**: azul-marinho `#132450`, creme `#F6F0DA`, dourado `#C19A2E`.
- **Dois tokens de raio** no `styles.css`, de propósito. Botões usam `--radius-btn`
  (20px) e são o único elemento arredondado da página; cartões, molduras e faixas
  usam `--radius` (2px), ou seja, praticamente retos. Esse contraste é o que faz o
  botão saltar. Nada de neon, sombra colorida ou gradiente vibrante.
- **Fonte**: Host Grotesk em toda a página, carregada do Google Fonts. O corpo do
  texto usa o peso Regular 400; títulos, preços e perguntas usam 600, só para dar
  hierarquia. Se quiser tudo em 400, é uma linha no `styles.css`.
- **Sem ornamento**: as faixas azuis são cor chapada, sem textura nem padrão. A
  página não tem nenhum elemento decorativo; o que separa as seções é a troca
  entre os três fundos (creme, papel e azul) e os filetes dourados.
- **Animação mínima**: só o cabeçalho ganhando fundo ao rolar e o menu do celular
  abrindo. Nada entra deslizando.
- **Hierarquia dos botões**: WhatsApp sempre em dourado sólido, iFood sempre como
  link discreto ao lado, exatamente a lógica do Entregável 1, de empurrar o pedido
  para o canal de margem cheia sem esconder o aplicativo.
- **Barra fixa no rodapé do celular** com o botão do WhatsApp, porque é lá que a
  maior parte do tráfego de Instagram vai cair.

## Escrita

A página não usa travessão em lugar nenhum. Onde havia aposto entre travessões,
o texto foi reescrito em frase curta ou com vírgula. Vale manter o padrão ao
editar a copy.

## Estrutura do código

Não há comentário nenhum no HTML, no CSS nem no JavaScript. A orientação do que
mexer está toda aqui neste arquivo.

O HTML usa a tag que descreve o conteúdo em vez de `div` genérica. O que cada uma
marca:

| Tag | Onde | Por quê |
|---|---|---|
| `header` | topo do site e cabeçalho das seções | abertura de um bloco |
| `nav` | menu do desktop e menu do celular | conjunto de links de navegação |
| `article` | os dois blocos da seção "O produto" | unidades de conteúdo independentes |
| `section` | cada faixa da página e cada coluna do rodapé | agrupamento com título próprio |
| `ol` / `li` | os passos de "Como pedir" | é uma sequência, e a ordem importa |
| `figure` / `figcaption` | todas as fotos e o selo do hero | imagem com legenda |
| `aside` | barra fixa de pedido do celular | conteúdo complementar, fora do fluxo |
| `small` | linha de copyright | letra miúda legal |
| `blockquote` / `cite` | a citação na seção da história | fala atribuída a uma pessoa |

Os `div` que sobraram são só de layout: `wrap`, as colunas de grid e os
agrupamentos de botão. É exatamente para isso que `div` existe.

A numeração dos passos (01, 02, 03) não está escrita no HTML. Vem de um contador
CSS em `.step::before`, então acrescentar ou remover um passo renumera sozinho.

## Acessibilidade e SEO

- Estrutura semântica, um `<h1>` só, hierarquia de títulos sem pulo.
- Contraste conferido nas combinações creme/marinho e marinho/dourado.
- Respeita `prefers-reduced-motion`.
- `JSON-LD` do tipo `Bakery` com cidade e telefone, para a busca por
  "pastel de nata Aparecida de Goiânia", com a cidade correta de operação.
- Open Graph preenchido, para o link renderizar com imagem no WhatsApp e no Instagram.
