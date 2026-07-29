# FUNNEL MÍDIA — Especificação de Landing Page

**Versão 1.0 · Julho de 2026**
Documento de handoff para designer e desenvolvedor. Contém copy final, estrutura, comportamento, requisitos técnicos e plano de medição.

---

# 0. Briefing técnico

| Item | Definição |
|---|---|
| **URL** | `funnelmidia.com.br` (raiz — é o site institucional e a LP ao mesmo tempo) |
| **Objetivo primário** | Solicitações de Diagnóstico Funnel qualificadas |
| **Objetivo secundário** | Captura de e-mail via material de conformidade OAB |
| **Métrica de sucesso** | ≥ 3% de conversão em formulário qualificado sobre visitantes de tráfego pago; ≥ 60% das solicitações dentro do ICP |
| **Persona** | Sócio de banca, 32–55 anos, decisor, cético, lê rápido, acessa 55–65% via mobile |
| **Tom** | Sóbrio, específico, numérico. Zero hype, zero emoji, zero exclamação. |
| **Idioma** | pt-BR |
| **Stack sugerida** | Next.js (App Router) + Tailwind + Vercel · alternativa no-code: Framer |
| **Peso alvo** | < 500 KB na primeira renderização |
| **Performance alvo** | LCP < 2.0s · CLS < 0.05 · INP < 200ms · Lighthouse mobile ≥ 92 |

### Princípio de design que governa tudo

> **Nota de cor:** todo texto em "Latão" citado neste documento (labels, numeração `01 —`, links de acento) deve usar **`#836230`** quando estiver sobre fundo Papel, e **`#B08D57`** quando estiver sobre fundo Tinta. Elementos gráficos (barras, réguas, bullets) usam `#B08D57` em qualquer fundo.

> **A página deve parecer que foi feita por um escritório, não por uma agência.**
> Fundo Papel `#F6F4EF`, muito espaço vazio, tipografia serifada em títulos, uma única cor de acento em latão, nada de gradiente, nada de ilustração 3D, nada de foto de banco de imagem com martelo. Se em algum momento a página parecer "vendedora", ela está errada.

### Decisões estratégicas de conversão

1. **Sem preço na página.** Preço público é sinal de commodity.
2. **CTA primário é um formulário de qualificação, não um link direto de agenda.** O atrito é intencional: filtra curioso e reforça escassez. Agenda só é liberada após qualificação.
3. **Prova social é anonimizada e de processo** (custo por reunião, tempo de resposta), nunca "aumentamos o faturamento em X%" com nome do advogado — isso exporia o cliente ao Provimento 205/2021. Ver seção 5 do documento de marca.
4. **A escassez é real e declarada:** dez contas ativas. Mostrar quantas vagas restam, e manter o número honesto.

---

# 1. Mapa da página

```
┌────────────────────────────────────────────────┐
│ 00  Nav (sticky, minimal)                      │
│ 01  Hero — promessa + CTA                      │
│ 02  Prova de credibilidade (faixa discreta)    │
│ 03  Diagnóstico do problema — "o que trava"    │
│ 04  Reposicionamento — as duas agências ruins  │
│ 05  O método: SINAL · CONFIANÇA · AGENDA       │
│ 06  O que entra (entregáveis, sem preço)       │
│ 07  Conformidade OAB (diferencial técnico)     │
│ 08  Casos anonimizados — métricas de processo  │
│ 09  Para quem é / para quem não é              │
│ 10  Como funciona (5 passos até começar)       │
│ 11  Sobre — quem opera a conta                 │
│ 12  FAQ / objeções                             │
│ 13  CTA final (fundo escuro)                   │
│ 14  Rodapé                                     │
│ ──  Formulário: página dedicada /diagnostico   │
│ ──  Obrigado: /diagnostico/recebido            │
└────────────────────────────────────────────────┘
```

**Grid base:** container 1200px, 12 colunas, gutter 24px, margem lateral mobile 20px.
**Ritmo vertical:** seções com `padding-block: 128px` desktop / `72px` mobile. Ritmo generoso é o que comunica premium.

---

# 2. Especificação seção a seção

---

## 00 — Navegação

**Comportamento:** transparente sobre o hero; ao rolar > 80px, ganha fundo `#F6F4EF` com 92% de opacidade, `backdrop-filter: blur(8px)` e borda inferior 1px em Névoa. Transição 200ms.

**Estrutura:** logo à esquerda (símbolo + wordmark FUNNEL) · links centralizados · CTA à direita.

**Links:** Método · Conformidade · Casos · Sobre
**CTA:** `Solicitar diagnóstico` — botão Tinta, texto Papel, `border-radius: 2px`, `padding: 12px 24px`.

**Mobile:** logo + botão CTA compacto ("Diagnóstico"). Sem hambúrguer — a página é linear, o menu não agrega. Se insistir em menu, use drawer full-screen em Tinta.

---

## 01 — Hero

**Layout:** coluna única, alinhado à esquerda, largura máxima do H1 de 16 colunas (~900px). Altura ~85vh, não 100vh — deixe a borda da próxima seção visível para induzir scroll.

```
─────────────────────────────────────────────
  ARQUITETURA DE AQUISIÇÃO PARA ADVOCACIA   ← label, Latão, 12px, uppercase, .12em

  Escritório cheio                          ← display 72px, Instrument Serif
  não é sorte.
  É processo.

  Desenhamos e operamos o caminho completo   ← body-lg 20px, Grafite, max 62ch
  entre quem procura um advogado e a reunião
  na sua sala. Dentro do que a OAB permite.

  [ Solicitar diagnóstico ]  Ver o método →   ← CTA primário + link texto

  ───────────────────────────────────────    ← régua 1px Névoa
  Máximo de 10 bancas atendidas por vez.      ← small 14px, Grafite
  3 vagas abertas para o próximo trimestre.
─────────────────────────────────────────────
```

**Copy final:**

- **Label:** `ARQUITETURA DE AQUISIÇÃO PARA ADVOCACIA`
- **H1:** `Escritório cheio não é sorte. É processo.`
  *(quebra de linha após "cheio" e após "sorte." — três linhas no desktop, controlar com `<br>` ou `text-wrap: balance`)*
- **Subtítulo:** `Desenhamos e operamos o caminho completo entre quem procura um advogado e a reunião na sua sala. Dentro do que a OAB permite.`
- **CTA primário:** `Solicitar diagnóstico`
- **CTA secundário (link, com seta):** `Ver o método`
- **Nota de escassez:** `Máximo de 10 bancas atendidas por vez. 3 vagas abertas para o próximo trimestre.`

**Notas de implementação:**
- O H1 usa Instrument Serif 400. A palavra `sorte.` pode receber itálico da mesma fonte — **uma única palavra**, mais que isso polui.
- Sem imagem no hero. O espaço vazio é o recurso visual. Se precisar de algo, use o símbolo das três barras em Névoa a 8% de opacidade, escala 600px, ancorado no canto inferior direito, sem interferir na leitura.
- A nota de escassez precisa ser verdadeira e atualizada manualmente. Se não vai manter, remova a segunda frase.

---

## 02 — Faixa de credibilidade

Faixa fina logo abaixo do hero, `padding-block: 32px`, borda superior e inferior 1px Névoa.

Três itens em linha, separados por divisor vertical, `label` em Grafite:

```
Atendemos bancas em 6 estados  │  Média de 5 meses de contrato ativo  │  100% das peças revisadas para conformidade
```

> ⚠️ **Substituir por números reais.** Se ainda não existem, corte a seção inteira. Número inventado em página institucional é passivo, não ativo.

---

## 03 — Diagnóstico do problema

**Objetivo:** o visitante precisa se ver na página nos primeiros 5 segundos desta seção. Antes de vender, nomear a dor.

**Layout:** título à esquerda (5 colunas), três blocos empilhados à direita (6 colunas), cada um numerado `01 —` em Latão.

```
01 — O PROBLEMA

Você não tem um             ┌──────────────────────────────────────┐
problema de                 │ 01 —                                 │
competência.                │ O mês é uma montanha-russa.          │
                            │ Tem mês que falta gente para atender │
Tem um problema de          │ e tem mês em que a agenda esvazia    │
distribuição.               │ sem explicação. Não porque o trabalho│
                            │ piorou, mas porque a entrada de novos│
                            │ clientes nunca foi um processo.      │
                            ├──────────────────────────────────────┤
                            │ 02 —                                 │
                            │ Você já pagou por marketing e não    │
                            │ sabe o que voltou. Relatório com     │
                            │ alcance, impressão e engajamento.    │
                            │ Nenhuma linha respondendo quantos    │
                            │ contratos entraram e a que custo.    │
                            ├──────────────────────────────────────┤
                            │ 03 —                                 │
                            │ E existe o medo justificado. Uma     │
                            │ peça mal escrita por uma agência que │
                            │ não conhece o Provimento 205 vira    │
                            │ representação na Ordem. O risco é    │
                            │ seu, não da agência.                 │
                            └──────────────────────────────────────┘
```

**Copy final:**
- **Label:** `01 — O PROBLEMA`
- **H2:** `Você não tem um problema de competência. Tem um problema de distribuição.`
- Blocos 01, 02 e 03 conforme o wireframe acima.

**Comportamento:** os três blocos entram com fade + translateY de 12px, escalonados em 80ms, ao cruzarem 60% da viewport. Respeitar `prefers-reduced-motion`.

---

## 04 — Reposicionamento

**Objetivo:** eliminar as alternativas antes de apresentar a solução. Esta é a seção que justifica o preço.

**Layout:** duas colunas iguais com um card cada, e uma linha de fecho em largura total abaixo.

```
02 — POR QUE NÃO FUNCIONOU

Existem dois tipos de agência. Nenhum dos dois resolve.

┌─────────────────────────────┐  ┌─────────────────────────────┐
│ A AGÊNCIA DE TRÁFEGO        │  │ A AGÊNCIA DE CONTEÚDO       │
│                             │  │                             │
│ Aplica o mesmo playbook de  │  │ Entende a Ordem, faz posts  │
│ loja virtual no seu escri-  │  │ sóbrios e bem escritos, e   │
│ tório. Entrega volume de    │  │ o perfil cresce. Mas não    │
│ contato, não capacidade de  │  │ existe nenhum mecanismo     │
│ pagamento. Sua equipe gasta │  │ ligando o seguidor à sala   │
│ o dia triando quem nunca ia │  │ de reunião. Autoridade sem  │
│ contratar.                  │  │ funil é vaidade paga.       │
└─────────────────────────────┘  └─────────────────────────────┘

──────────────────────────────────────────────────────────────
A Funnel opera as duas pontas e, principalmente, a que fica
no meio: o que acontece depois que a pessoa levanta a mão.
──────────────────────────────────────────────────────────────
```

**Copy final:**
- **Label:** `02 — POR QUE NÃO FUNCIONOU`
- **H2:** `Existem dois tipos de agência. Nenhum dos dois resolve.`
- **Card A — título:** `A AGÊNCIA DE TRÁFEGO` · corpo conforme wireframe
- **Card B — título:** `A AGÊNCIA DE CONTEÚDO` · corpo conforme wireframe
- **Fecho:** `A Funnel opera as duas pontas e, principalmente, a que fica no meio: o que acontece depois que a pessoa levanta a mão.`

**Visual:** cards em Branco puro sobre Papel, borda 1px Névoa, `border-radius: 2px`, `padding: 40px`. Sem ícone. Sem sombra colorida.

---

## 05 — O método (seção âncora `#metodo`)

**Objetivo:** é a seção mais importante da página. Transforma serviço em produto nomeado.

**Layout:** três blocos horizontais empilhados. Cada bloco: à esquerda a barra visual do estágio (larguras 100% / 62% / 33%, replicando o logo), no centro o nome e a explicação, à direita os entregáveis em lista.

```
03 — O MÉTODO

Três estágios. Nesta ordem.

████████████████████   SINAL          Entregáveis
                       Encontrar quem   ▪ Mapa de demanda da praça
                       já está procurando. ▪ Campanhas por intenção de busca
                                        ▪ SEO de fundo de funil
   A demanda jurídica raramente é       ▪ Google Business Profile
   criada. Ela é capturada. Alguém foi
   demitido, recebeu uma autuação,
   decidiu se divorciar. Começamos pela
   intenção que já existe — é mais
   barata e converte melhor.
────────────────────────────────────────────────────────────

████████████           CONFIANÇA      Entregáveis
                       Fazer ele        ▪ Landing page por área de atuação
                       escolher você.   ▪ Conteúdo educativo em conformidade
                                        ▪ Arquitetura de prova permitida
   Entre três advogados igualmente      ▪ Revisão de posicionamento técnico
   competentes, o cliente escolhe
   aquele em quem confia mais. Confiança
   não é sorte: é prova organizada no
   lugar certo, no momento da decisão.
────────────────────────────────────────────────────────────

██████                 AGENDA         Entregáveis
                       A parte que      ▪ CRM configurado e integrado
                       ninguém faz.     ▪ Roteiro de triagem e qualificação
                                        ▪ Cadência de follow-up automatizada
   Um contato não respondido em dez     ▪ Painel de reuniões e no-show
   minutos vale metade. Estruturamos
   o que acontece depois do formulário:
   quem responde, o que pergunta, o que
   faz quando não há resposta, e como
   isso vira número no fim do mês.
────────────────────────────────────────────────────────────
```

**Copy final:**
- **Label:** `03 — O MÉTODO`
- **H2:** `Três estágios. Nesta ordem.`
- **Estágio 1:** `SINAL` / `Encontrar quem já está procurando.` / corpo e entregáveis conforme wireframe
- **Estágio 2:** `CONFIANÇA` / `Fazer ele escolher você.` / idem
- **Estágio 3:** `AGENDA` / `A parte que ninguém faz.` / idem
- **Fecho da seção (destaque, Instrument Serif 36px, centralizado, largura 46ch):**
  `Agência nenhuma entrega cliente. Nós entregamos reunião com quem pode pagar. O contrato é com você.`

**Notas visuais:**
- As barras dos estágios usam Tinta nos dois primeiros e **Latão no terceiro** — coerente com o logo, e reforça que Agenda é o diferencial.
- No mobile, as barras viram um indicador fino de 4px acima do título do estágio, mantendo as proporções relativas.
- Opcional (bom investimento): as barras crescem da esquerda para a direita ao entrar na viewport, 600ms, `cubic-bezier(.2,.8,.2,1)`, escalonadas. Desabilitar com `prefers-reduced-motion`.

---

## 06 — O que entra

**Layout:** grid de 2 colunas × 4 linhas. Cada célula: título em Inter 600 + uma linha de descrição em Grafite. Divisores 1px em Névoa entre células (bordas internas apenas).

**Copy — 8 itens:**

| Item | Descrição |
|---|---|
| Estratégia de aquisição | Plano de 90 dias por área de atuação, com meta de custo por reunião. |
| Mídia paga | Google Ads e Meta operados por quem escreve a copy conhecendo o Provimento. |
| Páginas de conversão | Landing pages por especialidade, escritas e testadas por nós. |
| Conteúdo em conformidade | Pauta, roteiro e revisão ética de tudo que sai com o nome da banca. |
| CRM e automação | Configuração, integração e cadências de follow-up. |
| Playbook de atendimento | Roteiro de triagem e treinamento de quem atende o primeiro contato. |
| Revisão de conformidade | Toda peça passa por checagem contra o Provimento 205/2021 antes de subir. |
| Relatório de uma linha | O número que importa no topo. O detalhe fica abaixo, para quem quiser. |

- **Label:** `04 — O QUE ENTRA`
- **H2:** `Um sistema, não uma lista de serviços.`
- **Nota abaixo do grid (small, Grafite):** `Não vendemos serviços avulsos. O método só funciona inteiro.`

---

## 07 — Conformidade OAB

**Objetivo:** este é o fosso competitivo. Merece uma seção inteira e um tratamento visual distinto.

**Tratamento:** **seção em fundo escuro** — Tinta `#0E0E10`, texto Papel, acentos Latão. É uma das duas únicas seções escuras da página.

**Layout:** título e parágrafo à esquerda (5 colunas), tabela comparativa à direita (7 colunas).

```
05 — CONFORMIDADE

O Provimento 205 não        ┌──────────────────┬──────────────────┐
proíbe marketing.           │ VEDADO           │ PERMITIDO        │
Proíbe o marketing          ├──────────────────┼──────────────────┤
que a maioria das           │ Promessa de      │ Conteúdo         │
agências escreve            │ resultado        │ informativo      │
no piloto automático.       ├──────────────────┼──────────────────┤
                            │ Preço ou         │ Impulsionamento  │
A norma permite             │ condição de      │ com caráter      │
publicidade informativa     │ pagamento em     │ educativo        │
e até impulsionamento.      │ anúncio          │                  │
O que ela veda é promessa   ├──────────────────┼──────────────────┤
de resultado, preço em      │ Captação ativa   │ Anúncio por      │
anúncio, mercantilização    │ de clientela     │ intenção de      │
e captação ativa.           │                  │ busca            │
                            ├──────────────────┼──────────────────┤
Aqui, nenhuma peça sobe     │ "O melhor        │ Especialidade    │
sem passar por revisão —    │ advogado de..."  │ técnica e        │
e o critério fica visível   │                  │ atuação          │
para você.                  ├──────────────────┼──────────────────┤
                            │ Urgência         │ Sobriedade e     │
                            │ artificial       │ discrição        │
                            └──────────────────┴──────────────────┘

Fonte: Provimento 205/2021 do Conselho Federal da OAB. →
```

**Copy final:**
- **Label:** `05 — CONFORMIDADE` (em Latão)
- **H2:** `O Provimento 205 não proíbe marketing. Proíbe o marketing que a maioria das agências escreve no piloto automático.`
- **Corpo:** `A norma permite publicidade informativa e até impulsionamento em redes sociais. O que ela veda é promessa de resultado, preço em anúncio, mercantilização e captação ativa de clientela. Aqui, nenhuma peça sobe sem passar por revisão de conformidade — e o critério fica visível para você.`
- **Tabela:** duas colunas, `VEDADO` / `PERMITIDO`, cinco linhas conforme wireframe. Coluna VEDADO com texto em Grafite claro; PERMITIDO em Papel com um traço Latão de 12×2px como bullet.
- **Link de fonte (small, sublinhado, Latão):** `Fonte: Provimento 205/2021 do Conselho Federal da OAB` → `https://www.oab.org.br/leisnormas/legislacao/provimentos/205-2021` (`target="_blank" rel="noopener"`)
- **CTA secundário (lead magnet):** botão outline Papel — `Baixar o guia de conformidade em publicidade jurídica`

**Nota jurídica obrigatória, em `small` no rodapé da seção:**
`Esta tabela é um resumo didático e não substitui a leitura da norma nem orientação da seccional competente.`

---

## 08 — Casos anonimizados

**Objetivo:** provar sem expor o cliente a risco ético. Ver seção 1.9 do documento de marca.

**Layout:** três cards em linha (empilham no mobile). Cada card: descritor da banca em `label` + a métrica de processo em `metric` (56px) + uma linha de contexto.

```
06 — RESULTADOS DE PROCESSO

┌────────────────────┬────────────────────┬────────────────────┐
│ BANCA TRIBUTÁRIA   │ FAMÍLIA E SUCESSÕES│ EMPRESARIAL        │
│ 8 advogados · SP   │ 3 advogados · MG   │ 12 advogados · PR  │
│                    │                    │                    │
│ R$ 890 → R$ 310    │ 41h → 8min         │ 34% → 71%          │
│                    │                    │                    │
│ Custo por reunião  │ Tempo médio de     │ Comparecimento em  │
│ qualificada, em    │ primeira resposta  │ reuniões agendadas,│
│ 5 meses.           │ ao novo contato.   │ após novo roteiro. │
└────────────────────┴────────────────────┴────────────────────┘

Não publicamos nome de cliente nem resultado processual. O Provimento 205
vincula o advogado, e material identificado com números de resultado expõe
quem contratou — não quem produziu.
```

**Copy final:**
- **Label:** `06 — RESULTADOS DE PROCESSO`
- **H2:** `Medimos o que vira honorário.`
- Três cards conforme wireframe
- **Nota de rodapé (small, Grafite, largura total):** `Não publicamos nome de cliente nem resultado processual. O Provimento 205/2021 vincula o advogado, e material identificado com números de resultado expõe quem contratou — não quem produziu. Referências completas são apresentadas na reunião de diagnóstico.`

> ⚠️ **Os números acima são placeholders estruturais.** Substituir por dados reais antes de publicar. Se ainda não houver histórico, troque a seção por "Como medimos" e mostre o painel/relatório em vez do resultado — honesto e igualmente persuasivo.

**Visual da métrica:** Inter 600, 56px, `font-variant-numeric: tabular-nums`. O valor final (o melhor) em Verde sinal `#2E6F53`; a seta `→` em Latão.

---

## 09 — Para quem é / para quem não é

**Objetivo:** qualificação por auto-seleção. Dizer não publicamente é o gesto mais premium da página.

**Layout:** duas colunas. Esquerda em Papel; direita em Névoa com opacidade reduzida no texto.

```
07 — QUALIFICAÇÃO

FUNCIONA PARA                      NÃO FUNCIONA PARA

▪ Bancas de 2 a 15 advogados       ▪ Quem está começando e não tem
  com reputação já construída        caixa para sustentar 6 meses

▪ Ticket médio de honorário        ▪ Quem quer contratar tráfego ou
  acima de R$ 5 mil                  social media avulso

▪ Áreas empresarial, tributária,   ▪ Quem quer volume de lead a
  imobiliária, família de alto       qualquer custo
  padrão, previdenciária premium
                                   ▪ Quem não tem ninguém disponível
▪ Quem já contratou agência e        para responder um contato em
  quer entender por que não deu       até 10 minutos

▪ Quem trata marketing como        ▪ Quem negocia conformidade
  investimento com prazo, não
  como despesa mensal
```

- **Label:** `07 — QUALIFICAÇÃO`
- **H2:** `Não atendemos qualquer escritório.`
- **Fecho (body, centralizado, 52ch):** `Se você se reconheceu na coluna da direita, é melhor não conversarmos agora. Vale mais para os dois.`

---

## 10 — Como funciona

**Layout:** timeline horizontal no desktop (5 etapas), vertical no mobile. Cada etapa com número em Latão, título, uma linha de descrição e prazo.

| # | Etapa | Descrição | Prazo |
|---|---|---|---|
| 01 | Formulário | Você preenche a solicitação de diagnóstico. Leva 3 minutos. | — |
| 02 | Triagem | Avaliamos o encaixe e respondemos em até 1 dia útil. | 24h |
| 03 | Conversa | 45 minutos para entender a banca, o ticket e o gargalo. | Semana 1 |
| 04 | Diagnóstico | Auditoria dos canais, da conformidade e do custo atual de aquisição. | 10 a 15 dias |
| 05 | Plano | Você recebe um plano de 90 dias. É seu, com ou sem contrato. | — |

- **Label:** `08 — COMO COMEÇA`
- **H2:** `O primeiro passo é pago. E é seu de qualquer forma.`
- **Nota (small):** `O valor do diagnóstico é abatido integralmente do setup, caso a banca siga com a implantação.`

---

## 11 — Sobre

**Layout:** foto à esquerda (4 colunas), texto à direita (7 colunas).

- **Label:** `09 — QUEM OPERA`
- **H2:** `Você fala com quem executa.`
- **Corpo:** `Não temos camada de atendimento. A pessoa que apresenta a estratégia é a mesma que abre o gerenciador, escreve a copy e te liga quando um número desanda. É o motivo de atendermos no máximo dez bancas — e de não pretendermos crescer além disso.`
- Nome, cargo, e link do LinkedIn em `small`.

**Foto:** retrato em ambiente real, luz natural lateral, tratamento dessaturado e levemente quente, enquadramento médio, sem terno de banco de imagem, sem braços cruzados. Se não houver foto boa, **não use foto** — use o símbolo grande em Névoa. Foto ruim custa mais credibilidade do que ausência de foto.

---

## 12 — FAQ

Acordeão. Fechado por padrão, um aberto por vez. Ícone `+` / `−` em Latão, sem chevron. Borda 1px Névoa entre itens. Marcação semântica `<details>/<summary>` para acessibilidade nativa.

- **Label:** `10 — PERGUNTAS`
- **H2:** `O que costumam perguntar antes de contratar.`

**Itens (copy final):**

**1. Vocês garantem resultado?**
Não. Quem garante resultado em captação está vendendo risco. O que garantimos é processo: entregáveis definidos, prazo por etapa, e um número na mesa toda semana. Se em 90 dias o custo por reunião qualificada não tiver caído, essa conversa acontece por nossa iniciativa, antes de você precisar puxar.

**2. Isso é permitido pela OAB?**
Sim, dentro de limites claros. O Provimento 205/2021 permite publicidade informativa e impulsionamento, e veda promessa de resultado, preço em anúncio, mercantilização e captação ativa de clientela. Toda peça produzida aqui passa por revisão de conformidade antes de ir ao ar, e o critério de revisão fica documentado e disponível para você.

**3. Quanto custa?**
Depende da praça, do número de áreas e do estágio atual da estrutura. Não publicamos tabela porque não vendemos pacote. O diagnóstico é a única etapa com valor fixo, e ele é apresentado antes de qualquer proposta.

**4. Em quanto tempo aparece resultado?**
Os primeiros contatos qualificados costumam aparecer entre a terceira e a sexta semana. Contrato assinado depende do ciclo de decisão da sua área — em consumidor pode ser dias, em empresarial pode passar de três meses. Por isso o contrato mínimo é de seis meses: menos que isso não produz uma leitura confiável.

**5. Preciso aparecer em vídeo?**
Ajuda, mas não é obrigatório. Existem bancas operando bem com conteúdo escrito e páginas técnicas. Se você quiser aparecer, montamos a estrutura para isso. Se não quiser, montamos outra.

**6. Vocês atendem concorrentes na mesma cidade?**
Não. Exclusividade por área de atuação e por praça, prevista em contrato.

**7. E se eu já tiver agência?**
O diagnóstico funciona igual, e frequentemente é contratado exatamente nesse cenário. Auditamos o que está rodando e apontamos onde o dinheiro está vazando. Você decide o que fazer com a informação.

**8. Quem responde os contatos que chegam?**
Sua equipe. Nós montamos o roteiro, configuramos o CRM, automatizamos o follow-up e treinamos quem atende — mas o primeiro contato humano tem que ser da banca. Terceirizar isso quebra a confiança que construímos no estágio anterior.

---

## 13 — CTA final

**Tratamento:** fundo Tinta cheio, `padding-block: 160px`. Segunda e última seção escura.

```
                    ┌─────────┐
                    │   ▄▄▄   │      ← símbolo grande, 64px, Papel + Latão
                    └─────────┘

           Se a agenda do próximo trimestre
           não está resolvida, o momento de
                 desenhar é agora.

     Três minutos para preencher. Resposta em até um dia útil.

              [ Solicitar diagnóstico ]

           Máximo de 10 bancas. 3 vagas abertas.
```

- **H2 (Instrument Serif, 48px, Papel, centralizado, 24ch):** `Se a agenda do próximo trimestre não está resolvida, o momento de desenhar é agora.`
- **Subtítulo (body, Grafite claro):** `Três minutos para preencher. Resposta em até um dia útil.`
- **CTA (botão Papel, texto Tinta):** `Solicitar diagnóstico`
- **Nota (small, Latão):** `Máximo de 10 bancas atendidas por vez. 3 vagas abertas.`

---

## 14 — Rodapé

Fundo Tinta (continuação da seção anterior, separado por régua 1px em `rgba(246,244,239,.12)`). Três colunas + linha inferior.

- **Coluna 1:** lockup vertical + `Arquitetura de aquisição para advocacia.`
- **Coluna 2:** navegação — Método · Conformidade · Casos · Sobre · Diagnóstico
- **Coluna 3:** contato — e-mail, WhatsApp comercial, LinkedIn, Instagram
- **Linha inferior:** `© 2026 Funnel Mídia · CNPJ 00.000.000/0001-00 · Política de Privacidade · Termos de Uso`

**Aviso obrigatório (small, Grafite):**
`A Funnel Mídia é uma empresa de comunicação e marketing. Não presta serviços jurídicos e não é vinculada à Ordem dos Advogados do Brasil.`

---

# 3. Página de conversão — `/diagnostico`

Página separada, sem navegação e sem rodapé completo. Só logo, formulário e prova mínima. Zero saídas.

**Layout:** duas colunas. Esquerda (5 col): título, três bullets de reforço, uma métrica de caso. Direita (6 col): formulário em card Branco puro.

**Título:** `Solicitação de diagnóstico`
**Subtítulo:** `Avaliamos o encaixe antes de marcar conversa. Nem toda solicitação vira reunião — e tudo bem.`

### Campos

| # | Campo | Tipo | Obrigatório | Notas |
|---|---|---|---|---|
| 1 | Nome completo | texto | ✔ | |
| 2 | E-mail | e-mail | ✔ | validação de formato |
| 3 | WhatsApp | tel | ✔ | máscara `(00) 00000-0000` |
| 4 | Nome da banca | texto | ✔ | |
| 5 | Cidade / UF | texto | ✔ | |
| 6 | Site ou Instagram | url | ✖ | |
| 7 | Número de advogados | select | ✔ | `Só eu` · `2 a 5` · `6 a 15` · `16+` |
| 8 | Principal área de atuação | select | ✔ | Empresarial · Tributário · Trabalhista · Família e Sucessões · Imobiliário · Previdenciário · Criminal · Consumidor · Outra |
| 9 | Honorário médio por contrato | select | ✔ | `Até R$ 3 mil` · `R$ 3 a 10 mil` · `R$ 10 a 30 mil` · `Acima de R$ 30 mil` · `Prefiro não informar` |
| 10 | Investe em mídia paga hoje? | radio | ✔ | `Não` · `Sim, até R$ 3 mil/mês` · `Sim, R$ 3 a 10 mil/mês` · `Sim, acima de R$ 10 mil/mês` |
| 11 | Qual é o gargalo, na sua leitura? | textarea | ✔ | placeholder: `Ex.: chegam contatos, mas quase nenhum fecha.` · mín. 30 caracteres |
| 12 | Consentimento LGPD | checkbox | ✔ | ver texto abaixo |

**Campos ocultos:** `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content`, `gclid`, `fbclid`, `referrer`, `landing_page`, `timestamp`.

**Texto do consentimento (LGPD):**
`Autorizo a Funnel Mídia a tratar os dados acima para avaliação de encaixe e contato comercial, nos termos da Política de Privacidade. Posso solicitar exclusão a qualquer momento.`

**Botão:** `Enviar solicitação` — largura total, Tinta, texto Papel.

### Lógica de pontuação (qualificação automática)

Calcular no backend e gravar no CRM como `score`:

| Condição | Pontos |
|---|---|
| Advogados: 2–5 / 6–15 / 16+ | +2 / +3 / +2 |
| Honorário: R$ 3–10k / R$ 10–30k / > R$ 30k | +2 / +3 / +3 |
| Já investe em mídia paga | +2 |
| Área em empresarial, tributário, imobiliário ou família | +2 |
| Campo de gargalo com mais de 120 caracteres | +1 |
| Advogados = "Só eu" **e** honorário até R$ 3 mil | −4 |

**Roteamento:** `score ≥ 7` → alerta imediato no WhatsApp/Slack + prioridade de resposta. `score 4–6` → fila normal. `score < 4` → sequência de e-mail com conteúdo, sem reunião.

### Anti-spam
Honeypot invisível + `hCaptcha` invisível + rate limit por IP. **Não usar reCAPTCHA v2 com checkbox** — atrito desnecessário no público-alvo.

---

# 4. Página de agradecimento — `/diagnostico/recebido`

- **H1:** `Solicitação recebida.`
- **Corpo:** `Vamos avaliar o encaixe e responder em até um dia útil, no WhatsApp informado. Se houver encaixe, enviamos três horários para a conversa de 45 minutos.`
- **Enquanto isso (card):** link para o guia de conformidade em publicidade jurídica (PDF).
- Dispara o evento de conversão. `noindex`.

---

# 5. Requisitos técnicos

### Stack e infra
- **Recomendado:** Next.js 14+ (App Router), Tailwind, deploy na Vercel. Alternativa sem código: Framer (aceitável; perde controle fino de performance).
- Formulário: rota de API própria → CRM. **Não** usar embed de terceiro que injete iframe (destrói LCP e dificulta o tracking).
- Fontes: self-hosted em `woff2`, `font-display: swap`, `preload` apenas do peso usado no hero. Não carregar via `fonts.googleapis.com` — custa um DNS lookup no caminho crítico.

### Performance
- Imagens em AVIF com fallback WebP, `loading="lazy"` exceto acima da dobra, `width`/`height` sempre declarados.
- CSS crítico inline; resto adiado.
- Sem biblioteca de animação pesada. `IntersectionObserver` + transições CSS bastam.
- Scripts de terceiros (pixels) carregados após `load` ou via GTM com trigger de `Window Loaded`.

### Acessibilidade (WCAG 2.1 AA)
- Contraste mínimo 4.5:1 em texto corrido. **Atenção:** o Latão `#B08D57` sobre Papel dá apenas 2,8:1 e reprova. Sempre que o acento for **texto** sobre fundo claro (labels, links, numeração de seção), usar **Latão Texto `#836230`** (5,1:1). O `#B08D57` fica restrito a barras, réguas, bordas, ícones e a acentos sobre a Tinta (6,2:1).
- Foco visível: outline 2px Latão com offset 2px. Nunca `outline: none` sem substituto.
- Ordem de headings correta (um `<h1>`, hierarquia sem pulos).
- Acordeão com `<details>/<summary>` ou `aria-expanded` correto.
- Todos os inputs com `<label>` associado — placeholder não é label.
- `prefers-reduced-motion: reduce` desabilita todas as animações de entrada.
- Navegação completa por teclado, com skip link para o conteúdo.

### Responsividade
Breakpoints: `375` / `768` / `1024` / `1280` / `1536`.
Testar prioritariamente em iPhone 13/14 e Galaxy S21 — a maioria do tráfego entra por Instagram e Google no mobile.

### Conformidade e legal
- Política de Privacidade e Termos de Uso publicados (LGPD).
- Banner de cookies com consentimento granular; pixels só disparam após aceite (Consent Mode v2 no GTM).
- Aviso de não-vinculação com a OAB no rodapé (ver seção 14).
- Nenhuma afirmação de resultado sem lastro documental arquivado.

---

# 6. SEO

**Title (≤ 60 car.):**
`Funnel Mídia — Aquisição de clientes para advocacia`

**Meta description (≤ 155 car.):**
`Desenhamos e operamos o sistema que leva quem procura um advogado até a reunião na sua sala. Dentro do Provimento 205/2021 da OAB.`

**Estrutura de headings:** um `<h1>` (hero), `<h2>` por seção, `<h3>` em cards e itens de FAQ.

**Schema.org (JSON-LD):**
- `Organization` — nome, logo, sameAs (LinkedIn, Instagram), contato
- `Service` — `serviceType: "Marketing jurídico"`, `areaServed: "BR"`
- `FAQPage` — todos os 8 itens do acordeão, marcados
- `BreadcrumbList` na página de diagnóstico

**Open Graph / Twitter Card:** imagem 1200×630 em fundo Tinta com o lockup vertical em Papel e a tagline. Sem texto pequeno.

**Técnico:** `sitemap.xml`, `robots.txt`, canonical em todas as páginas, `noindex` em `/diagnostico/recebido`.

**Palavras-chave-alvo (secundárias, não forçar no texto):** marketing jurídico, captação de clientes advocacia, tráfego pago para advogados, marketing para escritório de advocacia, provimento 205 publicidade.

---

# 7. Medição

### Eventos (GA4 + Meta Pixel + Google Ads)

| Evento | Disparo | Prioridade |
|---|---|---|
| `view_hero` | carregamento | — |
| `scroll_50` / `scroll_90` | profundidade de rolagem | baixa |
| `cta_click` | qualquer clique em "Solicitar diagnóstico" (param: `location`) | média |
| `view_metodo` | seção Método 50% visível por 2s | média |
| `view_conformidade` | seção Conformidade 50% visível | média |
| `faq_open` | abertura de item (param: `question`) | baixa |
| `form_start` | primeiro campo focado | **alta** |
| `form_submit` | envio bem-sucedido | **conversão primária** |
| `lead_qualificado` | `form_submit` com `score ≥ 7` | **conversão de otimização** |
| `guia_download` | download do PDF de conformidade | conversão secundária |

### Configuração
- **Otimizar campanhas por `lead_qualificado`**, não por `form_submit`. Isso é o que impede o algoritmo de trazer volume ruim — e é literalmente o argumento que a página vende.
- Conversão offline: enviar de volta ao Google Ads e ao Meta os leads que viraram reunião realizada e contrato assinado (Enhanced Conversions / CAPI). Fecha o ciclo e melhora a otimização em 60–90 dias.
- Server-side tagging via GTM quando o volume justificar.
- Microsoft Clarity ou Hotjar nos primeiros 90 dias para mapas de calor e gravações. Desligar depois.

### Testes A/B em ordem de prioridade
1. H1 do hero: `Escritório cheio não é sorte. É processo.` **vs.** `Você não tem problema de competência. Tem problema de distribuição.`
2. CTA: `Solicitar diagnóstico` **vs.** `Ver se há encaixe`
3. Nota de escassez presente **vs.** ausente
4. Formulário de 12 campos **vs.** versão curta de 6 campos com qualificação na conversa

Só rodar teste com **mínimo de 100 conversões por variante**. Abaixo disso o resultado é ruído — não decida com base nele.

---

# 8. Checklist antes de publicar

- [ ] Todos os números placeholder substituídos por dados reais (seções 02 e 08)
- [ ] Contagem de vagas conferida e com responsável por atualizar
- [ ] Política de Privacidade e Termos publicados
- [ ] Aviso de não-vinculação com a OAB no rodapé
- [ ] Consentimento LGPD no formulário
- [ ] Banner de cookies com Consent Mode v2
- [ ] Formulário testado ponta a ponta até o CRM
- [ ] Alerta de lead com score alto chegando no WhatsApp/Slack
- [ ] Lighthouse mobile ≥ 92 em performance e ≥ 95 em acessibilidade
- [ ] Teste com leitor de tela na navegação e no formulário
- [ ] OG image renderizando corretamente no WhatsApp e no LinkedIn
- [ ] 404 personalizada
- [ ] E-mail de resposta automática configurado
- [ ] Revisão de texto por terceiro — erro de português nesta página custa caro com este público

---

## Fontes

- [Provimento 205/2021 da OAB sobre publicidade — Conselho Federal da OAB](https://www.oab.org.br/leisnormas/legislacao/provimentos/205-2021)
- [Provimento 205/2021 da OAB e novas regras de marketing jurídico — Projuris](https://www.projuris.com.br/blog/provimento-205-2021/)
- [Publicidade na Advocacia 2025: OAB, Marketing Jurídico e Limites — Rockham](https://rockham.com.br/publicidade-na-advocacia/)
- [Marketing para Advogados: OAB, tráfego pago e SEO — AmdJus](https://amdjus.com.br/marketing-para-advogados-oab-trafego-pago-e-seo/)
