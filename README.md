# Landing de captação — Tica Promos

Página de entrada dos grupos de WhatsApp. **Este repositório é a fonte da
verdade** e é publicado pelo GitHub Pages em `grupos.ticapromos.com.br`.

## Como publicar

Commit na `main` publica sozinho pelo GitHub Pages (domínio em `CNAME`). Leva
de um a dois minutos; confira em aba anônima. Não existe mais cópia na
Hostinger — o site de lá foi excluído em set/2026.

## Estrutura

| Arquivo | O que é |
|---|---|
| `index.html` | A landing inteira: HTML, CSS e JS num arquivo só |
| `imgs/tico.png` | Tico âncora, 256px — logo do topo |
| `imgs/tico-og.png` | Tico em 1024px — preview do link no WhatsApp |
| `favicon.ico`, `apple-touch-icon.png` | Ícones |
| `imgs/*.jpg` | Prints do grupo, fotos de oferta e feedbacks |
| `default.php` | Placeholder da Hostinger, não usado |

## Link dos botões

Todos os CTAs passam pelo distribuidor do proxy CDV, nunca por um convite
fixo do WhatsApp. Isso dá três coisas que o link direto não dá: rotação entre
os 14 grupos, censo de membros e atribuição de clique por origem.

O destino é montado no `<script>` do fim do arquivo:

- `BASE` — host do distribuidor. Trocar para `grupo.ticapromos.com.br` quando
  o DNS do domínio novo estiver de pé. O proxy já aceita os dois hosts.
- `?g=<chave>` na URL escolhe o slug (`wpp` → `/groups`, `grupos` → `/wpp`).
  Sem `?g=`, cai no padrão `/geral`.
- `?o=<origem>` marca a origem do clique. Se não vier, usa `utm_source`; se
  também não vier, grava `landing`. É o que separa o tráfego por canal no
  `dados/tsp/grupos-links.json` — antes disso, tudo caía em `direto`.

Exemplo: `https://<dominio>/?g=wpp&o=meta-ads` envia para o slug `groups` e
contabiliza a origem `meta-ads`.

## Marca

Paleta do Tico, sem quarta cor. As variáveis `--orange` e `--dark-orange` são
nomes legados mantidos para não reescrever 40 regras de CSS: hoje carregam
coral `#FA5150` e o vermelho da moldura dos avatares `#D93636`. O fundo é
navy `#12141C`, não preto puro.

Voz: segunda pessoa do singular, frases curtas, sem urgência falsa. A bíblia
do personagem está em `davileles/dados`.

## Landings de nicho

Cada nicho tem a própria landing numa subpasta, reaproveitando `favicon.ico`,
`apple-touch-icon.png` e `imgs/whatsapp.png` da raiz via `../`.

| Pasta | Slug do distribuidor | Origem padrão |
|---|---|---|
| `bebidas/` | `ir.ticapromos.com.br/bebidas` | `landing-bebidas` |
| `babykids/` | `ir.ticapromos.com.br/babykids` | `landing-babykids` |
| `ferramentas/` | `ir.ticapromos.com.br/ferramentas` | `landing-ferramentas` |

O `?o=` / `utm_source` funciona igual à landing geral. A landing de bebidas pede
confirmação de 18+ no primeiro clique do CTA (guardada na sessão) e empurra o
evento `entrar_grupo` com `nicho` e `local` no `dataLayer`.
Os achados da página (`ACHADOS` no script) são reais, tirados do histórico de
envios da categoria bebidas — atualizar à mão quando envelhecerem.

A landing Baby e Kids não pede confirmação de idade. Os preços típicos dela são a
mediana do preço de vitrine em `dados/tsp/precos_hist_AAAA-MM.json`; a faixa de
data comemorativa (Dia das Crianças até 12/10, depois Natal) é calculada no dia.

A landing de Ferramentas mostra só achados de marca e explica as regras de
curadoria do grupo (as mesmas de `curadoriaNicho` em `dados/tsp/categorias.json`:
marca reconhecida entra, genérico só 25% abaixo da mediana, voltagem inflada
fica fora) — se as regras mudarem lá, atualizar o texto da seção "Como o Tico
escolhe o que entra". Selo de data: Dia dos Pais → Black Friday → Natal, a até
75 dias da data, calculado no dia.

## Agregador de links (`links/`)

Página única com um botão por grupo, para stories e link da bio. Cada botão vai
para o distribuidor (`ir.ticapromos.com.br/<slug>`), nunca para convite fixo.

| Botão | Slug |
|---|---|
| Ofertas gerais | `geral` |
| Só cupons | `cupons` |
| Bebidas (pede 18+, mesma chave `tsp-18` da landing) | `bebidas` |
| Baby e Kids | `babykids` |
| Ferramentas | `ferramentas` |

- `?o=<origem>` marca a origem (padrão `links`; aceita `utm_source`).
- `?d=<slug>` sobe esse grupo para o topo com selo "Em destaque" (padrão `geral`).

Exemplos: `/links/?o=bio`, `/links/?d=bebidas&o=story-bebidas`.
Para adicionar um grupo, incluir o item em `GRUPOS` no script da página (o slug
precisa existir em `dados/tsp/grupos-links.json`).
