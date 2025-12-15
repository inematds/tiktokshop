# Template de Planilha de Controle
## TikTok Shop Academy 2025 - Trilha Automacao IA

---

## Estrutura Recomendada (Google Sheets)

Crie um Google Sheets com as seguintes abas:

---

## Aba 1: Dashboard

### Metricas Gerais (Atualizar Automaticamente)

| Metrica | Valor | Meta | Status |
|---------|-------|------|--------|
| Videos Publicados (Mes) | =COUNTIF(...) | 90 | =IF() |
| Views Totais | =SUM(...) | 500K | =IF() |
| GMV Total | =SUM(...) | R$30K | =IF() |
| Taxa de Conversao Media | =AVERAGE(...) | 3% | =IF() |
| Videos Winners | =COUNTIF(...) | 15 | =IF() |
| Contas Ativas | =COUNTA(...) | 5 | =IF() |

### Grafico Semanal
- Views por dia
- Vendas por dia
- Posts por dia

---

## Aba 2: Videos

### Colunas

| Coluna | Tipo | Descricao |
|--------|------|-----------|
| ID | Numero | Identificador unico |
| Data_Criacao | Data | Quando foi criado |
| Produto | Texto | Nome do produto |
| Tipo_Video | Dropdown | Avatar/Faceless/Manual |
| Formato | Dropdown | Problema-Solucao/Tutorial/Review/etc |
| Roteiro | Texto Longo | Texto do roteiro |
| Gancho | Texto | Primeiras palavras |
| CTA | Texto | Chamada para acao |
| URL_Video | URL | Link do arquivo |
| Status | Dropdown | Pendente/Pronto/Publicado/Arquivado |
| Data_Publicacao | Data | Quando foi publicado |
| Horario | Hora | Horario da publicacao |
| Conta | Dropdown | @conta_usada |
| Views_24h | Numero | Views nas primeiras 24h |
| Views_Total | Numero | Views totais |
| Likes | Numero | Curtidas |
| Comments | Numero | Comentarios |
| Shares | Numero | Compartilhamentos |
| Saves | Numero | Salvamentos |
| CTR_Carrinho | Porcentagem | Cliques/Views |
| Vendas | Numero | Quantidade vendida |
| GMV | Moeda | Receita gerada |
| Winner | Checkbox | E um winner? |
| Repostado | Checkbox | Ja foi repostado? |
| Notas | Texto | Observacoes |

### Formulas Uteis

```
// Engagement Rate
=((Likes+Comments+Shares)/Views)*100

// Winner (auto)
=IF(AND(Views>MEDIA_VIEWS*2, CTR>3%), TRUE, FALSE)

// GMV por 1K Views
=(GMV/Views)*1000

// Status baseado em Views
=IF(Views>10000, "Viral", IF(Views>5000, "Bom", IF(Views>1000, "Normal", "Baixo")))
```

---

## Aba 3: Contas

### Colunas

| Coluna | Tipo | Descricao |
|--------|------|-----------|
| Conta_ID | Texto | Identificador interno |
| Username | Texto | @nomedaconta |
| Nicho | Dropdown | Beleza/Tech/Casa/etc |
| Tipo | Dropdown | Principal/Secundaria/Teste |
| Seguidores | Numero | Quantidade atual |
| Status | Dropdown | Ativo/Warmup/Pausado/Banido |
| Posts_Hoje | Numero | Quantos posts hoje |
| Limite_Diario | Numero | Max posts permitidos |
| Ultimo_Post | DateTime | Quando foi o ultimo |
| Proximo_Slot | DateTime | Proximo horario disponivel |
| Saude | Dropdown | Otima/Boa/Atencao/Critica |
| Shadowban | Checkbox | Suspeita de shadowban |
| Data_Criacao | Data | Quando conta foi criada |
| Dispositivo | Texto | Qual device usa |
| IP | Texto | IP/Proxy usado |
| Email | Texto | Email de cadastro |
| Notas | Texto | Observacoes |

### Regras de Saude

```
// Saude da Conta
=IF(Shadowban=TRUE, "Critica",
  IF(AND(Posts_Hoje>=Limite, Engajamento<1%), "Atencao",
    IF(Engajamento>5%, "Otima", "Boa")))
```

---

## Aba 4: Produtos

### Colunas

| Coluna | Tipo | Descricao |
|--------|------|-----------|
| Produto_ID | Texto | SKU ou codigo |
| Nome | Texto | Nome do produto |
| Categoria | Dropdown | Categoria |
| Preco | Moeda | Preco de venda |
| Custo | Moeda | Custo do produto |
| Margem | Porcentagem | Margem de lucro |
| Comissao_Afiliado | Porcentagem | % para afiliados |
| Link_TikTok | URL | Link do TikTok Shop |
| Estoque | Numero | Unidades disponiveis |
| Status | Dropdown | Ativo/Pausado/Esgotado |
| Videos_Criados | Numero | Quantos videos tem |
| Total_Vendas | Numero | Unidades vendidas |
| GMV_Total | Moeda | Receita total |
| Melhor_Video | URL | Link do video que mais vendeu |
| Notas | Texto | Observacoes |

---

## Aba 5: Fila de Producao

### Colunas

| Coluna | Tipo | Descricao |
|--------|------|-----------|
| ID_Fila | Numero | Ordem na fila |
| Prioridade | Dropdown | Alta/Media/Baixa |
| Produto | Dropdown | (vinculado a aba Produtos) |
| Tipo_Video | Dropdown | Avatar/Faceless/Manual |
| Formato | Dropdown | Problema-Solucao/Tutorial/etc |
| Roteiro_Base | Texto | Ideia ou roteiro |
| Status | Dropdown | Fila/Em Producao/Pronto/Publicado |
| Responsavel | Texto | Quem esta fazendo |
| Prazo | Data | Data limite |
| Conta_Destino | Dropdown | (vinculado a aba Contas) |
| Horario_Agendado | DateTime | Quando publicar |
| Notas | Texto | Observacoes |

---

## Aba 6: Calendario Editorial

### Visao de Calendario

| Hora | Segunda | Terca | Quarta | Quinta | Sexta | Sabado | Domingo |
|------|---------|-------|--------|--------|-------|--------|---------|
| 08:00 | @conta1: Video X | - | @conta2: Video Y | - | ... | ... | ... |
| 12:00 | - | @conta1: Video Z | - | ... | ... | ... | ... |
| 18:00 | @conta1: Video A | @conta2: Video B | @conta1: Video C | ... | ... | ... | ... |
| 21:00 | @conta2: Video D | - | @conta1: Video E | ... | ... | ... | ... |

---

## Aba 7: Fila de Repost

### Colunas

| Coluna | Tipo | Descricao |
|--------|------|-----------|
| Video_ID | Texto | (vinculado a aba Videos) |
| Views_Original | Numero | Views do original |
| Conta_Original | Texto | Onde foi publicado |
| Data_Original | Data | Quando foi publicado |
| Conta_Destino | Dropdown | Onde repostar |
| Data_Repost | Data | Quando repostar |
| Variacao | Texto | O que mudar (gancho/caption) |
| Status | Dropdown | Fila/Agendado/Publicado |
| Views_Repost | Numero | Views do repost |
| Sucesso | Checkbox | Repost funcionou? |

---

## Aba 8: Alertas

### Log de Alertas

| Data/Hora | Tipo | Conta | Descricao | Acao Tomada | Resolvido |
|-----------|------|-------|-----------|-------------|-----------|
| 2025-01-15 14:30 | Shadowban | @conta2 | Views caíram 90% | Pausado 48h | Sim |
| 2025-01-14 09:00 | Winner | @conta1 | Video X passou 50K | Adicionado repost | - |

### Tipos de Alerta
- Winner (verde)
- Venda (verde)
- Atencao (amarelo)
- Shadowban (vermelho)
- Erro (vermelho)

---

## Automacao com n8n/Make

### Conexoes Necessarias

1. **Google Sheets** ↔ **n8n/Make**
   - Ler dados de Videos
   - Escrever metricas automaticamente
   - Atualizar status

2. **Trigger de Nova Linha**
   - Quando nova linha em "Fila de Producao" → Iniciar workflow

3. **Cron para Metricas**
   - A cada 6h → Buscar metricas do TikTok → Atualizar planilha

4. **Alertas Automaticos**
   - Quando Views < 50% da media → Adicionar alerta
   - Quando Views > 200% da media → Marcar como Winner

---

## Dicas de Uso

### Organizacao
- Use cores para status (Verde=Publicado, Amarelo=Em producao, Vermelho=Problema)
- Congele as primeiras linhas/colunas
- Use filtros para visualizacoes especificas
- Crie views separadas para cada tipo de analise

### Manutencao
- Atualize diariamente (ou automatize)
- Arquive videos com mais de 30 dias
- Faca backup semanal
- Revise metricas toda segunda-feira

### Expansao
- Adicione abas conforme necessidade
- Crie dashboards no Looker Studio conectado
- Integre com outras ferramentas via API

---

*TikTok Shop Academy 2025*
