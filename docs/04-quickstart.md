# 04 – Início Rápido (Quickstart)

Guia conceitual para rodar sua primeira avaliação. As APIs de código são **ilustrativas** (o framework está em fase de documentação/alpha).

## 1. Estruture seu dataset

Crie um arquivo JSON com casos de teste. Veja o exemplo completo em [`datasets/example-eval-set.json`](../datasets/example-eval-set.json).

```json
{
  "name": "meu-eval-set",
  "cases": [
    {
      "id": "case-001",
      "input": "Qual a capital da França?",
      "expected": "Paris",
      "category": "factual"
    }
  ]
}
```

## 2. Crie um adapter para seu agente

O adapter conecta seu agente ao framework. Basta expor uma função que recebe a entrada e devolve a saída + metadados.

```python
# adapters/meu_agente.py (ilustrativo)
def run(input_text: str) -> dict:
    resposta = meu_agente.invoke(input_text)
    return {
        "output": resposta.text,
        "tokens": resposta.usage,
        "tool_calls": resposta.tools_used,
    }
```

## 3. Configure o experimento

```yaml
# config.yaml (ilustrativo)
dataset: datasets/example-eval-set.json
agent: adapters/meu_agente.py
repetitions: 3          # mede variabilidade
evaluators:
  - quality.llm_judge
  - cost.tokens
  - latency.total
  - reliability.success_rate
baseline: results/v1.json
```

## 4. Execute a avaliação

```bash
# (ilustrativo)
python -m agent_evals run --config config.yaml --out results/v2.json
```

## 5. Leia o relatório

```bash
python -m agent_evals report --current results/v2.json --baseline results/v1.json
```

Saída esperada (exemplo):

```
✅ 20/20 casos executados
Qualidade média (llm_judge): 4.5 / 5
Custo médio: $0.018 / execução
Latência p95: 1650 ms
Success rate: 97%

Comparado ao baseline v1: qualidade ▲, custo ▲ (avaliar).
```

## Próximos passos

- Amplie o dataset com **edge cases** e **casos adversariais**.
- Adicione um avaliador customizado (veja [`docs/03-arquitetura.md`](03-arquitetura.md)).
- Integre a avaliação ao seu **CI** para detectar regressões em cada PR.
