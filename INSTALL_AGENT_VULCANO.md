# INSTALL_AGENT_VULCANO.md

Use este arquivo como instrução operacional para criar ou instalar um novo agent-vulcano.

## Objetivo

Criar um agente com workspace próprio, estrutura padronizada, skills locais, boot limpo e comportamento operacional consistente.

## Regra obrigatória de workspace

Todo novo agent-vulcano deve usar este padrão de diretório:

```text
/home/openclaw/.openclaw/vulcanos/workspace-NOME_DO_AGENTE
```

Nunca criar esses workspaces soltos na raiz de `.openclaw` quando o agente for um vulcano.

---

## Passo 1 — Definir o nome do agente

Escolher um nome de agente curto, claro e operacional.

Exemplo:
- `dev-backend`
- `laravel-senior`
- `content-research`

A partir disso, o workspace deve virar:

```text
/home/openclaw/.openclaw/vulcanos/workspace-NOME_DO_AGENTE
```

---

## Passo 2 — Criar a estrutura base

Criar no workspace:

```text
AGENTS.md
IDENTITY.md
PLAYBOOK.md
MEMORY.md
BOOTSTRAP.md
playbook/
memory/
```

Subpastas mínimas de `memory/`:

```text
memory/daily/
memory/projects/
memory/people/
memory/topics/
```

---

## Passo 3 — Escrever os arquivos base

### `AGENTS.md`
Deve:
- apontar a ordem de leitura;
- carregar `IDENTITY.md` antes de `PLAYBOOK.md`;
- carregar `MEMORY.md` apenas quando necessário;
- incluir `BOOTSTRAP.md` apenas enquanto ele existir.

### `IDENTITY.md`
Deve conter só o necessário:
- nome;
- papel;
- tom;
- estilo;
- postura.

Não transformar `IDENTITY.md` em lore longa.

### `PLAYBOOK.md`
Deve conter:
- papel operacional do agente;
- lista explícita das skills locais;
- regra de prioridade;
- regra de recusa;
- política de subagentes;
- política de subsessions;
- política de relatórios;
- política de erro/tentativas;
- política de sono/idle.

### `MEMORY.md`
Deve ser memória curada para continuidade.
Registrar:
- decisões;
- autores;
- conversas relevantes;
- estado de projeto;
- detalhes técnicos úteis;
- regras locais já definidas.

### `BOOTSTRAP.md`
Deve existir apenas para a primeira inicialização.
Ao concluir o bootstrap:
1. remover a instrução de leitura dele no `AGENTS.md`;
2. excluir o próprio `BOOTSTRAP.md`.

---

## Passo 4 — Adicionar skills locais

As skills do agente devem ficar locais, dentro de:

```text
playbook/
```

Elas não devem ser atualizadas automaticamente.
Só atualizar quando um humano pedir.

### Regra de uso de skill

```text
Se existe skill específica compatível → usar a específica
Se não existe skill específica → usar a skill ampla do domínio
Se a tarefa não se encaixa nas skills do agente → recusar com clareza
```

O agente não deve improvisar fora do domínio principal.

---

## Passo 5 — Configurar comportamento operacional

### Subagentes
- usar apenas quando houver ganho real de especialização;
- não abrir subagente por hábito;
- subagente opera como coordenador especializado.

### Subsessions
- todo trabalho pesado deve preferir subsessions;
- o agente principal e o subagente devem continuar livres para orquestração.

### Limites
- agente principal: até 2 subagentes;
- agente principal: até 5 subsessions;
- cada subagente: até 2 subsessions.

---

## Passo 6 — Configurar comportamento em canal

O agent-vulcano deve:
- responder apenas se for mencionado;
- evitar loop entre IAs;
- ser objetivo;
- pausar se houver impedimento insolúvel;
- dormir quando estiver idle.

### Regra de impedimento

Tentar resolver até 3 vezes.
Se não resolver:
- pausar;
- reportar ao responsável adequado ou a quem o acordou.

### Regra de reentrada

Se devolveu uma tarefa travada, só deve retomá-la quando o impedimento tiver sido resolvido.

---

## Passo 7 — Configurar formato de relatório

Todo relatório deve incluir:
- o que foi feito;
- estado atual;
- bloqueios;
- próximo passo;
- arquivos afetados;
- publicações feitas;
- tempo gasto detalhado.

### Tempo gasto obrigatório

Registrar:
- início geral;
- fim geral;
- duração geral;
- tempo por subagente;
- tempo por subsession;
- tempo das subsessions dos subagentes.

Usar sempre:
- `iniciado em`
- `finalizado em`
- `duração`

---

## Passo 8 — Validar o agente antes de considerar pronto

Conferir se:
- o workspace está em `/home/openclaw/.openclaw/vulcanos/`;
- os arquivos-base existem;
- o `PLAYBOOK.md` lista as skills explicitamente;
- o agente recusa o que está fora do escopo;
- o bootstrap é descartável;
- a memória está pronta;
- o agente está configurado para orquestrar, não para se prender em execução pesada.

---

## Resultado esperado

Ao final, o agent-vulcano deve nascer:
- focado;
- modular;
- com workspace organizado;
- com skills locais bem definidas;
- com boot limpo;
- com memória útil;
- com execução pesada isolada em subsessions;
- com comportamento previsível em canal.
