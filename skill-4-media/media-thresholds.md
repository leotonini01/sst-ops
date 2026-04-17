# Media Thresholds — [MARCA]
## Template com valores SST preenchidos como referência

**Última atualização:** [DATA]
**Mantido por:** Leonardo + Vanessa
**Cadência de revisão:** mensal (via `/act-monthly-media-review`)

---

## Targets por canal/função (Meta Ads)

### Prospecting (Scale campaigns)

| SKU | ROAS target | CPA teto | CPA-ATC (Scale observado) | Budget pace mensal |
|-----|-------------|----------|---------------------------|--------------------|
| Sérum Preenchedor | 1,5x | R$165 | R$30-40 | R$[X]/mês |
| Pele de Porcelana | 1,6x | R$140 | R$25-35 | R$[X]/mês |
| [novo produto] | [a definir] | [a definir] | [a definir] | [a definir] |

**Notas:**
- ROAS target 1,5x/1,6x calibrado com L90D L180D reais. Recalibrar mensalmente se desvio >15%.
- CPA teto é hard limit — ad que passa desse valor por 14d vai pra kill candidate.
- CPA-ATC aqui é o **observado na Scale** (diferente do target do Testing).

### Testing campaigns (otimização por ATC)

| Categoria | CPA-ATC target | Kill threshold (3×) | Budget/ad (30 ATCs) | Graduation Criteria |
|-----------|----------------|---------------------|---------------------|---------------------|
| **Séruns** (Preenchedor etc.) | **R$5** | R$15 | R$150 | CPA-ATC ≤ R$5 + 30+ ATCs + 7+ dias |
| **Tratamentos** (PP etc.) | **R$10** | R$30 | R$300 | CPA-ATC ≤ R$10 + 30+ ATCs + 7+ dias |

**Faixa de "promissor" (acima target, abaixo de kill threshold):**
- Séruns: R$5-10
- Tratamentos: R$10-20

**Budget diário de campanha Testing (5 ads simultâneos):**
- Séruns: R$50-75/dia (ciclo 10 dias)
- Tratamentos: R$70-110/dia (ciclo 14 dias)

### Remarketing tiers (arquitetura SST 5-tier)

| Tier | Audiência | Janela | Budget % | ROAS esperado | Frequência saudável | Frequência warning |
|------|-----------|--------|----------|----------------|---------------------|---------------------|
| HOT (ATC) | Add to Cart não-compradores | 0-30d | 30% | 5x+ | 3-5 | 6+ |
| WARM (Visitantes) | Visitantes não-compradores | 0-30d | 25% | 3-4x | 3-5 | 6+ |
| COOL (Visitantes antigos) | Visitantes não-compradores | 30-90d | 15% | 2-3x | 3-5 | 6+ |
| GOLD (Recompra) | Compradores | 60-180d | 20% | 4x+ | 2-4 | 5+ |
| BRIDGE (Engajados) | Engajados IG/FB não-visitantes | 14-30d | 10% | 2x+ | 2-4 | 5+ |

---

## Graduation Criteria globais (ad Testing → Scale)

1. **CPA-ATC ≤ target do produto** em janela 7d consecutivos
2. **30+ ATCs acumulados** desde launch (volume alvo calibrado — ver seção Budget abaixo)
3. **P18 respeitado** — mínimo 7 dias no Testing sem edição
4. **Hipótese declarada no DSB confirmada** (hand-off SKILL 3)

Se **todos** atingidos: graduação aprovada.
Se falta qualquer um: status "Promissor" ou "Learning", aguardar.

---

## Kill Criteria globais

### Em Testing (ad-level)
- **3× CPA-ATC target sem graduação** (Séruns R$15 spend com CPA-ATC >R$5; Tratamentos R$30 com CPA-ATC >R$10)
- **CPA-ATC ≥ 2× target por 3+ dias** com 10+ ATCs
- **Thumb-stop <25% após 72h + 1000+ imps** (P18.1)

### Em Scale (ad-level ou campaign-level)
- **ROAS <0,8× target por 14+ dias** com 10+ conversões (ad-level)
- **Spend >2× target CPA sem nenhuma conversão** em 7d+ (ad-level)
- **Breakdown effect check negativo** antes de aplicar — regra 5 Bloco B

---

## Scaling Pace

### Aumento de budget em campanha validada
- **+20-30% a cada 2-3 dias** (P18 preserve learning)
- **Nunca >50%** de aumento (reseta learning)
- **50 conv/semana mínimo** por campanha em Scale pra algoritmo otimizar

### Duplicação pra scaling (pratica SST)
- Aceita quando budget increment (+30%) não está sendo gasto
- Monitoramento semanal obrigatório (Regra 4 reformulada Bloco B)
- Consolidar se razão ROAS <0,70 × referência

---

## Budget allocation mensal (SST hoje — exemplo)

| Área | Budget mensal | % do total |
|------|---------------|------------|
| Meta Prospecting | R$[X] | [60-70%] |
| Meta Remarketing | R$[X] | [15-20%] |
| Meta Testing | R$[X] | [10-15%] |
| **Total Meta** | **R$[X]** | **100%** |

**Regra de realocação:**
- Se ROAS Prospecting <1,2× target por 5+ dias consecutivos → realocar 15% de Prosp pra RMKT (regra Petvi importada)
- Se tier RMKT está subinvestido vs architecture → rebalancear tiers

---

## Recalibração via Monthly Media Review

Thresholds revisados mensalmente. Critério de ajuste:

**Ajustar pra baixo (threshold mais apertado):**
- Se True Winners confirmados tinham CPA-ATC consistentemente <R$3 (não R$5), apertar target pra R$4
- Se ROAS Scale real L90D foi 1,35x consistente, baixar target de 1,5x pra 1,35x (reconhecer realidade)

**Ajustar pra cima (threshold mais relaxado):**
- Se muitos True Winners ficaram no limite do target mas confirmaram, relaxar marginalmente
- Se conta amadurece e audience se expande, targets podem ser mais generosos

**Registrar mudanças em changelog:**

```
## Changelog

### YYYY-MM-DD
- CPA-ATC target Séruns: R$6 → R$5 (ajuste pra baixo)
  - Motivo: True Winners últimos 90d tiveram CPA-ATC médio R$3,80
  - Impacto: pipeline mais seletivo, esperado menos graduações mas maior taxa True Winner
```

---

## Notas operacionais

- **CPA-ATC é sempre manual** — spend dividido por actions_add_to_cart do Windsor
- **ROAS é sempre manual** — action_values_omni_purchase dividido por spend (P01)
- **Campos nativos do Windsor são proibidos** — calibrar no código da engine de Intelligence Hub
