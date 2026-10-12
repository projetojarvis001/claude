# HB — Reavaliação das rotinas (12/10/2026)

Origem: sessão de nuvem "ERP · diagnóstico: Claude não conecta no Chrome/simulador".
Decisões do dono (Wagner) em 12/10/2026. Itens marcados "→ inventário" devem ser
copiados para o STATUS/inventário do projeto indicado.

## Placar

| # | Rotina | Onde vive | Decisão do dono | Feito daqui? |
|---|--------|-----------|-----------------|--------------|
| 1 | VISÃO 360 — lembrete diário conectores | nuvem (trig_01BmWwC4X1GSHeFtcU8MWX9H) | fazer funcionar de verdade; se continuar estranho, reduzir ou cancelar | NÃO (criada via API; só o dono edita). Prompt novo abaixo. |
| 2 | Vaultwarden — checar releases (semanal) | nuvem (trig_01A93QeYmAKo6TVrW8K5UTME) | manter; problema dos conectores → inventário VISÃO 360 | manter = nada a fazer. Conectores: só pela tela. |
| 3 | Vigia de uso semanal do Claude | nuvem (trig_01StwGnZSPN4RhJezbMtStGY) | reavaliar e fazer funcionar | SIM: prompt reescrito (sem promoção vencida, regra por faixa do ciclo) e rotina reativada. Seg/qua 9h SP, Opus. |
| 4 | Checagem diária WhatsApp/Meta | local (app no Mac) | pausar; conectores → inventário VISÃO 360 | NÃO (local). Pausar no app. |
| 5 | Agendar sessão do contador (F4…) | local (app no Mac) | manter; conectores → inventário ERP | nada a fazer além do registro. |
| 6 | Retrospectiva semanal do ritmo | local (kit-ritmo-semanal) | reavaliar e fazer funcionar | NÃO (local). Ver seção "Retrospectiva". |
| 7 | Lembrete: cancelar renovação do O… | local (app no Mac) | manter até disparar | nada a fazer. |

## → Inventário VISÃO 360 (copiar para /opt/visao360/ESTADO.md ou equivalente)

- [ ] **Rotinas na nuvem carregam 11 conectores sem uso.** As rotinas "VISÃO 360 — lembrete diário conectores" e "Vaultwarden — checar releases" têm anexados Gmail, Google Drive, Microsoft 365, Booking.com, Mercado Livre (2), Windsor.ai, Lucid, Lovable, Claude Code Remote e VIS_O_360, embora o prompt use no máximo o Gmail (VISÃO 360) ou nenhum (Vaultwarden). Risco: exposição desnecessária de contas em execução automática. Ação: editar cada rotina em https://claude.ai/code/routines/<id> e deixar só o conector necessário (VISÃO 360: Gmail; Vaultwarden: nenhum). Só o dono consegue (criadas via API).
- [ ] **Rotina "Checagem diária WhatsApp/Meta" pausada em 12/10/2026** por decisão do dono. Motivo: checagem diária de aprovação que depende de terceiros só repete texto. Reavaliar quando houver gatilho real (resposta da Meta) ou transformar em checagem por e-mail, como feito no monitor dos conectores. Conferir também quais conectores ela carrega.
- [ ] **Monitor dos conectores (Amazon/Shopee/TikTok)**: o dono vai trocar o prompt pelo texto da seção abaixo. Primeira semana = teste. Se a saída continuar vazia ou estranha, reduzir para seg/qua/sex ou cancelar. Lembrar: o caso Amazon está em vendas@canaldistribuidora.com.br; se o Gmail conectado for outro, o monitor vai avisar.

## → Inventário ERP (copiar para enterprise-os/STATUS.md, bloco de pendências)

- [ ] **Rotina "Agendar sessão do contador (F4…)" mantida** (12/10/2026). É local (app no Mac). Pendência: conferir no app quais conectores ela carrega e deixar só o necessário; conferir se é recorrente ou única (se for reunião específica, deveria ser única).
- [ ] **Nenhuma rotina cobre o ERP hoje.** Candidatas, só se o dono quiser: (a) checagem semanal de releases/segurança do Odoo 19 (mesmo modelo da rotina Vaultwarden, barata, só web); (b) lembrete do deploy pendente do lote b121 enquanto não for rodado.

## Prompt novo para a rotina 1 (colar em https://claude.ai/code/routines/trig_01BmWwC4X1GSHeFtcU8MWX9H)

Nome sugerido: `VISÃO 360 — monitor diário conectores (checa Gmail)`. Agenda: manter seg–sex 9h SP na primeira semana. Modelo: Sonnet. Conectores: só Gmail.

```
Você é o MONITOR dos conectores de marketplace do projeto VISÃO 360 (dono: Wagner). Você roda na nuvem isolada: NÃO tem acesso ao servidor Friday nem aos consoles dos marketplaces. Ferramenta permitida: SOMENTE o conector Gmail, em modo leitura (buscar e ler threads). Nunca envie, responda, encaminhe, rotule ou apague e-mail. Não use nenhum outro conector.

PENDÊNCIAS (baseline 15/09/2026 — aguardam terceiros):
1. AMAZON — case 22059069071 (erro MD9100). Console: solutionproviderportal.amazon.com/cu/case-lobby (conta vendas@canaldistribuidora.com.br, NÃO wagner@wps.digital). Fica OK quando a Amazon responder habilitando/registrando o OAuth Redirect URI.
2. SHOPEE — app 242269, Go-Live em revisão. Console: open.shopee.com/console/app/242269. Fica OK quando App Status = Live e saírem partner_id/key de PRODUÇÃO.
3. TIKTOK — ticket 2026091501120200001. Console: partner.tiktokshop.com/ticket/center. Fica OK quando atribuírem o Account Manager.

PASSOS:
1. No Gmail, busque mensagens dos últimos 3 dias relacionadas a cada pendência. Buscas sugeridas (ajuste se necessário):
   - Amazon: newer_than:3d (22059069071 OR MD9100 OR "Solution Provider" OR "Selling Partner" OR from:amazon.com OR from:amazon.com.br)
   - Shopee: newer_than:3d (242269 OR "Open Platform" OR shopee)
   - TikTok: newer_than:3d (2026091501120200001 OR "TikTok Shop" OR tiktok)
2. Para cada pendência classifique: NOVIDADE (há e-mail novo e relevante: resuma em 1 linha com data, remetente e o que diz) ou SEM NOVIDADE. Ignore marketing/newsletter.
3. Saída em português, no máximo 8 linhas. Título: "📡 Conectores VISÃO 360 — <data de hoje>". Depois uma linha por pendência: "1. AMAZON — <NOVIDADE: resumo | SEM NOVIDADE> — <link do console>". Se as 3 estiverem SEM NOVIDADE, escreva só o título e a linha "Sem novidade nos 3 (Amazon, Shopee, TikTok)." e encerre.
4. Se a conta Gmail conectada claramente não for a que recebe esses e-mails (por exemplo, nenhuma mensagem de nenhum dos três em 30 dias), acrescente UMA linha: "⚠️ O Gmail conectado parece não receber os e-mails desses chamados; conferir manualmente nos consoles."
5. Última linha fixa: "⏹️ Quando os 3 estiverem OK, peça para desativar este monitor."

REGRAS: não invente status; não repita o texto das pendências além do necessário; não crie arquivos nem artifacts.
```

## Retrospectiva semanal do ritmo (rotina 6, local)

Não dá para ler daqui. Critérios para "funcionar de verdade", a conferir na sessão local
(kit-ritmo-semanal): (1) ela lê os mesmos números que o regulador usa (placar diário/semanal),
não estimativa; (2) sai em no máximo 10 linhas: consumo da semana × meta, 3 maiores
consumidores (sessão/projeto), 1 ajuste sugerido para a semana seguinte; (3) roda 1x por
semana, de preferência sexta após o reset das 14h SP ou segunda cedo; (4) não bloqueia nada,
só informa. Se já faz isso, está pronta. Se não, pedir na sessão local: "mostre o prompt da
Retrospectiva semanal do ritmo e proponha o ajuste para atender os 4 critérios do HB-rotinas".

## Regulador de ritmo (achado do dia, fora da lista de rotinas)

O "não consigo conectar no Chrome" vinha do hook do kit-ritmo-semanal bloqueando
mcp__claude-in-chrome__* em status 🔴 (460 de meta 263). Decisão pendente do dono: fazer o
hook só avisar (exit 0) e nunca bloquear Chrome nem xcrun/xcodebuild. Diff a ser proposto
na sessão local antes de aplicar.
