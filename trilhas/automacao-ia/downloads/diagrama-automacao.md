# Diagramas de Automacao
## TikTok Shop Academy 2025 - Trilha Automacao IA

---

## Fluxo Macro do Sistema

```
┌─────────────────────────────────────────────────────────────────┐
│                    SISTEMA DE AUTOMACAO COMPLETO                 │
└─────────────────────────────────────────────────────────────────┘

    ┌─────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
    │  IDEIA  │ ──► │ ROTEIRO  │ ──► │ VIDEO IA │ ──► │  EDICAO  │
    │         │     │   (IA)   │     │          │     │          │
    └─────────┘     └──────────┘     └──────────┘     └──────────┘
         │               │                │                │
         │               │                │                │
         ▼               ▼                ▼                ▼
    ┌─────────────────────────────────────────────────────────────┐
    │                        n8n / Make                            │
    │                   (ORQUESTRADOR CENTRAL)                     │
    └─────────────────────────────────────────────────────────────┘
                                │
                                ▼
    ┌──────────┐     ┌──────────┐     ┌──────────────────────────┐
    │PUBLICACAO│ ──► │  TIKTOK  │ ──► │ MONITORAMENTO & ANALYTICS │
    │   AUTO   │     │   SHOP   │     │                          │
    └──────────┘     └──────────┘     └──────────────────────────┘
                          │                        │
                          ▼                        ▼
                    ┌──────────┐            ┌──────────┐
                    │  VENDAS  │            │  REPOST  │
                    │COMISSOES │            │ WINNERS  │
                    └──────────┘            └──────────┘
```

---

## Workflow 1: Geracao de Roteiro

```
┌──────────────────────────────────────────────────────────────────┐
│                  WORKFLOW: IDEIA → ROTEIRO                        │
└──────────────────────────────────────────────────────────────────┘

┌─────────────────┐
│ GOOGLE SHEETS   │
│ Nova linha:     │
│ - Produto       │
│ - Beneficio     │
│ - Publico       │
└────────┬────────┘
         │
         ▼ Webhook
┌─────────────────┐
│     n8n/Make    │
│ Recebe dados    │
└────────┬────────┘
         │
         ▼ HTTP Request
┌─────────────────┐
│   OPENAI API    │
│ Model: GPT-4    │
│ Prompt: v3.2    │
│ Temp: 0.7       │
└────────┬────────┘
         │
         ▼ Response
┌─────────────────┐
│    OUTPUTS:     │
│ - 5 roteiros    │
│ - 5 ganchos     │
│ - 5 CTAs        │
└────────┬────────┘
         │
         ▼ Write
┌─────────────────┐
│ GOOGLE SHEETS   │
│ Salva roteiros  │
│ Status: Pronto  │
└─────────────────┘
```

---

## Workflow 2: Geracao de Video (Avatar)

```
┌──────────────────────────────────────────────────────────────────┐
│                  WORKFLOW: ROTEIRO → VIDEO                        │
└──────────────────────────────────────────────────────────────────┘

┌─────────────────┐
│ GOOGLE SHEETS   │
│ Trigger: Novo   │
│ roteiro pronto  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│     n8n/Make    │
│ Le roteiro      │
│ Formata texto   │
└────────┬────────┘
         │
         ▼ API Call
┌─────────────────┐
│    HEYGEN API   │
│ - Avatar ID     │
│ - Voice ID      │
│ - Script text   │
│ - Background    │
└────────┬────────┘
         │
         │ (Processamento: 3-5 min)
         │
         ▼ Webhook Callback
┌─────────────────┐
│     n8n/Make    │
│ Recebe URL do   │
│ video pronto    │
└────────┬────────┘
         │
         ├────────────────────┐
         ▼                    ▼
┌─────────────────┐  ┌─────────────────┐
│ GOOGLE DRIVE    │  │ GOOGLE SHEETS   │
│ Download video  │  │ Atualiza status │
│ Salva em pasta  │  │ Link do video   │
└─────────────────┘  └─────────────────┘
```

---

## Workflow 3: Publicacao Automatica

```
┌──────────────────────────────────────────────────────────────────┐
│                  WORKFLOW: VIDEO → PUBLICACAO                     │
└──────────────────────────────────────────────────────────────────┘

┌─────────────────┐
│  GOOGLE DRIVE   │
│ Pasta: /prontos │
│ Novo arquivo    │
└────────┬────────┘
         │
         ▼ Trigger
┌─────────────────┐
│     n8n/Make    │
│ Detecta video   │
│ Le metadados    │
└────────┬────────┘
         │
         ├─────────────────────────┐
         ▼                         ▼
┌─────────────────┐       ┌─────────────────┐
│ GOOGLE SHEETS   │       │   CHATGPT API   │
│ Busca caption   │       │ Gera hashtags   │
│ e produto       │       │ otimizadas      │
└────────┬────────┘       └────────┬────────┘
         │                         │
         └────────────┬────────────┘
                      │
                      ▼
              ┌─────────────────┐
              │   BOTATO API    │
              │ - Video file    │
              │ - Caption       │
              │ - Hashtags      │
              │ - Schedule time │
              │ - Product link  │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │    TIKTOK       │
              │ Post agendado   │
              │ para horario    │
              │ de pico         │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │   SLACK/TELE    │
              │ Notificacao:    │
              │ "Video agendado │
              │  para 18h"      │
              └─────────────────┘
```

---

## Workflow 4: Monitoramento

```
┌──────────────────────────────────────────────────────────────────┐
│                  WORKFLOW: MONITORAMENTO                          │
└──────────────────────────────────────────────────────────────────┘

┌─────────────────┐
│     CRON        │
│ A cada 6 horas  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│     n8n/Make    │
│ Inicia coleta   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  TIKTOK API     │
│ Busca metricas: │
│ - Views         │
│ - Likes         │
│ - Comments      │
│ - Shares        │
│ - CTR carrinho  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ PROCESSAMENTO   │
│ - Calcula media │
│ - Identifica    │
│   winners       │
│ - Identifica    │
│   losers        │
└────────┬────────┘
         │
         ├─────────────────────────┐
         │                         │
         ▼                         ▼
┌─────────────────┐       ┌─────────────────┐
│ SE WINNER:      │       │ SE LOSER:       │
│ - Alerta Slack  │       │ - Marca "nao    │
│ - Add fila      │       │   repostar"     │
│   repost        │       │ - Log para      │
│ - Destaca no    │       │   analise       │
│   dashboard     │       │                 │
└─────────────────┘       └─────────────────┘
         │
         ▼
┌─────────────────┐
│ GOOGLE SHEETS   │
│ Dashboard       │
│ atualizado      │
└─────────────────┘
```

---

## Workflow 5: Repost Automatico

```
┌──────────────────────────────────────────────────────────────────┐
│                  WORKFLOW: REPOST WINNERS                         │
└──────────────────────────────────────────────────────────────────┘

┌─────────────────┐
│ FILA DE REPOST  │
│ Videos winners  │
│ identificados   │
└────────┬────────┘
         │
         ▼ Daily Cron
┌─────────────────┐
│     n8n/Make    │
│ Seleciona       │
│ proximo winner  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│    VERIFICA:    │
│ - Ja repostado? │
│ - Conta destino │
│   disponivel?   │
│ - >2 semanas do │
│   original?     │
└────────┬────────┘
         │
         ├─── NAO ───► [Pula para proximo]
         │
         ▼ SIM
┌─────────────────┐
│   CHATGPT API   │
│ Gera variacao:  │
│ - Novo gancho   │
│ - Nova caption  │
│ - Novas tags    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   BOTATO API    │
│ Agenda repost   │
│ em conta        │
│ secundaria      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ GOOGLE SHEETS   │
│ Marca como      │
│ "repostado"     │
│ Data/Conta      │
└─────────────────┘
```

---

## Estrutura de Dados (Google Sheets)

### Planilha: Videos

| ID | Produto | Roteiro | Status | URL_Video | Data_Pub | Views | Likes | Comments | CTR | GMV | Winner |
|----|---------|---------|--------|-----------|----------|-------|-------|----------|-----|-----|--------|
| 001 | Serum X | "Voce sabia..." | Publicado | drive.com/... | 2025-01-15 | 15000 | 2300 | 145 | 3.2% | R$450 | SIM |

### Planilha: Contas

| Conta_ID | Username | Status | Posts_Hoje | Ultimo_Post | Shadowban | Notas |
|----------|----------|--------|------------|-------------|-----------|-------|
| C001 | @marca_principal | Ativo | 3 | 2025-01-15 18:00 | NAO | Conta principal |

### Planilha: Fila_Repost

| Video_ID | Conta_Origem | Conta_Destino | Data_Repost | Status |
|----------|--------------|---------------|-------------|--------|
| 001 | C001 | C002 | 2025-01-30 | Agendado |

---

## Alertas e Notificacoes

```
┌────────────────────────────────────────────────────────────────┐
│                    SISTEMA DE ALERTAS                          │
└────────────────────────────────────────────────────────────────┘

ALERTAS VERDES (Sucesso):
├── Video passou 10K views
├── Nova venda realizada
├── Winner identificado
└── Repost agendado com sucesso

ALERTAS AMARELOS (Atencao):
├── Video abaixo da media (24h)
├── Estoque baixo de produto
├── Conta proxima do limite diario
└── API com latencia alta

ALERTAS VERMELHOS (Urgente):
├── Possivel shadowban detectado
├── Erro em API critica
├── Video removido pelo TikTok
└── Conta restrita
```

---

## Legenda

```
Simbolos:
─────────  Fluxo de dados
   │
   ▼       Direcao do fluxo

┌───┐
│   │      Processo/Acao
└───┘

┌───┐
│   │      Servico externo (API)
└───┘

[texto]    Condicional
```

---

*TikTok Shop Academy 2025*
