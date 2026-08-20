# davileles-grupos

Espelho da landing de captação de grupos (`grupos.tudosobrepromos.com`) no
domínio `grupos.davileles.com`. Estático, servido pelo GitHub Pages.

## Arquivos

| Caminho | O que é |
|---|---|
| `index.html` | a página inteira (HTML, CSS e JS inline) |
| `imgs/` | 17 imagens (logo, prints, depoimentos) |
| `CNAME` | `grupos.davileles.com` |

## Origem

A página original mora na **Hostinger**, fora do GitHub. Esta cópia foi tirada
do ar em produção e continua intocada lá. As duas são independentes: mudança
numa não reflete na outra.

## Dependências externas

- `https://grupo.tudosobrepromos.com/geral` — distribuidor de grupos no Railway
  (`painel-cdv/index.js`, rota `/g/:slug`). Responde 302 para o convite do
  WhatsApp. **Mesmo destino da página original.**
- `GTM-WSXGHM5P` — mesmo container de Tag Manager da original.
