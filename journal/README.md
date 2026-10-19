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

- Tracing: 19 verificações locais seguiram requisições reais Flask/Psycopg pelo Collector e Tempo, conferiram a propagação do pai, consultaram o Grafana e correlacionaram logs pelo trace ID. [Resultados](https://github.com/tommmdl/tracing-lab/blob/main/docs/validation.md).

- Configuração no Kubernetes: seis blocos e 26 exercícios locais próprios inspirados nos temas do iximiuz; 39 verificações cobriram ambiente, arquivos, atualização, ConfigMap imutável e TLS validado. [Resultados](https://github.com/tommmdl/kubernetes-config-lab/blob/main/docs/validation.md).

- Segurança de imagens: 15 testes locais cobriram decisões da política e scans reais de Dockerfiles com Trivy. Os gates das imagens bloquearam 48 ocorrências HIGH na API básica e 95 HIGH / 4 CRITICAL no PostgreSQL. [Resultados](https://github.com/tommmdl/security-lab/blob/main/docs/validation.md).

Para as próximas entradas, use o [modelo](../templates/daily-log.md). Conte o que aconteceu e o que você entendeu, sem preencher dias só para manter uma sequência.

- Correções nas imagens: a API passou de 173 para 164 achados e o PostgreSQL de 472 para 412. Nenhum achado restante tem correção publicada nessa fotografia do Trivy; o gate ainda bloqueia 44 HIGH na API e 71 HIGH / 3 CRITICAL no banco. As mudanças chegaram ao Compose e ao Argo CD com testes de integração, restauração e tracing. [Relatórios completos de antes e depois](https://github.com/tommmdl/security-lab/blob/main/docs/remediation.md).

- Análise dos críticos do PostgreSQL: SQLite e ferramentas GPG sem uso removidos; aplicação separada do superusuário bootstrap. Os achados passaram de 412 para 350, com dois críticos mantidos. A libxml2 continua afetada e recebe controles compensatórios; o empacotamento do Debian e a inspeção sustentam que o MiniZip afetado está ausente da zlib distribuída. Nenhuma exceção foi acrescentada ao gate. Passaram os testes da API, de privilégios, de atualização do volume, de Kubernetes e de tracing. [Análise e evidências](https://github.com/tommmdl/security-lab/blob/main/docs/postgresql-critical.md).

- Alternativa PostgreSQL: Alpine 3.24.2 / PostgreSQL 17.11 com libxml2 2.13.9-r2, auxiliar estático corrigido e zlib atualizada. A candidata testada tem zero achados reportados na fotografia registrada do Trivy, sem exceções. Sete notas Unicode sobreviveram à migração lógica, aos testes da API/ciclo de vida e à restauração de volta ao Debian; backups privados dos labs existentes também foram restaurados com sucesso. A alternativa usa volume próprio e localhost:8015; os bancos originais permanecem iguais. [Comparação e evidências](https://github.com/tommmdl/security-lab/blob/main/docs/postgres-alternative.md).

### PostgreSQL Alpine adotado com rollback real

Docker e Kubernetes agora usam o digest Alpine testado. Pausamos as escritas, restauramos backups lógicos em volumes novos e guardamos os originais Debian. Uma nota criada após a troca sobreviveu ao retorno real da API por outro volume/PVC Debian restaurado; depois os dois labs voltaram ao Alpine. Conferimos self-heal, logs e traces. Os achados completos continuam visíveis, incluindo a imagem afetada de recuperação. [Procedimento e evidências nos dois idiomas](https://github.com/tommmdl/security-lab/blob/main/docs/postgres-adoption.md).

### Olhando de perto os HIGH da API

Os 44 HIGH representam oito CVEs do sistema operacional. Os candidatos do repositório estável continuam iguais às versões instaladas. Conferimos privilégios e componentes presentes e limitamos os recursos da API no Compose e no Kubernetes. Os achados completos continuam visíveis e bloqueando; mitigação não foi apresentada como patch de binário. [Análise nos dois idiomas](https://github.com/tommmdl/security-lab/blob/main/docs/api-high-review.md).

### Testando Alpine para a API

As variantes básica e OpenTelemetry ficaram com zero achados e inventário completo, depois de retirar ferramentas de instalação sem uso e atualizar a zlib. Cada uma passou em 23 testes da API e 20 de segurança do banco; conferimos tracing real pelo Collector/Tempo e pelo Grafana/Loki em outro workload Kubernetes. A API Debian principal e seus 44 HIGH foram preservados. [Ensaio e evidências](https://github.com/tommmdl/security-lab/blob/main/docs/api-alpine.md).

### APIs Alpine adotadas com rollback real de imagem

Docker/Kubernetes básico passam ao digest Alpine básico publicado; o tracing GitOps usa o digest instrumentado. Restauramos backups privados em separado e comprovamos que notas escritas após a troca sobreviveram ao retorno Debian e à volta ao Alpine. Containers/PVCs e schema do PostgreSQL continuam iguais. Imagens ativas e de recuperação têm alvos de scan separados. [Procedimento e evidências](https://github.com/tommmdl/security-lab/blob/main/docs/api-adoption.md).

- Alertas: 23 verificações locais seguiram falhas reais da API e do banco até o Alertmanager e o receptor HTTP, com resolução, agrupamento, inibição, silêncios e persistência. A aplicação e o GitOps foram restaurados ao final. [Resultados em português e inglês](https://github.com/tommmdl/alerting-lab/blob/main/docs/validation.md).

- Backup e restauração: 25 verificações locais recuperaram a aplicação e um dump lógico do PostgreSQL com Velero/Kopia em namespace e PVCs novos. Falha de hook, checksum inválido, dados, schema, índices e sequência foram conferidos; a escrita posterior permaneceu apenas na origem. [Resultados e avisos preservados](https://github.com/tommmdl/backup-restore-lab/blob/main/docs/validation.md).
