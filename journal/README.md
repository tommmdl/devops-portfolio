# Diário de aprendizado

[English](README.en.md) · [Voltar ao portfólio](../README.md)

Este é o lugar para guardar o que mudou, o que deu errado e o que merece outra tentativa. Os registros abaixo apontam para os resultados já obtidos em cada laboratório.

- Dia 001: diagnóstico preparado em `linux-operations-lab`; script validado pelo assistente no WSL, análise pelo autor pendente.
- Jenkins: ambiente configurado; builds #1 SUCCESS e #2 FAILURE validados em 17/10/2026, com artefatos e persistência após recriação. [Evidências](https://github.com/tommmdl/jenkins-lab/blob/main/docs/validation.md).
- Docker: aplicação de notas bilíngue com PostgreSQL publicada em 17/10/2026; 23 testes verificaram CRUD, persistência e recuperação de indisponibilidade. [Evidências](https://github.com/tommmdl/docker-lab/blob/main/docs/validation.md).
- GitHub Actions: pipeline publicado em 17/10/2026; 23 testes passaram, a mesma imagem foi publicada no GHCR e o pull anônimo e uso local foram validados. [Evidências](https://github.com/tommmdl/github-actions-lab/blob/main/docs/validation.md).
- Terraform: infraestrutura Docker modular publicada em 17/10/2026; 22 verificações cobriram apply, idempotência, persistência, drift e destroy. CI de validação aprovado. [Evidências](https://github.com/tommmdl/terraform-lab/blob/main/docs/validation.md).

- Ansible: dois alvos configurados pelo mesmo role; 16 testes locais e no CI verificaram idempotência, alteração limitada, check mode, handlers e correção de drift. [Resultados](https://github.com/tommmdl/ansible-lab/blob/main/docs/validation.md).

- Kubernetes: a aplicação de notas entrou em um cluster kind dedicado; 24 testes locais e no CI cobriram réplicas, recuperação de Pods, PVC, escala e rollback. [Resultados](https://github.com/tommmdl/kubernetes-lab/blob/main/docs/validation.md).


- Monitoramento: Prometheus e Grafana acompanham a aplicação por sondas HTTP; 14 verificações locais cobriram coleta, consultas pelo painel, um alerta provocado por 404 e sua recuperação. [Resultados](https://github.com/tommmdl/monitoring-lab/blob/main/docs/validation.md).

- Logging: Alloy coleta os logs da API e do PostgreSQL pela API do Kubernetes; 16 verificações locais cobriram consultas no Loki e no Grafana, persistência após trocar o Pod do Loki e permissões restritas do coletor. [Resultados](https://github.com/tommmdl/logging-lab/blob/main/docs/validation.md).

Para as próximas entradas, use o [modelo](../templates/daily-log.md). Conte o que aconteceu e o que você entendeu, sem preencher dias só para manter uma sequência.
