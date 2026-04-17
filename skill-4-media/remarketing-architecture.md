# Remarketing Architecture — SST
## Estado atual + arquitetura target

**Última atualização:** 2026-04-17 (via Windsor data L30D)
**Dono:** Leonardo (estratégia) + Vanessa (execução)
**Cadência de revisão:** mensal (via Monthly Media Review)
**Documento canônico:** Remarketing Reestruturação 5-tier SST (Google Drive — inserir URL quando migrado)

---

## Seção A — Arquitetura ATUAL (estado real)

SST opera hoje com **2 campanhas de Remarketing ativas**:

| Campanha | Spend 30d | Purchases | ROAS | Frequência | Audiência (presumida) |
|----------|-----------|-----------|------|------------|----------------------|
| #CA_Compra_Remarketing-2 | R$10.536 | 93 | 2,26x | 1,98 | Visitantes + ATC (consolidado) |
| #CA_Compra_Retenção | R$2.983 | 51 | 4,35x | 2,17 | Compradores (recompra) |

**Budget allocation RMKT atual:**
- Remarketing-2: ~78% do spend RMKT
- Retenção: ~22% do spend RMKT

**Observações operacionais:**
- Frequência média 1,98-2,17 está ABAIXO do range saudável RMKT (3-5). Indica audiências grandes OU subinvestimento em RMKT.
- Retenção com ROAS 4,35x (excepcional) com spend relativamente baixo — candidato a scaling (validar audience size antes).
- Audiência real de cada campanha precisa ser confirmada no Meta Ads Manager (este doc presume baseado no naming).

---

## Seção B — Arquitetura TARGET (5-tier)

**Status:** projeto de evolução, ainda não implementado.

| Tier | Audiência | Janela | Budget target | ROAS esperado | Freq saudável | Freq warning |
|------|-----------|--------|---------------|---------------|---------------|--------------|
| HOT (ATC) | ATC não-compradores | 0-30d | 30% | 5x+ | 3-5 | 6+ |
| WARM (Visitantes) | Visitantes não-compradores | 0-30d | 25% | 3-4x | 3-5 | 6+ |
| COOL (Visitantes antigos) | Visitantes não-compradores | 30-90d | 15% | 2-3x | 3-5 | 6+ |
| GOLD (Recompra) | Compradores | 60-180d | 20% | 4x+ | 2-4 | 5+ |
| BRIDGE (Engajados) | Engajados IG/FB não-visitantes | 14-30d | 10% | 2x+ | 2-4 | 5+ |

---

## Seção C — Gap analysis (atual vs. target)

| Tier target | Estado atual | Gap |
|-------------|--------------|-----|
| HOT | Consolidado dentro de Remarketing-2 | Faltam audiência dedicada + criativos específicos |
| WARM | Remarketing-2 (parcial) | Ok, mas mistura com HOT |
| COOL | Não explorado | Audiência 30-90d não tem campanha |
| GOLD | Retenção (performance excepcional) | Estrutura existe, nome não alinhado com target |
| BRIDGE | Não explorado | Audiência engajados IG/FB não explorada |

---

## Seção D — Roadmap de evolução (proposta)

**Fase 1 — Separar HOT de WARM (próximo ciclo de 30d)**
- Criar campanha `#RMKT_HOT_ATC` com audiência ATC 0-30d isolada
- Realocar 30% do budget Remarketing-2 pra HOT
- Remarketing-2 vira WARM (visitantes não-compradores apenas)
- Expectativa: ROAS HOT 5x+ (ATC audience tem intenção maior)

**Fase 2 — Renomear Retenção → GOLD + validar janela (Q2 2026)**
- Ajustar naming: `#CA_Compra_Retenção` → `#RMKT_GOLD_Recompra`
- Validar janela atual (é 60-180d?)
- Considerar scaling controlado dado ROAS 4,35x — verificar audience size

**Fase 3 — Explorar COOL e BRIDGE (Q3 2026)**
- COOL: criar segmento visitantes 30-90d com criativo de re-aproximação
- BRIDGE: testar audiência engajados IG/FB (Manu Marques, Mari Arpini, etc)
- Budget conservador (5-10% cada) até validar performance

---

## Critérios operacionais por tier target

### HOT — ATC não-compradores (quando implementado)
- Criativos: prova social direta, oferta clara, senso de urgência
- Sinal de fadiga: frequência >6 OU ROAS <4x por 7d
- Ação de fadiga: creative refresh via SKILL 3

### WARM — Visitantes recentes (Remarketing-2 evoluído)
- Criativos: educacional + benefício + soft CTA
- Sinal de fadiga: frequência >6 OU ROAS <2,5x por 7d

### COOL — Visitantes antigos (quando implementado)
- Criativos: re-aproximação + novidade + oferta forte
- Sinal de fadiga: frequência >6 OU ROAS <2x por 10d

### GOLD — Compradores (Retenção atual)
- Criativos: cross-sell, lançamentos, programa de fidelidade
- Sinal de fadiga: ROAS <3x por 14d

### BRIDGE — Engajados não-visitantes (quando implementado)
- Criativos: educação ao produto + quebra de objeção
- Sinal de fadiga: frequência >5 OU ROAS <1,5x por 10d

---

## Notas operacionais

- Arquitetura target documentada: doc canônico no Drive
- Evolução prevista vs estrutura anterior consolidada: 2,26x → 4,0x+ projetado (após implementação completa)
- Recalibração mensal via Monthly Media Review
- Mudanças estruturais (ex: migração Fase 1) requerem Structure Change Order via SKILL 4 Bloco B

