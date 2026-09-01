# 02 – Catálogo de Métricas

Referência das métricas suportadas pelo framework, agrupadas pelos 4 pilares. Use este catálogo para escolher **o que medir** de acordo com o objetivo do seu agente.

## 📏 Qualidade

| Métrica | Descrição | Faixa | Quando usar |
|---------|-----------|-------|-------------|
| `exact_match` | A saída é idêntica à esperada | 0–1 | Respostas canônicas (fatos, classificação) |
| `semantic_similarity` | Similaridade por embeddings | 0–1 | Respostas abertas com sentido equivalente |
| `llm_judge_score` | Nota atribuída por LLM-juiz | 0–5 | Qualidade subjetiva (clareza, utilidade) |
| `schema_valid` | Saída respeita o formato/JSON esperado | bool | Saídas estruturadas |
| `faithfulness` | Resposta fiel às fontes (anti-alucinação) | 0–1 | Agentes RAG |

## 💰 Custo

| Métrica | Descrição | Unidade |
|---------|-----------|---------|
| `input_tokens` | Tokens consumidos na entrada | tokens |
| `output_tokens` | Tokens gerados na saída | tokens |
| `total_cost` | Custo monetário estimado | moeda |
| `tool_calls` | Número de chamadas a ferramentas | contagem |

## ⏱️ Latência

| Métrica | Descrição | Unidade |
|---------|-----------|---------|
| `latency_total` | Tempo total da execução | ms |
| `latency_p50` | Mediana entre execuções | ms |
| `latency_p95` | Percentil 95 (cauda lenta) | ms |
| `time_to_first_token` | Tempo até o primeiro token | ms |

## 🛡️ Confiabilidade

| Métrica | Descrição | Faixa |
|---------|-----------|-------|
| `success_rate` | % de execuções sem erro | 0–1 |
| `tool_correctness` | Uso da ferramenta correta | 0–1 |
| `hallucination_rate` | % de respostas com informação inventada | 0–1 |
| `robustness` | Estabilidade sob entradas adversariais | 0–1 |

## Como interpretar

- **Nunca olhe uma métrica isolada.** Um agente pode ter alta qualidade e custo proibitivo.
- **Estabeleça limiares (thresholds)** aceitáveis para cada métrica antes de rodar.
- **Compare sempre contra um baseline** — o valor absoluto importa menos que a variação.

### Exemplo de scorecard agregado

```
Agente v2 vs v1 (baseline)
──────────────────────────────
Qualidade (llm_judge)  4.2 → 4.5   ▲ +0.3
Custo médio ($)        0.012 → 0.018  ▲ +50%  ⚠️
Latência p95 (ms)      1800 → 1650  ▼ -8%
Success rate           0.94 → 0.97   ▲ +3pp
──────────────────────────────
Veredito: melhor qualidade, mas avaliar o aumento de custo.
```
