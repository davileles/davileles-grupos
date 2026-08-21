# Landing de captação — Tica Promos

Página de entrada dos grupos de WhatsApp. **Este repositório é a fonte da
verdade**; a publicação é manual, por upload na Hostinger.

## Como publicar

1. Baixe o conteúdo deste repositório.
2. Suba tudo para `public_html/` na Hostinger, no domínio da landing.
3. Confira `https://<dominio>/` — o cache do LiteSpeed pode segurar a versão
   antiga por alguns minutos.

Não existe deploy automático aqui. Se você editar direto no painel da
Hostinger, a alteração se perde no próximo upload — edite aqui primeiro.

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
