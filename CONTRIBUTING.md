# Contribuindo

Obrigado pelo interesse em contribuir com o **Agent Evals Framework**! 🎉

Este é um projeto **educativo, open-source e agnóstico de organização**.

## 🧭 Princípios

- **Conteúdo genérico**: sem dados, credenciais ou processos de organizações específicas.
- **Segurança**: nunca inclua segredos, tokens ou senhas em código, exemplos ou datasets.
- **Datasets fictícios**: qualquer dado de exemplo deve ser claramente marcado como fictício.
- **Rigor**: métricas e metodologias devem ser justificadas e, quando possível, referenciadas.

## 🌿 Fluxo de contribuição

1. Faça um **fork** do repositório.
2. Crie uma **branch** a partir da `main`:
   - `docs/...` para documentação
   - `feat/...` para novas funcionalidades (ex.: novo avaliador)
   - `fix/...` para correções
   - `chore/...` para manutenção
3. Faça commits pequenos e objetivos.
4. Abra um **Pull Request** para a `main` explicando o quê e o porquê.

## ✅ Conventional Commits

```
tipo: descrição curta no imperativo
```

Exemplos:
- `feat: adiciona avaliador de faithfulness`
- `docs: melhora catálogo de métricas`

## 🧩 Adicionando um novo avaliador

Um bom avaliador deve:
- [ ] Medir **uma dimensão** clara (qualidade, custo, latência ou confiabilidade)
- [ ] Retornar uma pontuação **normalizada** e documentada
- [ ] Incluir **testes** com casos de exemplo
- [ ] Ser documentado no [catálogo de métricas](docs/02-metricas.md)

## 💬 Dúvidas

Abra uma **issue** para propor ideias ou discutir mudanças maiores antes de implementá-las.

Toda contribuição é bem-vinda! 🙌
