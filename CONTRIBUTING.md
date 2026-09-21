# Como contribuir

Obrigado por melhorar a trilha. Há dois fluxos distintos: editar **conteúdo** e editar a **trilha**.

## Antes de começar

Leia o [CONTEXT.md](CONTEXT.md) — ele define a linguagem que usamos para falar do material (quadrante,
tipo de página, nível, papel, rascunho). Usar os mesmos termos evita metade das discussões de revisão.

## 1. Editar uma página de conteúdo

### Escolha o quadrante

Antes de escrever, responda: **o que a pessoa que abre esta página está tentando fazer?**

| Ela quer… | Quadrante | Pasta |
|---|---|---|
| aprender, sendo guiada do início ao fim | Tutorial | `docs/tutoriais/` |
| resolver uma tarefa específica | Guia | `docs/guias/` |
| consultar um fato enquanto trabalha | Referência | `docs/referencia/` |
| entender por que as coisas são assim | Explicação | `docs/explicacao/` |
| aplicar tudo em uma entrega | Desafio | `docs/desafios/` |
| comparar alternativas para decidir | Pesquisa | `docs/pesquisa/` |

Se a resposta for "as duas coisas", são **duas páginas**. Essa é a regra de ouro do Diátaxis e a fonte
mais comum de páginas ruins.

### Escreva

1. Copie o template correspondente de `templates/`.
2. Mantenha o cabeçalho `> Tipo: **X**` logo abaixo do título.
3. Termine com uma seção **Veja também** com links relativos para páginas relacionadas.

### Convenções

- **Português do Brasil**, com linguagem neutra quando não há pessoa específica ("quem constrói",
  "a pessoa", "a equipe").
- **Links relativos** entre páginas (`../referencia/glossario.md`) — o visualizador `doc.html`
  converte automaticamente.
- **Exemplos do setor público**: atendimentos, unidades, municípios, processos, demandas. Evite
  exemplos de e-commerce.
- **Tabelas** para comparações ("use X quando… / use Y quando…"). Elas são escaneáveis e é isso que
  quem consulta precisa.
- Uma página termina quando **responde à pergunta que a motivou** — não quando cobre o assunto inteiro.

### Páginas em rascunho

Uma página com o marcador `Rascunho — a escrever` tem esqueleto, mas não tem conteúdo. Ao escrevê-la:

1. Remova o marcador e o aviso sobre o documento-fonte.
2. Substitua todos os `_A definir._`.
3. Mantenha os títulos das seções — eles vêm do levantamento original e preservam o escopo acordado.

## 2. Editar a trilha

Edite **apenas** [ROADMAP.md](ROADMAP.md). Depois rode:

```bash
python3 tools/gen_roadmap.py
```

Isso regenera `roadmap.html`, `roadmap-dashboards.xmind`, `docs/trilhas/index.md` e a região de níveis
de `index.html`.

### Formato do item

```
- [tipo] **Título** — papel — `caminho/para/doc.md`
```

| Campo | Valores aceitos |
|---|---|
| tipo | `tutorial` `how-to` `reference` `explanation` `challenge` `research` |
| papel | `core` `support` `capstone` `optional` `advanced` |

O gerador **valida** esses valores e falha com mensagem clara. Ele também **cria um esqueleto** para
todo `.md` referenciado que não exista — então adicionar uma linha em `ROADMAP.md` e rodar o gerador é
a forma correta de criar uma página nova.

Caminhos repetidos são permitidos: vários nós podem apontar para o mesmo documento de propósito.

### Nunca edite à mão

- a região entre `<!-- ROADMAP:START -->` e `<!-- ROADMAP:END -->` em `roadmap.html`;
- a região entre `<!-- LEVELS:START -->` e `<!-- LEVELS:END -->` em `index.html`;
- `roadmap-dashboards.xmind`;
- `docs/trilhas/index.md`.

Tudo o mais em `roadmap.html` e `index.html` (design, CSS, JS) é seu.

## 3. Pré-visualizar

```bash
python3 -m http.server 8000
```

E abra <http://localhost:8000/>.

## 4. Decisões estruturais

Mudanças na forma como o material é organizado — não no conteúdo de uma página — vão para
`docs/adr/`, seguindo o formato de [ADR 0001](docs/adr/0001-mapeamento-diataxis-do-levantamento.md):
contexto, decisão, consequências, alternativas consideradas.

## 5. Commits

Prefixo por tipo de mudança:

```
docs: escreve a página de acessibilidade
trilha: move storytelling para o nível 2
tools: valida papéis duplicados no gerador
site: ajusta contraste da legenda no roadmap
```
