# Self-host do GitHub Readme Stats

Este guia deixa o card de stats do perfil pronto para mostrar commits privados de forma confiável.

## Por que isso é necessário

O endpoint público `https://github-readme-stats.vercel.app/api` é mantido como serviço compartilhado e usa cache. Segundo a documentação oficial do projeto, ele é "best-effort" e as estatísticas privadas exigem uma instância própria com seu token.

No README atual, os parâmetros:

- `count_private=true`
- `include_all_commits=true`

já estão configurados, mas **isso sozinho não basta** no endpoint público.

## Caminho recomendado

Use uma instância própria do `github-readme-stats` no Vercel.

Repositório oficial:

- [anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats)

## Passo a passo

1. Faça um fork de `anuraghazra/github-readme-stats` para a sua conta.
2. Acesse o [Vercel](https://vercel.com/) e crie um novo projeto a partir desse fork.
3. Durante o deploy, adicione a variável de ambiente:
   - `PAT_1`
4. Crie um Personal Access Token no GitHub e use esse valor em `PAT_1`.

## Token recomendado

Para estatísticas privadas, o token precisa conseguir ler seus repositórios privados.

Na prática, o cenário mais compatível com o projeto costuma ser:

- token clássico com escopo `repo`

Se preferir testar com fine-grained token, ele precisa ter permissão de leitura suficiente para os repositórios que você quer contabilizar, mas a compatibilidade mais comum do projeto continua sendo com `repo`.

## Depois do deploy

Quando o Vercel gerar sua URL, troque no `README.md`:

De:

```md
https://github-readme-stats.vercel.app/api?username=nicolasagra-dev&show_icons=true&theme=tokyonight&hide_border=true&count_private=true&include_all_commits=true
```

Para algo como:

```md
https://SEU-PROJETO.vercel.app/api?username=nicolasagra-dev&show_icons=true&theme=tokyonight&hide_border=true&count_private=true&include_all_commits=true
```

E no card de linguagens:

De:

```md
https://github-readme-stats.vercel.app/api/top-langs/?username=nicolasagra-dev&layout=compact&theme=tokyonight&hide_border=true&langs_count=6
```

Para:

```md
https://SEU-PROJETO.vercel.app/api/top-langs/?username=nicolasagra-dev&layout=compact&theme=tokyonight&hide_border=true&langs_count=6
```

## O que muda quando estiver certo

- commits privados passam a contar com mais consistência
- o card deixa de depender do cache e da limitação da instância pública
- as estatísticas do seu perfil ficam mais fiéis ao seu uso real do GitHub

## Observação final

Mesmo em self-host, pode existir algum atraso por cache do próprio serviço, mas ele costuma ser bem mais confiável do que a instância pública.
