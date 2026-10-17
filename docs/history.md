# Sobre o histórico / About the history

Em 17/10/2026, as mensagens dos commits da branch `main` foram encurtadas para facilitar a leitura. Essa etapa preservou os arquivos de cada commit, seus autores e suas datas. Depois vieram as alterações de documentação. Os backups do histórico anterior foram salvos localmente antes do force push.

Os relatórios, logs e metadados de imagens continuam mostrando os SHAs usados nas execuções originais. Eles são registros históricos e não foram alterados para aparentar novas execuções. A tabela relaciona esses commits com os commits equivalentes do histórico revisado. O pipeline passa a usar uma revisão acessível do histórico novo em `source.json`.

On 2026-10-17, commit messages on `main` were shortened for readability. This step preserved each commit's files, authors and dates; documentation edits came afterward. Local backups were saved before the force push.

Reports, logs and image metadata still show the SHAs used by their original runs. They are historical records, not rewritten test results. The table maps those commits to their equivalents in the revised history. The pipeline's `source.json` uses an accessible revision from the new history.

| SHA anterior / Previous SHA | SHA equivalente / Equivalent SHA | Mensagem / Message |
| --- | --- | --- |
| `98fe92e91c290b9cf013949302613b9e7a031279` | `67b515c2569435dc313e17d8e0b2fd3ffdcf80a3` | Cria o índice do portfólio DevOps |
| `3820bd6aba30dc29e93cb364a2474e52498c9064` | `d8457ccc6bd612d5ce0e3d87d7c4b91044731362` | Adiciona os primeiros laboratórios ao portfólio |
| `dbb709fe801ba761ba96d43f3e41a45e307c1bd6` | `c29f4578d517d4a8f35d1fdd2738396ec93c8964` | Registra os primeiros builds do Jenkins |
| `566df574aae14eaad79eb6e7f83f8e2e4bbfb3af` | `b5a1a09de653919a555155c9af035cdbd162d264` | Adiciona o laboratório Docker |
| `481932eea33e7cbaf5833810c8016111918d8d4a` | `909866dc928bffd073aafd83ee0a620bab71f3be` | Adiciona o pipeline do GitHub Actions |
| `f84594509c27e36435489ab0c90c66e0619f200d` | `21d9633e48e3d712395e49da751db6587f490936` | Adiciona o laboratório Terraform |
