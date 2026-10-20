# Uma ordem para estudar e repetir

[English](study-guide.en.md) · [Início](../README.md) · [Arquitetura](architecture.md) · [Evidências](results.md)

A sequência abaixo ajuda a conectar os assuntos sem exigir um calendário. Escolha uma etapa, execute seu exercício e anote o que conseguiu explicar. Os links abrem o README com os comandos e os cuidados daquele projeto.

## Antes de começar

Tenha Git e, para os labs de containers, Docker funcionando em Linux/WSL. Confira versões, ferramentas e portas no README escolhido; os requisitos variam. Os exercícios de Ansible, Terraform e Jenkins têm ambientes próprios. Os de observabilidade integram componentes do cluster principal.

Quando uma integração pedir projetos vizinhos, mantenha a organização como nesta árvore. Ela é um exemplo de disposição dos checkouts, não uma lista para instalar tudo de uma vez:

```text
estudos/
├── devops-portfolio/
├── docker-lab/
├── kubernetes-lab/
├── argocd-lab/
├── monitoring-lab/
├── logging-lab/
└── tracing-lab/
```

## A trilha

| Etapa | Projetos e exercício | O que conseguir explicar antes de avançar |
| --- | --- | --- |
| 1 · Ler o sistema | [Linux](https://github.com/tommmdl/linux-operations-lab): rode o diagnóstico e compare com as consultas individuais. | O que carga, memória disponível e espaço em disco dizem — e o que o script não mede. |
| 2 · Rodar a aplicação | [Docker](https://github.com/tommmdl/docker-lab): crie uma nota, recrie containers, pare e religue o banco. | Por que o dado sobrevive, como a API encontra o banco e a diferença entre liveness e readiness. |
| 3 · Entregar uma revisão | [Jenkins](https://github.com/tommmdl/jenkins-lab): provoque um build quebrado. [GitHub Actions](https://github.com/tommmdl/github-actions-lab): siga a imagem até o GHCR. | Qual etapa falhou, qual artefato ficou salvo e como conferir a identidade da imagem publicada. |
| 4 · Descrever mudanças | [Terraform](https://github.com/tommmdl/terraform-lab): plan/apply, drift e destroy no Docker local. [Ansible](https://github.com/tommmdl/ansible-lab): duas execuções, mudança limitada e correção de drift. | O papel do state, o significado de um plano e por que a segunda execução de um role pode ter `changed=0`. |
| 5 · Entender o cluster | [Kubernetes](https://github.com/tommmdl/kubernetes-lab): réplicas, Service, PVC e rollback. [Configuração](https://github.com/tommmdl/kubernetes-config-lab): ConfigMaps, Secrets, TLS e Downward API. | Quem repõe um Pod, como readiness muda os endpoints e o que um PVC preserva. |
| 6 · Seguir o Git e avaliar imagens | [Argo CD](https://github.com/tommmdl/argocd-lab): compare drift sem/com self-heal. [Segurança](https://github.com/tommmdl/security-lab): leia um bloqueio e os relatórios das alternativas. | Quem controla o estado desejado, por que publicar não significa passar no gate e como separar achado, correção e mitigação. |
| 7 · Observar de ponta a ponta | [Monitoring](https://github.com/tommmdl/monitoring-lab) → [Logging](https://github.com/tommmdl/logging-lab) → [Tracing](https://github.com/tommmdl/tracing-lab) → [Alerting](https://github.com/tommmdl/alerting-lab). Faça uma requisição e depois provoque uma falha. | Como passar de uma sonda ou alerta para logs e spans; como confirmar a recuperação e a entrega da notificação. |
| 8 · Recuperar e retornar | [Backup](https://github.com/tommmdl/backup-restore-lab) → [DR](https://github.com/tommmdl/disaster-recovery-lab) → [Failover](https://github.com/tommmdl/failover-lab). Compare o ponto de backup, os dados restaurados e as escritas no destino. | Por que replicação e backup resolvem problemas diferentes; por que bloquear o escritor anterior e reconciliar uma resposta incerta. |
| 9 · Investigar falhas | [Chaos Mesh](https://github.com/tommmdl/chaos-lab): acompanhe HTTP, alertas, eventos, pacotes e recuperação nas remoções. | A diferença entre recuperar réplicas e atender todas as requisições; o que prova um SYN sem resposta e o que continua desconhecido. |
| 10 · Aprofundar em microVMs | [Firecracker](https://github.com/tommmdl/firecracker-lab): verifique fontes, compile kernel/rootfs, execute o boot em uma cópia e confira o encerramento. | Por que HTTP 204 não prova shutdown, como os hashes preservam os originais e quais proteções ainda não foram validadas. |

Você pode fazer o primeiro scan do security-lab logo depois do Docker e voltar a ele ao trocar imagens. Na etapa de automação, Terraform e Ansible ensinam abordagens diferentes em ambientes separados; o Terraform deste portfólio não provisiona os clusters kind.

O Firecracker é uma trilha independente de aprofundamento: dá para iniciá-la depois de Linux, sem subir os clusters ou a aplicação de notas. Exige Linux x86-64 com KVM acessível para o boot, ferramentas de compilação e espaço para fontes e cópias do disco. Comece pelo [guia de construção](https://github.com/tommmdl/firecracker-lab/blob/main/docs/build-from-source.md), leia o hardening pendente e use apenas tarefas conhecidas nesta etapa.

## Dependências que merecem atenção

A base da integração é o **kubernetes-lab**. O **argocd-lab** adota sua aplicação. O **monitoring-lab** prepara Prometheus e Grafana; o **logging-lab** acrescenta Loki e Alloy; o **tracing-lab** usa essas peças para ligar traces e logs. O **alerting-lab** reaproveita as sondas e o Prometheus.

Antes do DR, complete o backup-restore-lab e guarde o kit descrito no disaster-recovery-lab. O failover-lab usa os dois clusters, com bancos próprios. O chaos-lab instala uma aplicação e observação isoladas no cluster de estudo; siga seu preparo de kernel e permissões.

A partir da adoção pelo Argo CD, faça mudanças permanentes na aplicação por sua fonte Git. Para repetir exercícios manuais anteriores, siga o procedimento de convivência do lab; reaplicar um bootstrap antigo pode disputar o estado desejado.

## Um ciclo de estudo que cabe em qualquer etapa

1. Leia o objetivo, o alcance e a limpeza do exercício.
2. Confira o estado inicial e formule uma hipótese: o que deve acontecer quando o banco parar ou o Pod sair?
3. Rode o cenário e compare a previsão com logs, respostas, recursos e dados.
4. Registre o resultado com a revisão usada, incluindo erros e recuperação.
5. Repita uma variação pequena e explique o resultado com suas palavras.

Use o [modelo de anotação](../templates/daily-log.md) e acrescente ao [diário](../journal/README.md) o que aprendeu. Uma dúvida bem delimitada também é um resultado útil.

## Para apresentar o portfólio

Comece com a aplicação do Docker lab, mostre o caminho de publicação e escolha uma investigação ou recuperação. Nos [resultados selecionados](results.md), abra o relatório correspondente e explique a hipótese, o teste, a conclusão e um limite. Vale conseguir responder por que o teste passou mesmo registrando falhas HTTP, ou por que um restore concluído ainda deixou avisos.

O roteiro segue o que está publicado. Domínio do assunto aparece ao repetir, interpretar e defender as decisões; a implementação assistida está registrada nos projetos. O próximo passo pode ser aprofundar uma lacuna observada, em vez de adicionar outra ferramenta.
