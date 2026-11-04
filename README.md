# GRADE HORÁRIA 2027 — DOCUMENTO DE CONTINUIDADE (v3)

> **Objetivo deste arquivo:** permitir que QUALQUER modelo/IA (ou pessoa) continue o projeto sem ler a conversa anterior. Ele é autossuficiente.
> **Última atualização:** 04/11/2026.

**REGRA ABSOLUTA:** responder SEMPRE e ÚNICAMENTE em **PORTUGUÊS** (nunca espanhol).

---

## 1. OBJETIVO

Montar a **grade de oficinas 2027** da escola **Verdescola**, **17 turmas ativas** (Infância e Adolescência), com **cores por eixo**, **ZERO conflitos de educador**, regra de **pares na Adolescência** (slots 2 e 3 iguais), e publicar numa **página interativa no GitHub Pages** (edição manual + geração + exportação Excel).

**Fonte oficial (mais recente):**
```
C:\Users\danid\Downloads\Horário_Grupos_Educadores_2027 _Rev3daniel.xlsx
```
(versão da coordenação, 30/10/2026 — substitui o `Horário_Grupos_Educadores_novo_2027.xlsx`).

---

## 2. EIXOS (CORES)

| Eixo | Cor | Oficinas |
|---|---|---|
| **Convivência** | verde `#73A186` | Corpo e movimento; Habilidades Motoras e Esportes; Semeando Valores; Jogos Estratégias e desafios |
| **Pertencimento** | azul `#8EAADB` | Expressão Artística e Comunitária; Território Meio Ambiente e Comunidade; Artes Plásticas; Inventar e Criar |
| **Ampliação de direitos** | amarelo `#FFC000` | Inglês e Novas Culturas; Língua Portuguesa; Matemática; Comunicação Expressão e participação – Fiscal do Sahy; Voz da vila |
| **Emancipação** | branco (na tabela: preto/`#FFFFE0`) | Canoagem; Construindo a própria trajetória; Cidadania e Participação no mundo digital; Xadrez/Projeto Maker; Ciências; HIST; GEO; PORT |

---

## 3. TURMAS ATIVAS (17)

- **Infância matutino:** G1-A, G1-B, G2-A, G2-B, G3-A
- **Infância vespertino:** G3-B, G4-A, G4-B, G5-A, G5-B
- **Adolescência matutino:** G8A, G8B, G9-A (1º semestre)
- **Adolescência vespertino:** G6-A, G6-B, G7-A, G7-B

**Descartados:** P. Infância (P1/P2 — não mexer), G9-A 2º semestre, bloco "LOCAL S 48", G3-B duplicada (linhas 60–66 da aba Infancia; a válida é 52–57).

**Educadores descartados p/ 2027:** Livia, Alessandra, Cenira, Marques, Renilson. Brena/Isadora ficam só na P. Infância.

---

## 4. REGRAS DE NEGÓCIO

1. **Multiset de oficinas por turma é IMUTÁVEL** — a quantidade de cada oficina na semana não muda (respeita o Rev3Daniel).
2. **Educador é FIXO por célula** — cada célula mantém o educador descrito no Rev3Daniel. **NUNCA trocar educador entre células/turmas.**
3. **Zero conflitos** — mesmo educador não pode estar em 2 turmas no mesmo horário sobreposto.
4. **Regra da Adolescência:** em cada dia, **slots 2 e 3 (8h40–9h30 + 9h50–11h00, ou 15h30–16h15 + 16h15–17h00) são a MESMA oficina com o MESMO educador** (par). O slot 1 é único. **G9-A SEX = exceção** (canoagem nos slots 1–2, outra oficina no slot 3).
5. **Como zerar conflitos:** apenas **REMOVER o educador** da célula em conflito (a oficina fica, sem educador, p/ escolha manual). Distribuir de forma **equilibrada entre gémeas** (G1-A/G1-B etc.).
6. **Meta = coluna OFICINA** da aba HORAS. **MULTI = horas livres** (substituição), separada da meta.
7. **Indisponibilidades:** DENNIS (não seg. manhã); MILENA (não sex. tarde nem seg. manhã); JULIA DUARTE (não sex.).
8. **Opcionais (sem meta):** MARIA, LETICIA REINA, CLEVERSON — aparecem no dropdown, não são sugeridos.
9. **Canoagem fixa na sexta:** G9-A e G7-A (só 1º semestre).
10. **Construindo a própria trajetória (Leticia)** saiu da grade no G9-A (SEG, para cumprir a regra de pares) mas **continua como opção no dropdown** de oficinas.

---

## 5. ARQUIVOS E ROTAS

**Pasta de trabalho:**
```
C:\Users\danid\AppData\Local\Temp\opencode\horario2027_v4\
```

| Arquivo | Função |
|---|---|
| `parse_rev3.py` | Lê o Rev3daniel → `grade2027.json` + `metas.json` + `diagnostico.txt` |
| `solver_final.py` | (v1) CP-SAT: 0 conflitos, remoção de educadores → `grade2027_resolvida.json` |
| `fazer_v2.py` | Corrige as 5 exceções da regra de pares na **base original** → `grade2027_resolvida_v2.json` (ainda com conflitos) |
| `fix_fiel.py` | **USADO HOJE:** parte da base original (`grade2027.json`), remove educadores em conflito de forma **equilibrada entre gémeas**, sem mexer em nada → **0 conflitos** → `grade2027_resolvida_v2.json` |
| `gen_html.py` | Gera `grade2027.html` (v1) |
| `gen_html_v2.py` | Gera `grade2027_v2.html` (v2, a versão atual) |
| `solver_v2_final.py` | (experimental, não usado) solver de unidades CP-SAT que quebrava a fidelidade — **NÃO USAR** |

**Entregas (abrir no navegador):**
```
C:\Users\danid\Downloads\grade2027.html      (v1)
C:\Users\danid\Downloads\grade2027_v2.html   (v2 — versão atual/principal)
```

**Pipeline (v2):**
```powershell
cd C:\Users\danid\AppData\Local\Temp\opencode\horario2027_v4
py -3 -X utf8 .\fazer_v2.py    # opcional: corrige exceções de pares na base
py -3 -X utf8 .\fix_fiel.py    # zera conflitos removendo educadores (equilibrado)
py -3 -X utf8 .\gen_html_v2.py # gera grade2027_v2.html
Copy-Item .\grade2027_v2.html C:\Users\danid\Downloads\grade2027_v2.html -Force
```

---

## 6. ESTADO ATUAL (04/11/2026)

**Grade v2 (`grade2027_resolvida_v2.json` + `grade2027_v2.html`):**
- **0 conflitos** ✅
- **Pares da Adolescência respeitados** (slots 2 e 3 iguais) ✅
- **Multiset de oficinas preservada** ✅
- **100% fiel ao Rev3Daniel** (nada embaralhado; educador fixo por célula) ✅
- **147 células com educador, 108 sem educador** (ficam para escolha manual).
- Distribuição equilibrada entre gémeas (ex.: G1-A 8 / G1-B 7; G4-A 8 / G4-B 7; G5-A 6 / G5-B 6; G8A 5 / G8B 5; G6-A 6 / G6-B 6).

**HTML interativo (v2):**
- Tabela por turma com **cores por eixo** e **dropdowns** de oficina (todas as opções, incl. "Construindo a própria trajetória") e de educador (todos).
- **Célula muda de cor** ao trocar a oficina.
- Painel de **conflitos** (tempo real) e **carga por educador** (real vs meta OFICINA + multi separado).
- Botões: **Gerar novo**, **Voltar ao anterior** (undo), **Restaurar** (grade default), **Exportar para Excel**.

**Exportação para Excel (v2) — 2 abas:**
- Aba **"Grade 2027"**: layout por turma (colunas largas: horário 90 / oficinas 160), cores por eixo, wrap text, **bordas em todas as células** (grossas no título/turmas, finas no resto), título verde.
- Aba **"Planejamento"**: mesmo layout da grade (Horário | Seg..Sex), mas **por educador** — mostra a oficina que dá (com turma e cor do eixo), **MULTI** (laranja, até a meta) e **PLANEJAMENTO** (cinza, até a meta) nos horários livres. Resumo por bloco: "Oficinas X/meta | Multi meta | Planejamento meta".

---

## 7. PENDÊNCIAS / PRÓXIMOS PASSOS

1. **GitHub Pages** (próximo passo): publicar `grade2027_v2.html` como `index.html` num repositório GitHub, ativar GitHub Pages, e a escola acessa o link. O HTML é **estático e autocontido** (dados + geração + edição + exportação em JS, sem servidor). Perguntar ao usuário: conta/repositório GitHub existente?
2. **Aba de oficinas multi** — o usuário mencionou que faria abas com as oficinas multi (contam no total, não aparecem na grade já tratadas na aba Planejamento).
3. **P. Infância** e **2º semestre**: fora desta etapa.

---

## 8. DECISÕES-CHAVE (contexto)

1. Fonte oficial = `Rev3daniel` (30/10).
2. Eixos por cor (verde/azul/amarelo/branco).
3. Educador **fixo** por célula (fiel ao arquivo); conflitos zerados só **removendo educador**.
4. Remoção **equilibrada entre gémeas** (não esvaziar uma turma só).
5. Regra de **pares na Adolescência** (slots 2 e 3 iguais); G9-A SEX (canoagem) é exceção.
6. Meta = OFICINA; MULTI = horas livres (separado).
7. Exportação com 2 abas: Grade + Planejamento (por educador), com cores/larguras/bordas.

---

## 9. AVISOS / ARMADILHAS

- **Nunca** alterar as abas do Excel; **nunca** inventar dados para pendências.
- **NÃO reembaralhar células com o solver** — quebra a fidelidade (educador trocado de turma) e os pares da Adolescência. A v2 deve partir da **base original** (`grade2027.json`) e apenas remover educadores em conflito (`fix_fiel.py`).
- **`solver_v2_final.py` e `solver_final.py` embaralham** — usar só se o objetivo for rearranjo livre (v1); **NÃO usar na v2**.
- Os scripts `_patch*.py` são patches aplicados ao `gen_html_v2.py` (exportação com estilos/2 abas); mantê-los por referência.
- No template do `gen_html.py`, usar `String.fromCharCode(10)` para quebra de linha em JS (evita problema de escape `\n` do Python).
- PowerShell adiciona **BOM** ao salvar com `Set-Content`/redirect (quebra `json.load`) — JSON via `.py` com `encoding='utf-8'` (corretos).
- Acentos aparecem quebrados no console do PowerShell (CP1252), mas os arquivos estão OK (UTF-8).
- Não expor tokens/segredos. O acesso Google **não** é usado neste fluxo.