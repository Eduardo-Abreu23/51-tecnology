# Handoff: 51 Tecnologia — E-commerce (home + carrinho + favoritos + modal de produto)

## Overview
Loja online de tecnologia "51 Tecnologia". Página única com header sticky, hero da JBL Boombox 4 com troca de cor, categorias, destaques, benefícios, banner promocional (AirPods Max), ofertas, catálogo com busca/filtros/ordenação, footer, e painéis de carrinho, favoritos, menu mobile e modal de produto. Idioma: pt-BR. Moeda: BRL.

## About the Design Files
Os arquivos deste pacote são **referências de design feitas em HTML** — protótipos que mostram aparência e comportamento, **não código de produção para copiar**. A tarefa é **recriar este design** num projeto real. Se ainda não existe projeto, sugestão: **React + Vite (ou Next.js) + CSS Modules/Tailwind**, com componentes:
Header, MobileMenu, Hero, CategorySection/CategoryCard, FeaturedProducts, SpotlightCard, ProductCard, ProductGrid, Filters, Benefits, PromotionBanner, Offers, CartDrawer, FavoritesDrawer, ProductModal, Toast, Footer.

Para ver o protótipo: abra `51 Tecnologia.dc.html` num servidor local (ex. `npx serve .`) — ele depende de `support.js`, `ProductCard.dc.html`, `image-slot.js` e `images/`. Toda a lógica (dados, estado, handlers) está na classe `Component` dentro do `<script>` do arquivo principal.

## Fidelity
**High-fidelity.** Cores, tipografia, espaçamentos, raios, interações e breakpoints são finais. Recriar fielmente.

## Dados (fonte única — manter assim)
- `PRECOS` — **único lugar dos preços (todos são MOCK/exemplo)**. `{ preco, de? }`; se `de > preco` o produto vira "OFERTA" e mostra % de desconto automaticamente.
- `PARCELAS = 10` → "ou 10x de R$ X sem juros".
- `CATS` — 7 categorias com cores do card (bg, fg, muted, ghost, botão).
- `PRODUTOS` — 11 produtos: id, name, brand, cat, sub, ghost (texto grande de placeholder), rating, reviews, recent (ordem "mais recentes"), featured, spotlight (TV 85"), stock:'baixo' ("Poucas unidades" em ofertas), tint (fundo da foto), img, blend, colors/imgs (JBL), desc, features.
- `blend: true` = foto com fundo branco (não recortada) exibida com `mix-blend-mode: multiply` sobre o tint e sem drop-shadow. Ideal: substituir por PNG recortado e remover `blend`.

Produtos: JBL Boombox 4 (Marrom/Laranja/Preto), Starlink (sem foto ainda), Apple AirPods Max, Samsung HD TV H500F 32", iMac Roxo Claro, TCL Ar-Condicionado Inverter Série Elite GV, Xiaomi Robot Vacuum S40, Gaabor Air Fryer NEO 4L, Xiaomi Robot Vacuum H50 Pro, Ninja Creami, Samsung Crystal UHD U8600F 85".

## Design Tokens
**Cores**
- Ink `#111111` · Texto secundário `#4a4a4e`, `#6b6b6f`, `#77777b` · Terciário `#9a9a9e`
- Vermelho (CTA/ofertas/badges) `#E1261C` · hover `#C81E15` · vermelho claro (texto sobre preto) `#ff8a82`
- Fundo `#ffffff` · Cinza claro `#f4f4f3` · Bordas `#ececec`, `#e2e2e2` · Footer `#111111`, linhas `#2a2a2e`, texto `#b4b4b8`
- Hero bg: `radial-gradient(110% 90% at 72% 42%, #fbfbfb 0%, #eeeeed 50%, #e3e3e2 100%)`
- Categorias (bg/fg): Áudio `#141414`/#fff · TVs `#EFEFED`/#111 · Computadores `#DCD3F2`/`#1B1530` · Casa Inteligente `#E1261C`/#fff · Eletrodomésticos `#F1E9DE`/`#2A1F14` · Climatização `#DDE9EF`/`#0F2530` · Internet `#26262A`/#fff
- JBL cores (hex / tint): Marrom `#6B4A36`/`#EFE8E2` · Laranja `#E8742A`/`#FBECE0` · Preto `#1D1D1F`/`#EAEAEB`

**Tipografia** — Google Font **Archivo** (eixo variável `wdth 62..125`, `wght 100..900`).
- Display (H1 hero): 900, `font-stretch:112%`, `letter-spacing:-0.045em`, `line-height:.88`, `clamp(46px,7.4vw,108px)`
- H2 seção: 900, stretch 112%, `-0.04em`, lh .95, `clamp(30px,4.4vw,56px)`
- Eyebrow: 12px, 800, `letter-spacing:.2em`, vermelho
- Logo "51": 900, stretch 125%, `-0.06em`, "1" em vermelho; "TECNO/LOGIA" 10.5px 800 `.28em` com borda esquerda 1.5px
- Corpo 14–15px, lh 1.5 · Preço card `clamp(19px,2.2vw,24px)` 800
- Palavras fantasma de fundo (BOOMBOX, MAX, 85”, nomes de categoria): 900, stretch 125%, cor branca ou rgba baixa

**Raios**: cards 22px · banners `clamp(24px,3vw,36px)` · categorias `clamp(22px,2.4vw,30px)` · botões/pílulas 999px · miniaturas 14–16px
**Sombras**: hover card `0 24px 44px -24px rgba(17,17,17,.30)` · dropdown `0 24px 48px -20px rgba(0,0,0,.22)` · CTA vermelho `0 14px 28px -14px rgba(225,38,28,.7)` · foto `drop-shadow(0 18px 16px rgba(0,0,0,.16))`
**Container**: max-width 1320px, padding lateral `clamp(16px,4vw,40px)`. Espaço entre seções `clamp(56px,8vw,112px)`.
**Alvos de toque**: mínimo 44px.

## Screens / Views (ordem da home)
1. **Top bar** preta 12px: "Preços ilustrativos (ambiente de demonstração)" — remover em produção.
2. **Header sticky** (fundo branco 94% + blur 14px): logo · busca pílula 50px (`#f4f4f3`, botão "Buscar" preto) com dropdown de sugestões (até 5, "Ver todos os resultados (n)", "Nenhum produto encontrado") · Minha conta (popover Entrar/Criar conta) · Favoritos (badge preto) · Carrinho (pílula preta com contador vermelho; "bump" scale 1.12 ao adicionar). Nav abaixo: Início, Ofertas (vermelho + ponto), Áudio, TVs, Computadores, Casa Inteligente, Eletrodomésticos, Climatização, Internet — categoria ativa com sublinhado vermelho 2px.
3. **Hero JBL Boombox 4**: grid 2 col (auto-fit min 380px). Esquerda: eyebrow "NOVO NA 51 TECNOLOGIA", H1 "JBL / BOOMBOX 4", subtítulo, seletor de cor (pílulas 44px com bolinha 28px; ativa com borda #111), "Comprar agora" (vermelho 54px) + "Ver detalhes" (outline), preço. Direita: 3 imagens empilhadas com crossfade (opacity .5s + scale .94→1), círculo da cor escolhida a 14% de opacidade atrás, sombra elíptica no chão. Palavra "BOOMBOX" branca gigante no rodapé do banner.
4. **Categorias** "ENCONTRE O QUE VOCÊ PRECISA": grid 4 col (≥1080) com spans [2,1,1,1,1,2,4]; 2 col (≥620) spans [2,1,1,1,1,2,2]; 1 col. Card: contador, nome, descrição, botão "Ver produtos →", marcas, palavra fantasma. Clique → filtra catálogo pela categoria e rola até ele.
5. **Produtos em destaque**: grid 4/3/2 col (≥1180/≥820/<820). Primeiro item = **Spotlight TV 85"** (span 2, fundo #111, badge "TELA GIGANTE", "85”" fantasma). Depois ProductCards de `featured`, quantidade ajustada para completar a última linha.
6. **Benefícios**: faixa com bordas top/bottom, 3 itens com ícone em círculo vermelho outline 52px: COMPRA SEGURA, SUPORTE ONLINE, PRODUTOS COM GARANTIA. (Frete foi removido de propósito.)
7. **Banner promocional** vermelho `#E1261C`: AirPods Max grande saindo pelo topo do banner (margin-top negativo), "MAX" fantasma, eyebrow "TECNOLOGIA QUE IMPRESSIONA", H2 "ENCONTRE SEU PRÓXIMO PRODUTO", botões "Ver produtos" (branco) e "AirPods Max" (outline branco).
8. **Ofertas da 51 Tecnologia**: produtos com `de`, ordenados por maior desconto; botão "Comprar"; "Poucas unidades" (ponto vermelho) se stock baixo.
9. **Todos os produtos**: sidebar de filtros sticky (280px; em <880px vira botão "Filtros" com contador que expande) — Categoria (checkbox), Marca (chips), Faixa de preço (range, "Até R$ X"/"Qualquer valor"), Avaliação (Todas / 4,7+ / 4,8+), "Limpar". Ordenação: Mais relevantes, Menor preço, Maior preço, Mais recentes. Chip "Resultados para 'x' ×". Estado vazio com "Limpar busca e filtros". Grid 3/2/3/2 col.
10. **Footer** preto: logo, descrição, redes (Instagram, Facebook, YouTube, TikTok), colunas SOBRE A 51 TECNOLOGIA / ATENDIMENTO / CATEGORIAS / INSTITUCIONAL, pagamentos (Pix, VISA, Mastercard, elo, AMEX, Boleto), "© 2026 51 Tecnologia. Todos os direitos reservados."

### ProductCard
Topo (aspect 1/0.9, fundo `tint`): badges "OFERTA" + "-X%", botões redondos 40px favoritar (coração vermelho quando ativo) e ver detalhes. Imagem 78%. Base: "MARCA · SUB" 10.5px caps, nome (abre modal), estrelas (preenchimento proporcional) + "4,8 (356)", bolinhas de cor (JBL), preço antigo riscado + %, preço, parcelamento, botão preto 46px "Adicionar ao carrinho" → vira vermelho "Adicionado ✓" por 1.4s. Hover: translateY(-4px) + sombra.

### ProductModal
Overlay 50% preto; painel max 1120px, raio 28px (tela cheia <640px), entra com fade + translateY(28px→0). Esquerda: foto única grande (sem galeria de miniaturas — removida de propósito), badge oferta. Direita: marca·categoria·sub, nome, avaliação, bloco de preço, descrição, seletor de cor (JBL: MARROM/LARANJA/PRETO, troca imagem com fade 160ms), quantidade −/+, favoritar, "Comprar agora" (adiciona + abre carrinho) e "Adicionar ao carrinho", lista CARACTERÍSTICAS com check vermelho, selos "Compra segura · Produto com garantia". Esc fecha.

### Drawers
Carrinho (direita, 440px): itens com miniatura, cor, −/+ (mín. 1), remover, total da linha; Subtotal, Total + parcelamento, "Finalizar compra" (vermelho; simula pedido → tela "Pedido recebido!"), "Continuar comprando". Vazio: "Explorar produtos". Favoritos (direita): lista com adicionar/remover. Menu mobile (esquerda, 360px). Todos: translateX com `.45s cubic-bezier(.2,.8,.2,1)`, overlay 45%, bloqueia scroll do body.

## Interactions & Behavior
- **Efeito 3D**: nas fotos (hero, banner, cards, modal) `mousemove` aplica `perspective(1000px) rotateY(x*20deg) rotateX(-y*16deg) scale(1.04)`; sombra do chão desloca `translateX(-x*36px)`. Transição .3s ease-out; reset no mouseleave. Ignorar em touch.
- **Flutuação**: hero e banner com `@keyframes float` (translateY 0 → -14px, 5–5.6s ease-in-out infinite) e sombra pulsando (scaleX 1→.86). Respeitar `prefers-reduced-motion`.
- **Reveal**: seções abaixo da dobra entram com opacity 0→1 + translateY(28px→0), .8–.9s, via IntersectionObserver.
- **Toast** inferior central preto: "X adicionado ao carrinho", "Salvo nos favoritos" etc., 2.2s.
- **Busca**: sem acento e case-insensitive em nome+marca+sub+categoria; todos os termos devem bater. Enter rola até o catálogo. "Samsung" → as 2 TVs.
- **Persistência**: carrinho e favoritos em localStorage (`51tec-cart`, `51tec-favs`).
- **Breakpoints**: hamburger/sem nav <1000px · busca vai para linha abaixo do header <760px · rótulos dos ícones só ≥1180px · filtros colapsáveis <880px. **Sem scroll horizontal** (`overflow-x: clip` no root).

## State
cart[{key,id,color,qty}], favs[id], query, searchFocus, fCats[], fBrands[], fPrice|null, fRating, sort, filtersOpen, heroColor, cardColor{id:color}, modal{id,color,qty}|null, drawer('menu'|'cart'|'fav'|null), accountOpen, added{id:bool}, toast, checkoutDone.

## Assets (`images/`)
Imagens geradas por IA pelo cliente (substituir por fotos oficiais/licenciadas se possível):
jbl-marrom-v2.png, jbl-laranja-v2.png, jbl-preto-v2.png, airpods-max.png, imac-roxo.png, samsung-h500f-32.png, samsung-u8600f-85.png, gaabor-neo-4l.png (recortadas) · tcl-elite-gv-w.png, xiaomi-s40-w.png, xiaomi-h50-pro-w.png, ninja-creami-w.png (fundo branco → `blend`). **Starlink ainda sem imagem.** Prompts em `Prompts de imagens.md`.

## Pendências
- Preços reais (todos são mock) · foto do Starlink · recorte dos 4 produtos brancos · checkout/pagamento e login reais · links do footer/redes · validar especificações técnicas com fichas oficiais.

## Files
- `51 Tecnologia.dc.html` — página completa (template + classe `Component` com dados e lógica)
- `ProductCard.dc.html` — card de produto
- `support.js`, `image-slot.js` — runtime do protótipo (não necessários na implementação)
- `images/` — fotos dos produtos
- `Prompts de imagens.md` — prompts para gerar as imagens
