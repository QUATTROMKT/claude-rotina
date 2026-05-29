# APEX Growth & Strategy — Automação Daily → Asana

## Regras invioláveis de atribuição
- **NUNCA** atribuir tasks à conta "Apex Growth & Strategy" (`contato@apex-growth.org`) — é conta mãe, só para controle
- Quando a transcrição citar "Apex Growth & Strategy" como responsável → atribuir ao **Cadu**
- Toda task obrigatoriamente vai para **Letícia**, **João** ou **Cadu**

## Usuários do Asana
| Nome | Email | GID |
|------|-------|-----|
| Cadu (Carlos Eduardo Braga) | cadubraga99@gmail.com | `1213891491411634` |
| João Kupke | joaolsk@hotmail.com | `1206635000245457` |
| Letícia Peripolli | peripollileticia@gmail.com | `1214312702976488` |
| ⚠️ Apex G&S (NÃO USAR como assignee) | contato@apex-growth.org | `1213891612678765` |

## Projeto principal
| Projeto | GID |
|---------|-----|
| Produção | `1213891606083089` |

## Clientes ativos
| Nome na daily | Nome no Asana | GID da opção |
|---------------|---------------|-------------|
| Atlanta | Atlanta | `1213891491411550` |
| Cober / Kobber SM | Kobber SM | `1213891491411547` |
| Kobber CWB | Kobber CWB | `1213891491411548` |
| Game Center | Game Center | `1214558522521134` |
| Chris Tattoo / Chris Bevilaqua | Chris Tattoo | `1214584924397287` |
| Clínica Gil / Gi Togni / Giovanna Togni | Gi Togni | `1214584924397288` |
| APEX / Apex Clinic (interno) | APEX | `1213891491411551` |

---

## Campos customizados — GIDs e opções

### 🔥 PRIORIDADE — `1213891606083094` (enum)
| Valor | GID |
|-------|-----|
| Baixa | `1213891606083095` |
| Média | `1213891606083096` |
| Alta  | `1213891606083097` |

### ⚠️ STATUS — `1213891606083099` (enum)
| Valor | GID |
|-------|-----|
| Em dia    | `1213891606083100` |
| Em risco  | `1213891606083101` |
| Em atraso | `1213891606083102` |

### 🏢 CLIENTE — `1213891491411546` (enum)
Ver tabela de clientes ativos acima.

### 📌 TIPO DA TAREFA — `1213891491411554` (multi_enum → array)
| Tipo | GID |
|------|-----|
| 🎨 Criativo | `1213891491411555` |
| ✍️ Copy / Roteiro | `1213891491411556` |
| 📱 Conteúdo Orgânico | `1213891491411557` |
| 📢 Campanha (Tráfego) | `1213891491411561` |
| 📊 Análise / Monitoramento | `1213891491411583` |
| 📈 Otimização | `1213891491411584` |
| 🧠 Estratégia | `1213891491411585` |
| 🤝 Atendimento / Cliente | `1213891491411586` |
| 📅 Agendamento / Publicação | `1213891491411587` |
| 📦 Operacional | `1213891491411588` |

### 🎯 OBJETIVO — `1213894067841069` (multi_enum → array)
| Objetivo | GID |
|---------|-----|
| Venda | `1213894067841070` |
| Lead | `1213894067841071` |
| Engajamento | `1213894067841072` |
| Alcance | `1213894067841073` |
| Branding | `1213894067841074` |
| Tráfego | `1213891491411577` |

### 📍 PLATAFORMA — `1213893985260918` (multi_enum → array)
| Plataforma | GID |
|-----------|-----|
| Instagram | `1213893985260919` |
| Facebook Ads | `1213893985260920` |
| Google Ads | `1213893985260921` |
| TikTok | `1213893985260922` |
| WhatsApp | `1213893985260923` |
| Outros | `1213893985260924` |

### 📊 MÉTRICA PRINCIPAL — `1213891491411569` (text)
Preencher apenas em tasks de campanha (tráfego pago). Exemplos: `CPA ≤ R$20`, `CTR ≥ 2%`, `ROAS ≥ 2`, `CPL ≤ R$15`.

### 🚧 GARGALO / BLOQUEIO — `1213894254139832` (multi_enum → array)
| Gargalo | GID |
|---------|-----|
| Aguardando cliente | `1213894254139833` |
| Falta material | `1213894254139834` |
| Aguardando aprovação | `1213894254139835` |
| Dependência interna | `1213891491411582` |

---

## Padrão de criação de tasks no Asana

### Título
```
[CLIENTE] - [Descrição da ação]
```
Exemplos: `ATLANTA - Finalizar Cards de Feed`, `KOBBER SM - Publicar Vídeo Concurso do Boné`

### Campos customizados (sempre via `custom_fields`)
Preencher diretamente nos campos do Asana — **nunca repetir na descrição**:
- `PRIORIDADE` → GID da opção (string)
- `STATUS` → GID da opção (string) — tasks novas sempre iniciam como "Em dia"
- `CLIENTE` → GID da opção (string)
- `TIPO` → array de GIDs (multi_enum)
- `OBJETIVO` → array de GIDs (multi_enum)
- `PLATAFORMA` → array de GIDs (multi_enum) — omitir se não aplicável
- `MÉTRICA` → string de texto — apenas para campanhas de tráfego
- `GARGALO` → array de GIDs (multi_enum) — apenas se houver bloqueio

### Descrição (notes)
Apenas o contexto da daily, sem repetir os campos:
```
📝 CONTEXTO DA DAILY:
[resumo do que foi dito sobre essa tarefa na call]
```

### Exemplo de task completa (create_tasks)
```json
{
  "name": "ATLANTA - Criar Criativos para Anúncios",
  "assignee": "1214312702976488",
  "due_on": "2026-05-30",
  "project_id": "1213891606083089",
  "notes": "📝 CONTEXTO DA DAILY:\nCriar cards estáticos com preço e comodidades para anúncios pagos. Fundo de funil. Enviar para aprovação do João.",
  "custom_fields": {
    "1213891606083094": "1213891606083097",
    "1213891606083099": "1213891606083100",
    "1213891491411546": "1213891491411550",
    "1213891491411554": ["1213891491411555"],
    "1213894067841069": ["1213894067841071"],
    "1213893985260918": ["1213893985260920"],
    "1213891491411569": "CPL (definir meta)"
  }
}
```
