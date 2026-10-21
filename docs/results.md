# Resultados que ajudam a entender o trabalho

[English](results.en.md) · [Início](../README.md) · [Arquitetura](architecture.md) · [Ordem de estudo](study-guide.md)

Seleção revisada em **20/10/2026**. Escolhi estes registros porque mostram uma decisão, uma falha ou uma recuperação que dá para inspecionar. Os números pertencem às execuções citadas; não são um placar acumulado nem uma promessa sobre a próxima execução.

## 1. Publicar o que foi testado

O GitHub Actions lab registra uma execução com **23 testes de integração** e verifica a identidade da imagem ao transferi-la entre jobs, publicá-la e baixá-la do GHCR. Também mantém a execução que falhou e impediu a publicação.

[Relato e proveniência](https://github.com/tommmdl/github-actions-lab/blob/main/docs/validation.md) · [CI citado](https://github.com/tommmdl/github-actions-lab/actions/runs/39073184363)

Isso demonstra aquele caminho de entrega. O workflow usa uma revisão fixada da aplicação, e o gate de vulnerabilidades é separado. Publicação bem-sucedida não equivale a aprovação de segurança.

## 2. Ver o self-heal acontecer

No ensaio local do Argo CD, a aplicação permaneceu com três réplicas por 30 segundos enquanto self-heal estava desligado. Ao ligá-lo, voltou a duas e ficou Synced/Healthy. Um segundo desvio foi corrigido, preservando o PVC e a nota do teste.

[Relatório de self-heal](https://github.com/tommmdl/argocd-lab/blob/main/evidence/notes-self-heal.json) · [Procedimento](https://github.com/tommmdl/argocd-lab#readme)

O registro inclui revisão e horário. Esse teste de notas foi executado localmente; a pipeline do repositório valida os manifests, sem executar esse ensaio de self-heal.

## 3. Seguir uma requisição até o SQL e os logs

O tracing-lab registra **19 verificações locais**, com propagação de um `traceparent` conhecido, relação entre spans Flask/Psycopg e consulta no Tempo/Grafana. O mesmo trace ID permite localizar logs no Loki. Há também repetição registrada no CI.

[Validação](https://github.com/tommmdl/tracing-lab/blob/main/docs/validation.md) · [Resumo dos spans](https://github.com/tommmdl/tracing-lab/blob/main/evidence/trace-summary.json) · [CI citado](https://github.com/tommmdl/tracing-lab/actions/runs/39128753855)

O span SQL observa o cliente de banco; não mede por dentro o processo PostgreSQL. A comparação com métricas e logs ajuda a explicar o alcance de cada sinal.

## 4. Trocar imagens com recuperação exercitada

A adoção das APIs Alpine básica e OpenTelemetry incluiu backup e rollback real de imagem, preservando notas criadas depois da troca. Para o PostgreSQL, a migração foi lógica: dump, restauração em volume novo e teste de retorno, com os volumes originais retidos.

[Adoção da API](https://github.com/tommmdl/security-lab/blob/main/docs/api-adoption.md) · [Adoção do PostgreSQL](https://github.com/tommmdl/security-lab/blob/main/docs/postgres-adoption.md) · [Scans e política](https://github.com/tommmdl/security-lab#readme)

Os achados das imagens antigas de recuperação continuam publicados e podem manter o resultado geral do gate bloqueado. Um scan sem achados descreve aquele digest e a base de vulnerabilidades daquela execução.

## 5. Recuperar o backup em outro lugar

O backup-restore-lab passou em **25 verificações locais e no CI** ao recuperar recursos e um dump em outro namespace. O disaster-recovery-lab passou em **32 locais e no CI**, restaurando em outro cluster enquanto a origem do exercício estava parada e sua API bloqueada a partir do destino. Os testes distinguem dados do backup de uma escrita posterior.

[Backup: validação](https://github.com/tommmdl/backup-restore-lab/blob/main/docs/validation.md) · [CI de backup](https://github.com/tommmdl/backup-restore-lab/actions/runs/39292524227) · [DR: validação](https://github.com/tommmdl/disaster-recovery-lab/blob/main/docs/validation.md) · [CI de DR](https://github.com/tommmdl/disaster-recovery-lab/actions/runs/39295149820)

Os restores terminaram com zero erros e dois avisos preservados. Os clusters e o S3 local compartilham o host. A origem isolada foi interrompida, sem destruir a aplicação principal ou simular perda da máquina.

## 6. Fazer failover e trazer as novas escritas de volta

O failover-lab passou em **48 verificações locais e no CI**. A troca exige bloquear o escritor anterior; o failback traz as notas criadas no destino. O teste também interrompe o controlador e reconcilia uma escrita que recebeu erro HTTP sem repeti-la automaticamente.

[Validação e falhas anteriores](https://github.com/tommmdl/failover-lab/blob/main/docs/validation.md) · [Relatório do runner](https://github.com/tommmdl/failover-lab/blob/main/evidence/ci-verification.json) · [CI citado](https://github.com/tommmdl/failover-lab/actions/runs/39310992536)

É um procedimento controlado com acesso aos dois clusters. Não demonstra eleição automática ou RPO zero geral. A suposição incorreta de que a sequência de IDs deveria ficar idêntica também permanece documentada.

## 7. Corrigir uma checagem que aprovava cedo demais

A checagem de troca de Pod misturava uma leitura de prontidão com outra de UIDs. Um controle com remoção real reproduziu o falso positivo. A correção usa uma observação coerente e confirma a saída do alvo do Chaos Mesh. Foram **116 verificações locais** e **123 em cada um de dois CIs** dessa etapa.

[Investigação](https://github.com/tommmdl/chaos-lab/blob/main/docs/pod-replacement.md) · [Controle real](https://github.com/tommmdl/chaos-lab/blob/main/evidence/pod-replacement-local-regression.json) · [CI dessa correção](https://github.com/tommmdl/chaos-lab/actions/runs/39417441792)

Os relatórios anteriores reprovados continuam disponíveis. Essa correção não eliminou os erros de conexão que motivaram a etapa seguinte.

## 8. Reproduzir os seis segundos com captura na matriz

O CI seguinte passou em **146 verificações** e reproduziu **cinco timeouts no estabelecimento TCP**, com SYNs retransmitidos e sem SYN-ACK. Quatro tiveram correspondência de pacotes para Pods em encerramento; o quinto começou antes da aplicação do experimento e continua sem backend identificado.

[Investigação completa](https://github.com/tommmdl/chaos-lab/blob/main/docs/resilience-timeouts.md) · [Casos e pacotes](https://github.com/tommmdl/chaos-lab/blob/main/evidence/matrix-timeouts-ci-39421860854-cases.json) · [Resumo do CI](https://github.com/tommmdl/chaos-lab/blob/main/evidence/matrix-timeouts-ci-39421860854-summary.json) · [CI citado](https://github.com/tommmdl/chaos-lab/actions/runs/39421860854)

As 32 capturas da matriz guardaram 432.610 quadros sem drops reportados; a reanálise dos arquivos reproduziu o resultado. Os controles de conexão e de espera por cabeçalhos ficam separados dos timeouts da API. A matriz local não reproduziu o timeout de seis segundos e manteve uma conexão lenta sem correspondência no intervalo observado.

A janela de atualização do encaminhamento e a permanência de uma tradução NAT são uma hipótese compatível com quatro casos. A falta de conntrack, regras e decisões de rota dessas tuplas impede apontar a causa exata. Aprovar recuperação e integridade da captura não significa que todas as requisições deram certo.

## 9. Construir uma microVM e verificar também o encerramento

O firecracker-lab compila Linux **6.12.113** com assinatura OpenPGP verificada e BusyBox **1.38.0** com SHA256 fixado. A imagem ext4 é montada do zero. A primeira tentativa chegou ao shell, mas faltavam os drivers AT/i8042/VT para receber Ctrl+Alt+Del: a API respondeu 204 e o encerramento precisou ser forçado. O teste ficou reprovado e o registro foi preservado.

Depois da correção, **dois boots locais** passaram em cópias novas do disco, com respostas do guest, root remontado somente para leitura, HTTP 204 e saída zero. Os hashes dos originais ficaram intactos. Há **dez testes de regressão** aprovados e um controle real que rejeita fonte alterado antes da extração.

[Construção e testes](https://github.com/tommmdl/firecracker-lab/blob/main/docs/build-from-source.md) · [Relatórios completos](https://github.com/tommmdl/firecracker-lab/blob/main/evidence/source-build-results.json) · [Hardening pendente](https://github.com/tommmdl/firecracker-lab#o-que-ainda-falta-de-hardening)

São testes locais em WSL2/KVM, sem boot no CI e sem integração com a aplicação de notas. O console mantém os achados de Spectre V2/Speculative Store Bypass. Hardening do kernel/console, rede/egress, toolchain hermético e isolamento completo ainda precisam de trabalho. O BusyBox tem verificação por checksum/HTTPS; não recebe a mesma garantia de assinatura do kernel. O lab ainda não valida execução segura de código não confiável.

### Primeiros controles com jailer

A etapa seguinte passou em duas execuções locais de seis cenários, observando UID/GID, capacidades, namespaces, raiz e seccomp após o boot. Os controles exercitaram throttling de CPU, rejeição de tarefas/descritores, OOM e corte por prazo. Perfis negativos e guests mortos não são declarados aprovados. [Testes e limites](https://github.com/tommmdl/firecracker-lab/blob/main/docs/jailer.md) · [Evidências](https://github.com/tommmdl/firecracker-lab/blob/main/evidence/jailer-results.json).

O auxiliar de preparação é privilegiado. `CapBnd` permanece amplo e alguns namespaces são compartilhados com ele. Um panic de shutdown sob quota apertada terminou com SIGSEGV e continua no histórico; esperar a carga e ampliar a quota ao encerrar passou nas repetições, sem provar causa ou eliminação do problema. CPU, rede do guest e isolamento para código não confiável continuam com pendências.


Na investigação seguinte, o Firecracker ganhou validação de binário musl estático e correções de prontidão do teclado e coleta do rastreador. Sob carga concorrente no host, a comparação corrigida teve dez encerramentos limpos por variante. A candidata com espera de cinco segundos tolerou um atraso controlado de 1,5 segundo na vCPU e ainda falhou com o atraso longo. As rodadas anteriores reprovadas continuam publicadas; o gatilho do panic histórico segue em aberto e a candidata continua experimental. [Investigação, resultados e limites](https://github.com/tommmdl/firecracker-lab/blob/main/docs/shutdown-investigation.md).

A [captura de escalonamento e sinais](https://github.com/tommmdl/firecracker-lab/blob/main/docs/vcpu-scheduling.md) acrescentou duas campanhas sequenciais com 24 encerramentos limpos e 12 traces válidos sob carga, com controles sem captura e teste de limite de tarefas. A maior espera pronta foi 13,262 ms. Houve throttling em dois encerramentos com meia CPU, ambos limpos; o panic espontâneo não reapareceu. A captura inicialmente vazia e uma sobreposição de campanhas foram preservadas e excluídas da comparação final.

A [investigação do protocolo com stacks do kernel](https://github.com/tommmdl/firecracker-lab/blob/main/docs/vcpu-protocol.md) acompanhou o binário oficial em 20 encerramentos limpos, dez deles instrumentados. A espera do canal chegou a 5,867 ms; o intervalo do `join`, a 83 µs. Uma stack em futex foi correlacionada à janela de espera do canal. Os erros de preparação, do validador e de leitura ficaram visíveis; o panic antigo não reapareceu e sua causa continua aberta.

## Como avaliar ou repetir

Abra o relato, localize a revisão e o relatório e confira o que foi realmente provocado e comparado. Os JSON completos ficam nos próprios repositórios; credenciais, dumps e conteúdo privado ficam fora do Git. As falhas esperadas são identificadas, e os limites não são convertidos em sucesso.

Para repetir, use a [ordem de estudo](study-guide.md) e a preparação do lab escolhido. Esta organização revisou a documentação e os links; não executou novamente todos os ambientes nem criou novos resultados operacionais.
