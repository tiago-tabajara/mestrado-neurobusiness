# SESSAO_CONTEXTO — Handoff do Site do Mestrado

**Projeto:** Master of Science in Neuroscience for Business  
**Domínio:** https://mestrado.infinityneuro.com  
**Repositório GitHub:** https://github.com/tiago-tabajara/mestrado-neurobusiness  
**Projeto Vercel:** `sitemestrado` (tiago-tabajaras-projects)  
**Arquivo principal:** `public/index.html`

---

## O que foi feito nesta sessão

### Novas seções adicionadas

#### BANCAS & DEFESAS (`#bancas`)
- Seção com 3 fotos do processo de defesa:
  - 1 foto hero grande: `images/defesa-apresentacao.png` — Karoline apresentando, legenda "Qualificação e Defesa presencial ou online"
  - 2 fotos menores lado a lado: `images/banca.png` (Banca examinadora) e `images/banca-online.png` (Qualificação híbrida), cada uma com legenda
- Título: "Ciência que se defende em público."
- Subtítulo sobre rigor acadêmico e banca examinadora
- Link de navegação adicionado no header

#### FORMANDOS (`#formandos`)
- Seção separada com 3 formandos nomeados e foto individual:
  - Suzete Álvares Leal → `images/suzete2.png`
  - Karoline Silveira → `images/defesa-karoline.png`
  - Márcio Harff → `images/defesa-marcio.png`
- Card dourado com: "A próxima foto de formatura pode ser a sua." + botão **Inscreva-se →**
- Link de navegação adicionado no header

### Alterações em seções existentes

| O que | Onde | Detalhe |
|-------|------|---------|
| Botão hero alterado | Hero | Texto: "Tire suas dúvidas com o coordenador" · Link: WhatsApp pessoal do coordenador `5551984244948` |
| WhatsApp dos demais botões | Nav, depoimentos, ingresso, CTA final, formandos | Novo número: `555141412090` |
| QR code e telefone removidos | Seção Formandos | Substituídos por botão "Inscreva-se →" |
| Foto da Suzete | Seção Formandos | Trocada de `defesa-suele.png` para `suzete2.png` |

### Imagens adicionadas em `public/images/`

| Arquivo | Conteúdo |
|---------|----------|
| `banca.png` | Banca examinadora presencial (3 professores com laptops) |
| `banca-online.png` | Banca híbrida — membro online via projetor + banner |
| `defesa-apresentacao.png` | Karoline apresentando dissertação ao vivo |
| `defesa-karoline.png` | Karoline Silveira com capelo e diploma |
| `defesa-marcio.png` | Márcio Harff com capelo e diploma |
| `defesa-suele.png` | Suzete com capelo e diploma (versão anterior) |
| `suzete2.png` | Suzete — foto nova usada atualmente |
| `qr-whatsapp.png` | QR code gerado (removido da UI, arquivo ainda existe) |

---

## Estrutura de WhatsApp no site

| Botão | Número | Destino |
|-------|--------|---------|
| "Tire suas dúvidas com o coordenador" (hero) | `5551984244948` | WhatsApp pessoal do Dr. Tiago |
| Nav "Tire suas dúvidas" | `555141412090` | WhatsApp da escola |
| "Quero participar" (depoimentos) | `555141412090` | WhatsApp da escola |
| "Inscreva-se →" (formandos) | `555141412090` | WhatsApp da escola |
| "Começar minha inscrição" (admissão) | `555141412090` | WhatsApp da escola |
| "Falar no WhatsApp" (CTA final) | `555141412090` | WhatsApp da escola |

---

## Pendências abertas

### 🔴 Crítico

- **Favicon não aparece em `mestrado.infinityneuro.com`** — O arquivo é servido corretamente (HTTP 200, conteúdo idêntico ao Vercel URL onde funciona). Causa raiz não identificada. O domínio usa CNAME via Wix DNS apontando para IP Vercel `76.76.21.21`. Hipóteses restantes: cache de favicon no browser específico do usuário, ou problema com a forma como o Wix redireciona subdomínios para Vercel.

### 🟡 Infraestrutura

- **Alias do domínio não segue deploys automáticos** — Cada deploy via CLI precisa de `vercel alias set <url> mestrado.infinityneuro.com` manual. O domínio foi adicionado ao projeto (`vercel domains add mestrado.infinityneuro.com sitemestrado`), mas o Vercel ainda não o reconhece como domínio primário de produção (pois o DNS não está configurado diretamente no Vercel — está via Wix). Solução definitiva: acessar o painel Wix e alterar o CNAME de `mestrado` para `cname.vercel-dns.com`, ou adicionar um registro A apontando para `76.76.21.21` com TTL baixo.

- **Comando para atualizar o domínio após cada deploy:**
  ```bash
  vercel --prod --yes && vercel alias set $(vercel ls --prod 2>&1 | grep "sitemestrado-" | grep -v "git-main" | head -1 | awk '{print $3}') mestrado.infinityneuro.com
  ```

### 🟢 SEO (aguardando revisão do usuário)

- Todos os elementos SEO foram listados (title, description, keywords, robots, author, canonical, OG, Twitter Card, JSON-LD com 4 entidades). Usuário solicitou a lista para análise — possíveis ajustes pendentes.

---

## Navegação atual do site (ordem)

1. O Programa (`#programa`)
2. Disciplinas (`#estrutura`)
3. Metodologia (`#metodologia`)
4. Docentes (`#docentes`)
5. Depoimentos (`#depoimentos`)
6. Bancas & Defesas (`#bancas`) ← novo
7. Formandos (`#formandos`) ← novo
8. FAQ (`#faq`)

---

## Ordem das seções na página

1. Hero (foto Tiago, botão WhatsApp coordenador)
2. Stats (+18 mil alunos, ~15 mil horas, Maior Referência)
3. O Programa
4. Coordenador (Dr. Tiago Tabajara, LinkedIn)
5. Diferenciais
6. Estrutura Curricular (13 disciplinas em accordion)
7. Metodologia de Ensino
8. Corpo Docente
9. Depoimentos
10. **Bancas & Defesas** ← novo
11. **Formandos** ← novo
12. Admissão
13. FAQ
14. CTA Final
15. Footer

---

## Deploy

- **Método:** `git push origin main` dispara deploy no Vercel via GitHub integration
- **Problema atual:** o alias do domínio personalizado precisa ser atualizado manualmente após cada deploy CLI
- **Último commit:** `1297765` — botão Inscreva-se na seção formandos
