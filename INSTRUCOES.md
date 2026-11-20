# Integração — Consciência Negra | Escola Estadual Nova Aparecida

Este pacote contém:
- `index.html`: site público para GitHub Pages.
- `Code.gs`: API de leitura do Google Planilhas via Apps Script.
- `modelo_planilha.xlsx`: modelo com as quatro abas e exemplos.
- `INSTRUCOES.md`: guia de configuração.

## Visão geral

O site consulta o Apps Script a cada 30 segundos. O Apps Script lê as abas da planilha e devolve apenas os registros ativos. O site mostra títulos, descrições, imagens e players de vídeo; não mostra o endereço dos arquivos.

## Passo 1 — Criar a planilha Google

1. Envie `modelo_planilha.xlsx` ao Google Drive.
2. Abra o arquivo com o Google Planilhas.
3. Selecione **Arquivo > Salvar como Planilhas Google**.
4. Confira se as abas têm estes nomes exatos:
   - `Apresentacoes`
   - `Fotografias`
   - `Entrevistas`
   - `Creditos`
5. Apague ou substitua as linhas de exemplo. Não altere os nomes das colunas da primeira linha.

## Passo 2 — Preparar os arquivos no Drive

1. Crie uma pasta para as mídias do projeto.
2. Envie fotos e vídeos.
3. Para cada arquivo que será exibido no site, configure **Acesso geral > Qualquer pessoa com o link > Leitor**.
4. Copie o link de compartilhamento e cole na coluna `link` da aba correspondente.
5. Não coloque informações privadas na planilha: o conteúdo das abas é disponibilizado publicamente pelo site.

Fotos são exibidas como miniaturas do Drive. Vídeos do Drive são exibidos no player incorporado do Google Drive. Links de vídeos do YouTube também são aceitos na coluna `link` de Apresentacoes ou Entrevistas.

## Passo 3 — Criar o Apps Script

1. Abra a planilha Google.
2. Vá em **Extensões > Apps Script**.
3. Apague o conteúdo inicial e cole o conteúdo de `Code.gs`.
4. Salve.
5. No seletor de funções, escolha `prepararPlanilha` e clique em **Executar**. Autorize o acesso solicitado. A função cria as abas que faltarem e não apaga registros existentes.
6. Clique em **Implantar > Nova implantação**.
7. Tipo: **Aplicativo da Web**.
8. Executar como: **Eu** (sua conta).
9. Quem pode acessar: **Qualquer pessoa**.
10. Clique em **Implantar**, autorize se solicitado e copie a URL terminada em `/exec`.

A opção “Qualquer pessoa” é necessária para o site público consultar a API. A planilha em si pode continuar compartilhada apenas com os editores. Não compartilhe o acesso de edição da planilha publicamente.

## Passo 4 — Ligar o site à planilha

1. Abra `index.html` em um editor de texto.
2. Procure esta linha:
   `const API_URL = "COLE_AQUI_A_URL_DO_APPS_SCRIPT";`
3. Substitua o texto entre aspas pela URL `/exec` copiada no passo anterior.
4. Salve o arquivo.

## Passo 5 — Publicar no GitHub Pages

1. Entre no GitHub e crie um repositório, por exemplo `consciencia-negra`.
2. Envie o arquivo `index.html` para a raiz do repositório.
3. Abra **Settings > Pages**.
4. Em Build and deployment, escolha **Deploy from a branch**.
5. Selecione a branch `main` e a pasta `/ (root)`, depois clique em **Save**.
6. Aguarde a publicação. O GitHub mostrará o endereço público do site.

## Como cadastrar conteúdo

### Apresentacoes
- `titulo`: nome da apresentação.
- `descricao`: texto curto que aparece abaixo do título.
- `link`: link de compartilhamento do arquivo no Drive ou URL de vídeo do YouTube.
- `tipo`: escreva `video` ou `foto`.
- `ativo`: `sim` para exibir; `nao` para ocultar.

### Fotografias
- `titulo`, `descricao`, `link`, `ativo`.
- A coluna `link` deve apontar para uma imagem acessível publicamente.

### Entrevistas
- `titulo`: tema ou nome da pessoa entrevistada.
- `descricao`: breve contexto.
- `link`: link do vídeo no Drive ou YouTube.
- `ativo`: `sim` ou `nao`.

### Creditos
- `aluno`: nome do estudante.
- `funcao`: atividade principal (ex.: Fotografia, Roteiro, Edição).
- `descricao`: detalhe da contribuição.
- `ativo`: `sim` ou `nao`.

Para retirar um item do site sem apagar a linha, mude `ativo` para `nao`. As alterações aparecem na próxima consulta (em até cerca de 30 segundos).

## Observações importantes

- O site não exibe links como texto, mas o vídeo/imagem precisa de uma URL para carregar. O navegador poderá revelar o endereço técnico nas ferramentas de desenvolvedor; não existe forma de ocultar totalmente uma URL usada pelo navegador.
- O Google Drive pode impor limites de visualização e não é um serviço de streaming. Para vídeos longos ou muitas visualizações, considere YouTube com vídeo “Não listado” ou uma hospedagem de vídeo apropriada.
- Teste os links em uma janela anônima antes de publicar.
- Não publique imagens ou entrevistas sem as autorizações necessárias, especialmente quando houver estudantes menores de idade.
- Se alterar o código do Apps Script depois da implantação, atualize a implantação existente para usar a nova versão.
