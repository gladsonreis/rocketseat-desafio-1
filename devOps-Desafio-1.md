# Plano de Implementação de Práticas DevOps na Tech

## 1. Diagnóstico Cultural (C de CALMS)

### Processo identificado para melhoria  
**Entrega e implantação de código (deploy)** no ambiente de produção.

### Descrição do processo atual
- Os desenvolvedores finalizam uma funcionalidade e empacotam o código manualmente.
- O pacote é enviado por e-mail ou pendrive à equipe de Operações.
- A equipe de Operações realiza o deploy manualmente, sem checklist padronizado.
- Testes são feitos após o deploy em produção.
- Não há rollback automatizado; falhas exigem intervenção manual prolongada.

### Pontos de atrito
- **Silos organizacionais**: Desenvolvimento e Operações atuam de forma isolada (mentalidade de “jogue por cima do muro”).
- **Falta de responsabilidade compartilhada**: Desenvolvedores não acompanham a performance em produção; operadores não participam do planejamento.
- **Baixa confiabilidade**: Deploy manual com 20% de falha gera insatisfação, retrabalho e risco de impacto ao cliente.
- **Conhecimento concentrado**: Apenas um desenvolvedor domina o sistema legado em Delphi, representando risco único de falha (bus factor = 1).

### Oportunidades de melhoria
- Integrar Dev e Ops desde o início do ciclo de vida do software.
- Estabelecer responsabilidade conjunta pela entrega e estabilidade em produção.
- Criar canais formais de comunicação e colaboração.

---

## 2. Automação (A de CALMS)

### Solução proposta
Implementar um **pipeline de CI/CD (Integração Contínua / Entrega Contínua)** com as seguintes etapas:

1. **Controle de versão centralizado** (Git + GitFlow).
2. **Build automatizado** em cada push (ex: usando Jenkins, GitHub Actions ou Azure DevOps).
3. **Testes automatizados** (unitários, integração, regressão).
4. **Deploy automatizado** nos ambientes de staging e produção.
5. **Rollback automático** em caso de falha crítica.

### Tecnologias sugeridas
- **Git** + **GitHub/GitLab** para versionamento.
- **Docker** para containerização (isola dependências, facilita testes e deploy).
- **Jenkins ou GitHub Actions** para orquestração do pipeline.
- **Ansible ou Terraform** para provisionamento da infraestrutura (IaC).
- **SonarQube** para análise de qualidade de código.

### Plano de implementação

| Etapa | Ação | Prazo | Envolvidos |
|------|------|-------|-----------|
| 1 | Treinamento introdutório sobre CI/CD e Git | Semana 1 | Todos |
| 2 | Containerizar aplicações (incluindo legado em Delphi com cuidado) | Semanas 2–3 | Dev + Ops |
| 3 | Configurar pipeline básico (build + testes) | Semana 4 | DevOps Engineer |
| 4 | Automatizar deploy em staging | Semana 5 | Ops + Dev |
| 5 | Validar e estender para produção com rollback | Semana 6–7 | Todos |
| 6 | Documentação e suporte contínuo | Contínuo | Líderes técnicos |

### Minimização de resistências
- Envolver as equipes desde o início (co-criação do pipeline).
- Demonstrar ganhos rápidos (ex: redução de 2 dias para 2 horas no deploy).
- Criar “campeões DevOps” em cada equipe para multiplicar a cultura.
- Manter o sistema legado funcional durante a transição (estratégia de strangler fig).

---

## 3. Mensuração e Compartilhamento de Conhecimento (M e S de CALMS)

### Métricas propostas (KPIs DevOps)

| Categoria | Métrica | Objetivo |
|----------|--------|--------|
| **Velocidade** | Tempo de ciclo (do commit ao deploy) | Reduzir de 2 dias para < 4 horas |
| **Qualidade** | Taxa de sucesso dos deploys | Aumentar de 80% para > 98% |
| **Estabilidade** | MTTR (Mean Time to Recover) | Reduzir de 4h para < 30 min |
| **Confiabilidade** | Número de incidentes pós-deploy | Reduzir de 2/semana para ≤ 0,5/semana |
| **Produtividade** | Frequência de deploys | Aumentar de 1–2/semana para diário |

### Plano de compartilhamento de conhecimento
- **Reuniões de retrospectiva quinzenais**: com Dev, Ops e Product Owner.
- **Dashboard de métricas visível a todos**: usando Grafana + Prometheus ou Azure Monitor.
- **Wiki interna**: documentação viva dos pipelines, arquitetura e boas práticas.
- **Dojos técnicos mensais**: sessões práticas sobre Docker, CI/CD, observabilidade.
- **Mentoria cruzada**: desenvolvedores aprendem sobre infra; operadores aprendem sobre código (especialmente o legado em Delphi).
- **Gamificação**: reconhecimento público por contribuições à melhoria contínua.

---

## 4. Aplicação das Três Maneiras do DevOps

### Primeira Maneira: Acelerar o Fluxo de Trabalho (Left to Right)
- **Eliminar gargalos**: automatizar testes e deploy para reduzir handoffs manuais.
- **Pequenos lotes**: dividir features em entregas menores e frequentes.
- **Ambientes idênticos**: usar containers para garantir que “funciona na minha máquina = funciona em produção”.
- **Resultado esperado**: entrega contínua de valor ao cliente com menor risco.

### Segunda Maneira: Ampliar o Feedback (Right to Left)
- **Monitoramento em tempo real**: logs estruturados, métricas e alertas (ex: ELK Stack + Prometheus).
- **Notificações automáticas**: alertas no Slack/Teams quando um deploy falha ou o sistema degrada.
- **Feedback rápido aos devs**: relatórios de qualidade de código e cobertura de testes integrados ao PR.
- **Revisão pós-incidente (blameless postmortem)**: análise colaborativa sem punição.
- **Resultado esperado**: falhas detectadas e corrigidas mais cedo, com aprendizado compartilhado.

### Terceira Maneira: Cultura de Experimentação e Aprendizado Contínuo
- **Ambiente seguro para falhar**: permitir testes em staging com dados sintéticos.
- **Simulações de falha (Chaos Engineering)**: em ambiente controlado, para testar resiliência.
- **Incentivo à inovação**: alocação de 10% do tempo para experimentos (ex: migrar legado para microsserviços).
- **Reconhecimento de aprendizado**: histórias de “o que aprendemos com o erro X” compartilhadas na intranet.
- **Resultado esperado**: cultura de melhoria contínua, onde a inovação é segura e valorizada.

---

## Conclusão

A implementação das práticas DevOps na **Tech** não se resume à automação de ferramentas, mas à transformação cultural apoiada por processos, métricas e colaboração. Ao aplicar o framework **CALMS** e as **Três Maneiras**, a empresa poderá:

- Reduzir significativamente o tempo e risco de entrega.
- Aumentar a confiabilidade e estabilidade dos sistemas.
- Fortalecer o alinhamento entre Dev e Ops.
- Criar um ambiente de aprendizado contínuo e inovação sustentável.

Esse plano oferece um caminho realista, incremental e centrado nas pessoas — o verdadeiro coração do DevOps.