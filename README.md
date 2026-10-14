# Termômetro de Segurança T2

Página de apuração do Termômetro de Segurança T2 (Demarco / Ambev): envio das bases do mês, cálculo dos 10 KPIs e ranking por CDD, regional e sócio operador, com visão do mês, do ano e o resumo.

## Como funciona

- `index.html` é a página inteira. Ela não depende de servidor: lê e grava os dados nesta mesma pasta do repositório.
- `data/` guarda os dados:
  - `index.json` lista os meses
  - `results/AAAA-MM.json` traz o resultado de cada mês
  - `inputs/AAAA-MM/` guarda as bases enviadas
  - `overrides/` guarda os valores manuais
  - `config/scoring.json` guarda os quartis
- **Ver o termômetro** não exige login nem token.
- **Enviar bases, recalcular, informar valor manual e editar quartis** exige um token do GitHub. A página grava tudo em **um único commit** por ação, então o histórico do Git mostra quem mudou o quê e quando, e qualquer envio pode ser desfeito revertendo o commit.

## Publicar (uma vez)

1. Crie um repositório e envie este conteúdo: `index.html`, `.nojekyll` e a pasta `data/`.
2. Em **Settings › Pages**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`.
3. Abra `https://<dono>.github.io/<repositório>/`. A página descobre o repositório pelo endereço. Se for publicar em outro endereço, preencha `owner` e `repo` em `window.TERMO_GITHUB`, no topo do `index.html`.

## Token de quem edita

Cada pessoa que envia bases cria o próprio token e informa na página, no botão **GitHub** (canto superior direito):

1. Acesse GitHub › **Settings › Developer settings › Personal access tokens › Fine-grained tokens › Generate new token**.
2. Em **Repository access**, escolha **Only select repositories** e marque só este repositório.
3. Em **Permissions › Repository permissions › Contents**, escolha **Read and write**. Não marque mais nada.
4. Defina uma validade (ex.: 90 dias) e copie o token.
5. Na página, clique em **GitHub**, cole o token e clique em **Salvar e conectar**.

O token fica salvo **apenas no navegador** de quem o informou. Ele não vai para o repositório nem para outras pessoas.

> **Nunca** coloque o token dentro do `index.html` nem em qualquer arquivo do repositório. Se o token estiver no código publicado, qualquer pessoa que abrir a página consegue copiá-lo e alterar ou apagar o repositório. Se isso acontecer por engano, revogue o token no GitHub na mesma hora.

## Rotina mensal

1. Na aba **Bases do mês**, escolha o mês no topo.
2. Clique em **Enviar bases do mês** e selecione **todos os arquivos de uma vez**. Podem ser os exports dos BIs (Excel ou CSV) ou as planilhas atuais de Termômetro, SIF Conversion e KPI Liderança.
3. O sistema identifica cada base pelas colunas e mostra o que achou. Confira, troque o que precisar e clique em **Salvar e calcular**. Tudo vai num único commit e o mês é publicado.

## Privacidade

As bases enviadas ficam no repositório e incluem nomes de colaboradores (por exemplo, quem realizou a Blitz) e números internos. Em repositório **público**, esses dados ficam visíveis para qualquer pessoa. Prefira um repositório **privado**. O GitHub Pages em repositório privado depende do plano: no GitHub Enterprise Cloud é possível restringir o acesso à página à organização. Nos outros planos, a página publicada fica pública mesmo com o repositório privado.
