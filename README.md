# DevOps na prática

[English](README.en.md) · Português

Aqui reúno meus projetos de DevOps e os caminhos que estou explorando para entender melhor cada ferramenta. A ideia é começar com algo que funciona, provocar algumas falhas e descobrir como investigar e recuperar o ambiente.

Cada laboratório tem seu próprio repositório, com código, instruções e um registro do que foi testado. Dá para acompanhar a sequência ou escolher um assunto e começar por ele.

## Por onde começar

| Projeto | O que você vai encontrar |
| --- | --- |
| [Linux](https://github.com/tommmdl/linux-operations-lab) | Um script para olhar memória, disco e carga do sistema e praticar os primeiros diagnósticos. |
| [Docker](https://github.com/tommmdl/docker-lab) | Uma aplicação de notas com PostgreSQL para explorar redes, volumes e o que acontece quando o banco para. |
| [Jenkins](https://github.com/tommmdl/jenkins-lab) | Um primeiro pipeline, um build que passa e outro que falha de propósito para ajudar a entender os logs. |
| [GitHub Actions](https://github.com/tommmdl/github-actions-lab) | A aplicação passando por testes antes de ter sua imagem publicada no GHCR. |
| [Terraform](https://github.com/tommmdl/terraform-lab) | O mesmo ambiente descrito como código: criar, conferir mudanças, corrigir drift e remover os recursos. |
| [Ansible](https://github.com/tommmdl/ansible-lab) | Um role configura dois alvos; depois entram repetição sem mudanças, templates, handlers e correção de drift. |
| [Kubernetes](https://github.com/tommmdl/kubernetes-lab) | A aplicação ganha réplicas, um banco com volume e exercícios de recuperação, escala e rollback no cluster local. |
| [Argo CD](https://github.com/tommmdl/argocd-lab) | A aplicação passa a seguir o Git, com testes de drift e correção automática pelo self-heal. |
| [Prometheus e Grafana](https://github.com/tommmdl/monitoring-lab) | Sondas acompanham a aplicação, um painel mostra os sinais e um exercício testa o alerta e a recuperação. |
| [Loki e Grafana](https://github.com/tommmdl/logging-lab) | Os logs da API e do banco chegam ao Loki; um marcador ajuda a seguir a mensagem até o Grafana. |
| [OpenTelemetry e Tempo](https://github.com/tommmdl/tracing-lab) | Uma requisição ganha spans da API e do banco, com o mesmo trace ID disponível nos logs. |

Se você está chegando agora, eu começaria por Linux e Docker. Vários projetos reaproveitam a aplicação de notas para conectar os assuntos. O Ansible usa dois alvos pequenos para explorar a configuração de servidores.

## O que já foi colocado à prova

Os repositórios guardam os comandos e resultados das verificações: builds de sucesso e falha no Jenkins, testes de integração com banco, publicação de imagem e o ciclo de vida da infraestrutura com Terraform. Cada projeto explica também os limites desses testes.

Esses são ambientes de estudo. Os registros distinguem o que foi executado com ajuda do assistente do que ainda está pendente de exploração pelo autor.

## Um roteiro para continuar

A trilha de 100 dias serve como direção. O ritmo pode mudar conforme os exercícios ficam mais interessantes ou difíceis.

| Dias | Assunto |
| --- | --- |
| 01–10 | Linux, Bash e Git |
| 11–20 | Redes, DNS, HTTP e TLS |
| 21–30 | Docker e Compose |
| 31–40 | Jenkins e GitHub Actions |
| 41–50 | Terraform |
| 51–60 | Ansible e cloud |
| 61–70 | Kubernetes |
| 71–80 | GitOps e segurança |
| 81–90 | Observabilidade e SRE |
| 91–100 | Integração, recuperação e apresentação dos projetos |

GitOps, métricas de disponibilidade, logs e traces já fazem parte da trilha. Métricas internas mais completas, segurança e recuperação são caminhos para continuar. Eles entram aqui conforme os projetos forem desenvolvidos; o roteiro não representa trabalho já concluído.

## Anotar faz parte

O [diário](journal/README.md) reúne os avanços. O [modelo de registro](templates/daily-log.md) ajuda a guardar decisões, erros e próximos passos, além do código. Não há publicação diária automática.

Os projetos têm documentação em português e inglês. Senhas e estados de infraestrutura ficam fora do Git. Quando houver exercícios em cloud paga, a documentação deve incluir custos e como remover os recursos.

[Sobre a revisão do histórico](docs/history.md)
