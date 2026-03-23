# OpenClaw Agent-Vulcano

Guia base para criar agentes modulares, focados e observáveis no OpenClaw.

Este repositório documenta o padrão **agent-vulcano**: agentes com identidade mínima, cérebro operacional baseado em playbook, memória disciplinada, skills locais e execução pesada isolada em subsessions.

O objetivo é ter agentes que:
- não divaguem;
- não carreguem contexto desnecessário;
- trabalhem com escopo claro;
- saibam recusar o que está fora do domínio;
- consigam retomar trabalho antigo sem ficar burros;
- operem bem em canais reais como Telegram, Slack e Discord.

---

## Visão geral da arquitetura

Cada agent-vulcano deve ter sua própria estrutura local de workspace.

### Arquivos base do agente

- `AGENTS.md` → arquivo-raiz do boot
- `IDENTITY.md` → personalidade mínima e tom
- `PLAYBOOK.md` → cérebro operacional
- `MEMORY.md` + `memory/` → continuidade
- `BOOTSTRAP.md` → usado apenas na primeira inicialização
- `playbook/` → skills locais do agente

### Ordem de leitura

Fluxo normal:
1. `IDENTITY.md`
2. `PLAYBOOK.md`
3. `MEMORY.md` apenas quando necessário

Fluxo de primeira inicialização:
1. `BOOTSTRAP.md`
2. executar bootstrap
3. remover a leitura do `BOOTSTRAP.md` do `AGENTS.md`
4. excluir `BOOTSTRAP.md`
5. seguir fluxo normal

---

## Estrutura do workspace

Para manter a casa organizada, cada agent-vulcano deve usar este padrão:

```text
/home/openclaw/.openclaw/vulcanos/workspace-NOME_DO_AGENTE
```

Exemplos:

```text
/home/openclaw/.openclaw/vulcanos/workspace-dev-backend
/home/openclaw/.openclaw/vulcanos/workspace-laravel-senior
/home/openclaw/.openclaw/vulcanos/workspace-content-research
```

### Por que isso existe

- separa os workspaces dos vulcanos do resto da estrutura do OpenClaw;
- evita bagunça na raiz de `.openclaw`;
- facilita manutenção, backup e navegação;
- deixa claro quais pastas pertencem a agentes-vulcano.

---

## Modelo operacional

### Agente principal
- recebe a demanda;
- analisa o que precisa ser feito;
- escolhe skill;
- decide se precisa de subagente;
- orquestra execução;
- consolida relatório;
- volta a dormir quando não houver mais trabalho.

### Subagente
- entra apenas quando houver ganho real de especialização ou divisão inteligente de frente;
- não existe para duplicar trabalho à toa;
- também opera como coordenador.

### Subsession
- é onde o trabalho pesado acontece de verdade;
- agente e subagente devem permanecer livres para orquestração;
- execução longa ou complexa deve rodar em subsessions.

---

## Limites definidos

- agente principal pode abrir até **2 subagentes**;
- agente principal pode abrir até **5 subsessions**;
- cada subagente pode abrir até **2 subsessions**.

### Regra central

O agente e o subagente não devem ficar presos executando trabalho pesado diretamente.
Eles devem permanecer livres para coordenar, acompanhar estados, consolidar resultados e responder no canal.

---

## Quando usar subagente

Abrir subagente quando houver frentes inteligentes diferentes, por exemplo:
- front + back
- back + API
- código + pesquisa
- texto + execução
- arquitetura + implementação

Se não houver ganho claro de especialização ou alívio operacional, não abrir subagente.

---

## Skills e playbook

O `PLAYBOOK.md` é o cérebro operacional do agente.

Ele deve:
- listar explicitamente as skills locais do agente;
- definir prioridade entre skill específica e skill ampla;
- definir política de delegação;
- definir política de recusa;
- definir política de relatório;
- evitar que a IA precise varrer a pasta `playbook/` sem necessidade.

### Regra de prioridade

```text
Se existe skill específica compatível → usar a específica
Se não existe skill específica → usar a skill ampla do domínio
Se a tarefa não se encaixa nas skills do agente → recusar com clareza
```

### Regra de recusa

Se o agente não tiver habilidade para executar com maestria, ele deve recusar.
Exemplo: um agente com perfil `dev-backend` não deve aceitar uma tarefa de design visual só para tentar “dar conta”.

---

## Regras de comportamento em canal

- responder apenas se for mencionado/marcado;
- evitar loop entre IAs;
- ser objetivo;
- não ficar acordado sem necessidade;
- se estiver idle e sem pendência, voltar a dormir.

### Regra de impedimento

Se travar por qualquer motivo:
1. tentar resolver até **3 vezes**;
2. se não conseguir, pausar;
3. reportar ao responsável adequado ou a quem o acordou.

### Regra de reentrada

Se o agente devolveu uma tarefa travada por impedimento, ele só deve pegar novamente esse mesmo trabalho quando o impedimento tiver sido resolvido.
Isso evita loop no mesmo problema.

---

## Ciclo operacional

```text
acordar
→ analisar a tarefa / tirar dúvidas
→ escolher skill
→ decidir se precisa de subagente
→ abrir subsessions de execução
→ consolidar resultado
→ entregar relatório
→ verificar se há novo trabalho
→ se não houver, dormir
```

---

## Relatórios

Todo relatório do agent-vulcano deve incluir:

- o que foi feito;
- estado atual;
- bloqueios;
- próximo passo;
- arquivos afetados;
- publicações feitas;
- tempo gasto detalhado.

### Tempo gasto obrigatório

O tempo deve ser detalhado com:
- início geral;
- fim geral;
- duração geral;
- tempo de cada subagente;
- tempo de cada subsession;
- tempo das subsessions dos subagentes.

Formato esperado:
- `iniciado em`
- `finalizado em`
- `duração`

### Publicações

Se houve publicação ou envio externo, registrar também:
- repositório;
- blog;
- fórum;
- comunidade;
- documentação;
- qualquer outro destino relevante.

---

## Estrutura mínima sugerida de um workspace

```text
/home/openclaw/.openclaw/vulcanos/workspace-NOME_DO_AGENTE/
├── AGENTS.md
├── IDENTITY.md
├── PLAYBOOK.md
├── MEMORY.md
├── BOOTSTRAP.md
├── playbook/
│   ├── dev-backend.md
│   ├── laravel.md
│   └── ...
└── memory/
    ├── daily/
    ├── projects/
    ├── people/
    └── topics/
```

---

## Conteúdo deste repositório

- `README.md` → guia humano do padrão agent-vulcano
- `INSTALL_AGENT_VULCANO.md` → guia operacional para IA criar/instalar um agent-vulcano
- `templates/` → arquivos-base reutilizáveis

---

## Próximo uso esperado

Este repositório deve servir para:
- criar novos agents-vulcano;
- revisar agentes existentes;
- orientar outra IA a instalar/configurar um agente-vulcano;
- manter um padrão único de arquitetura e operação.
