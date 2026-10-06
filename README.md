# R1 NO ALVO

App web (PWA) de estudo para a residência médica: **PlanejaMESTRE** (plano de estudos) e **MESTREstuda** (Grimório, Pergaminho, MESTREcards, MESTREquests e Caderno).

Este repositório contém a **versão compilada** (build do Vite + React), pronta para hospedar em qualquer servidor estático. Não precisa de `npm install` nem de build.

## Estrutura

```
.
├── index.html              # ponto de entrada
├── manifest.webmanifest    # PWA (nome, ícones, cores)
├── 404.html                # cópia do index (fallback de rota)
├── .nojekyll               # desliga o Jekyll no GitHub Pages
├── assets/                 # JS e CSS compilados (um arquivo por tela)
│   ├── index-*.js / .css   # núcleo do app e estilos
│   ├── Hoje, Planeja, Estuda, Grimorio, Pergaminho,
│   │   Cards, Quests, Caderno, Painel             # telas de estudo
│   └── Entrar, Cadastro, Verificar, Recuperar,
│       Conta, Legal, Layout, LeitorDoc, fluxo     # conta e utilitários
├── conteudo/
│   └── hda/                # tema: Hemorragia digestiva alta
│       ├── grimorio.html   # material completo
│       └── pergaminho.html # resumo
└── marca/                  # logo, ícones, ilustrações e capa OG
```

## Rodar localmente

```bash
npx serve .
# ou
python3 -m http.server 8080
```

Abra `http://localhost:8080`. (Abrir o `index.html` direto pelo explorador de arquivos não funciona, porque os módulos JS precisam de um servidor.)

## Publicar no GitHub Pages

1. Envie este conteúdo para a branch `main` de um repositório público.
2. No GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**.
3. Escolha **Branch: `main`** e pasta **`/ (root)`** e salve.
4. Em 1 a 2 minutos o site fica em `https://<seu-usuario>.github.io/<nome-do-repo>/`.

As rotas usam `#` (ex.: `#hoje`, `#cards`) e todos os caminhos são relativos (`./`), então o app funciona dentro da subpasta do GitHub Pages sem configuração extra.

## Adicionar um novo tema

Coloque o material em `conteudo/<slug>/grimorio.html` e `conteudo/<slug>/pergaminho.html`, seguindo o modelo de `conteudo/hda/`. Para o tema aparecer nas telas, os dados (unidades, cards, questões) precisam entrar no código do app, que hoje só traz o tema HDA.

## Observações importantes

- **Dados ficam no navegador.** Conta, plano, cards e progresso são salvos no `localStorage` de cada aparelho. Não há servidor nem banco de dados: limpar o navegador apaga o progresso, e não há sincronização entre aparelhos.
- **O login é só local.** Ele não protege nada de verdade. Para ter contas reais é preciso um backend (ex.: Supabase).
- **Sem código-fonte.** Os arquivos em `assets/` estão minificados. Para mudanças grandes, o ideal é recuperar ou recriar o projeto React original.
