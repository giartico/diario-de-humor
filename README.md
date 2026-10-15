# Diário de Humor

Aplicativo web para registrar o humor e os sentimentos ao longo do dia e acompanhar a evolução em um relatório com gráficos, PDF e exportação de dados.

É uma página web que pode ser adicionada à tela de início do iPhone e usada como um aplicativo. Todos os dados ficam guardados no próprio aparelho.

-----

## Sumário

1. [Funcionalidades](#funcionalidades)
1. [Arquivos do projeto](#arquivos-do-projeto)
1. [Como usar](#como-usar)
1. [Onde os dados ficam guardados](#onde-os-dados-ficam-guardados)
1. [Backup criptografado](#backup-criptografado)
1. [Publicar gratuitamente (GitHub Pages)](#publicar-gratuitamente-github-pages)
1. [Adicionar à tela de início do iPhone](#adicionar-à-tela-de-início-do-iphone)
1. [Atualizar o aplicativo](#atualizar-o-aplicativo)
1. [Privacidade e segurança](#privacidade-e-segurança)
1. [Limitações conhecidas](#limitações-conhecidas)
1. [Para quem quiser mexer no código](#para-quem-quiser-mexer-no-código)

-----

## Funcionalidades

### Registrar

- **Humor do momento**, em 5 opções: Muito bem, Bem, Neutro, Mal e Muito mal.
- **Sentimentos** (seleção múltipla): Medo, Ansiedade, Alegria, Tristeza, Raiva, Esperança, Vergonha, Frustração, Angústia, Confiança, Solidão, Culpa, Insegurança, Gratidão, Desânimo e Entusiasmo.
- **Sentimentos personalizados:** é possível criar novos sentimentos pelo campo “Outro sentimento”. Eles ficam salvos e podem ser removidos da lista a qualquer momento (os registros antigos mantêm o nome).
- **Comentário opcional.**
- **Data e hora do registro:** por padrão usa o momento em que você toca em Salvar. É possível escolher outra data e hora para fazer um registro retroativo. Não é permitido escolher um momento no futuro.
- Vários registros no mesmo dia são permitidos.

### Histórico

- Lista de todos os registros, agrupados por dia.
- Botão para alternar a ordem por data: **crescente** (mais antigos primeiro) ou **decrescente** (mais recentes primeiro).
- **Editar:** abre o formulário já preenchido (humor, sentimentos, comentário, data e hora). Ao salvar, o registro é atualizado, sem criar um novo.
- **Apagar:** exige um segundo toque para confirmar.

### Relatório

- **Filtro de período:** Hoje, Últimos 7 dias, Últimos 30 dias, Todo o período ou Personalizado (datas “De” e “Até”). Tudo no relatório respeita o período escolhido.
- **Contagem** total de avaliações e por humor.
- **Gráfico de barras** com a quantidade de cada humor.
- **Gráfico de linha (evolução do humor):** uma linha única numa escala de 1 a 5, para ver a tendência.
  - 1 = Muito mal, 2 = Mal, 3 = Neutro, 4 = Bem, 5 = Muito bem.
  - Cada registro é um ponto, posicionado pela sua data e hora, com a cor do humor.
  - Mostra a **média do período**.
  - Quando o período é de um único dia, o eixo horizontal mostra as horas.
- **Gráfico de sentimentos** com o total de cada sentimento no período, do mais frequente ao menos frequente (inclui os personalizados).
- **Comentários** em uma lista única, sempre em ordem de data (do mais antigo ao mais recente). Cada comentário mostra o emoji e o nome do humor, a data e hora, os sentimentos marcados e uma linha vertical na cor do humor.
- **Exportar PDF** do relatório.
- **Exportar CSV** dos registros do período.
- **Backup criptografado** (veja a seção própria).

-----

## Arquivos do projeto

|Arquivo               |Para que serve                                                                                                                                                           |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`index.html`          |O aplicativo completo (HTML, CSS e JavaScript em um único arquivo). Na versão de trabalho ele se chama `diario-de-humor.html`; para publicar, renomeie para `index.html`.|
|`apple-touch-icon.png`|Ícone de 180 x 180 pixels usado no atalho da tela de início do iPhone. Deve ficar na mesma pasta do `index.html`, com este nome exato.                                   |
|`README.md`           |Este documento.                                                                                                                                                          |

O aplicativo não depende de nenhuma biblioteca externa nem de internet para funcionar depois de carregado.

-----

## Como usar

1. **Registrar:** na aba *Registrar*, escolha o humor, marque os sentimentos, escreva um comentário se quiser e toque em **Salvar registro**.
1. **Registro retroativo:** antes de salvar, altere o campo *Data e hora do registro*. O botão **Agora** volta para o momento atual.
1. **Consultar:** na aba *Histórico*, veja, edite ou apague registros.
1. **Analisar:** na aba *Relatório*, escolha o período e veja os gráficos e os comentários.
1. **Gerar PDF:** no fim do Relatório, toque em **Gerar PDF do relatório**. Abre a folha de compartilhar do iPhone, onde você pode salvar em *Arquivos* ou enviar por WhatsApp, e-mail etc.
1. **Exportar CSV:** toque em **Exportar CSV**. O arquivo usa ponto e vírgula como separador e codificação UTF-8 com marcador de ordem de bytes (BOM), para abrir direto no Excel, Numbers ou Planilhas, com os acentos corretos.

### Conteúdo do PDF

Páginas em tamanho A4, numeradas, com: período e data de geração, total de avaliações, contagem por humor, gráfico de barras, gráfico de tendência com a média, gráfico de sentimentos e a lista de comentários em ordem de data. Como o PDF não tem fonte de emojis, cada comentário traz uma carinha desenhada na cor do humor, junto do nome do humor, no lugar do emoji.

### Colunas do CSV

`Data;Hora;Humor;Sentimentos;Comentário`, com os registros do período escolhido em ordem de data crescente.

-----

## Onde os dados ficam guardados

Os registros **não vão para nenhum servidor**. Ficam no próprio aparelho, e o aplicativo mostra, abaixo do botão de salvar, onde eles estão sendo guardados.

|Modo                   |Quando acontece                                                  |Onde fica                                      |
|-----------------------|-----------------------------------------------------------------|-----------------------------------------------|
|Armazenamento do Claude|App aberto dentro do Claude                                      |Armazenamento do próprio Claude, ligado à conta|
|Navegador              |App publicado, aberto pelo Safari ou pelo ícone da tela de início|`localStorage` do navegador                    |
|Sem armazenamento      |Ambiente que bloqueia o armazenamento                            |Nada é salvo; aparece um aviso amarelo no topo |

Pontos importantes:

- Os dados do Claude, os do Safari e os do ícone da tela de início são **separados**. O que é registrado em um não aparece nos outros. Escolha um único jeito de usar.
- Limpar os dados do Safari, remover o atalho ou trocar de celular pode apagar os registros. Por isso existe o backup.

### Estrutura dos dados

Cada registro é um objeto com:

```json
{
  "id": 1760000000000,
  "data": "2026-10-05T14:30:00.000Z",
  "humor": "bem",
  "sentimentos": ["Alegria", "Gratidão"],
  "comentario": "Texto opcional"
}
```

Valores possíveis de `humor` e o nível usado no gráfico de tendência:

|`humor`   |Nome     |Nível|
|----------|---------|-----|
|`muitoMal`|Muito mal|1    |
|`mal`     |Mal      |2    |
|`neutro`  |Neutro   |3    |
|`bem`     |Bem      |4    |
|`muitoBem`|Muito bem|5    |

A data escolhida no formulário é a data do registro. O aplicativo não guarda uma data de criação separada, e é por ela que tudo é ordenado e filtrado.

Chaves usadas no armazenamento: `registros` e `sentimentos-extras` (armazenamento do Claude), ou `diario-registros` e `diario-sentimentos-extras` (navegador).

-----

## Backup criptografado

Na aba *Relatório*, o cartão **Backup dos dados** tem um campo de senha e dois botões.

**Gerar backup**

1. Digite uma senha com pelo menos 6 caracteres.
1. Toque em **Gerar backup**.
1. Em **Backup pronto**, toque em **Salvar no celular** (abre a folha de compartilhar, onde você escolhe a pasta em *Arquivos*) ou em **Baixar arquivo**.

**Recuperar backup**

1. Digite a senha usada na criação do backup.
1. Toque em **Recuperar backup** e escolha o arquivo.
1. Os registros que ainda não estão no aplicativo são adicionados. Os que já existem (mesmo `id`) não são duplicados. Os sentimentos personalizados também são recuperados.

O arquivo é um `.json` com nome `diario-de-humor-backup-AAAA-MM-DD.json`. Backups antigos feitos em texto simples (uma lista de registros) ainda podem ser recuperados, sem senha.

**Alternativa em texto:** se o arquivo não puder ser salvo ou aberto no seu ambiente, há uma seção recolhida no cartão para copiar e colar o conteúdo do backup (que também é criptografado).

### Como a criptografia funciona

- Algoritmo: **AES-256-GCM**, que também detecta se o arquivo foi alterado.
- Chave derivada da senha com **PBKDF2-SHA256**, 250.000 iterações e um **sal aleatório** de 16 bytes.
- Cada backup usa um **IV aleatório** de 12 bytes.
- Tudo é feito pelo navegador (Web Crypto API), que exige uma página segura (`https`).
- O arquivo contém um envelope com os campos `app`, `versao`, `kdf`, `iter`, `sal`, `iv` e `dados` (o conteúdo criptografado).

> **Atenção:** a senha não é guardada em lugar nenhum e **não pode ser recuperada nem redefinida**. Se for perdida, o backup não pode ser aberto. Prefira uma frase longa e fácil de lembrar, por exemplo quatro palavras sem relação entre si.

-----

## Publicar gratuitamente (GitHub Pages)

Dá para fazer tudo pelo navegador do iPhone.

1. Salve o arquivo do aplicativo e o `apple-touch-icon.png` no app **Arquivos**. Renomeie o aplicativo para **`index.html`** e **não** renomeie o ícone.
1. No Safari, crie uma conta gratuita em [github.com](https://github.com).
1. Crie um repositório novo (por exemplo, `diario-de-humor`). Em contas gratuitas, ele precisa ser **público**.
1. Em **Add file → Upload files**, envie o `index.html` e o `apple-touch-icon.png` e toque em **Commit changes**.
1. Vá em **Settings → Pages**, escolha **Deploy from a branch**, a branch `main` e a pasta raiz (`/ (root)`), e salve.
1. Aguarde alguns minutos. O endereço será parecido com `https://SEUUSUARIO.github.io/diario-de-humor/`.

Só o código do aplicativo fica público. Os registros ficam no aparelho de cada pessoa.

-----

## Adicionar à tela de início do iPhone

1. No Safari, abra o endereço do aplicativo publicado.
1. Toque em **Compartilhar → Adicionar à Tela de Início**.
1. O nome sugerido é **Meu Humor** (curto, para não ser cortado embaixo do ícone). Você pode editá-lo nessa tela.

O ícone é um rosto sorridente branco sobre fundo índigo, com cinco pontos nas cores dos humores. O aplicativo abre em tela cheia, sem a barra do Safari.

Se você já tinha um atalho e trocou o ícone, **apague o atalho antigo e crie outro**: o iPhone guarda o ícone antigo. Lembre que o atalho novo é uma instalação separada e começa sem os registros do anterior, então gere um **backup antes** e recupere depois.

-----

## Atualizar o aplicativo

1. No repositório do GitHub, envie o novo `index.html` com **Add file → Upload files**. Ele substitui o antigo.
1. Aguarde um ou dois minutos.
1. No iPhone, feche o aplicativo e abra de novo.

Os registros guardados no aparelho continuam lá.

-----

## Privacidade e segurança

- Os registros ficam apenas no aparelho. O aplicativo não envia dados para nenhum servidor.
- Quem tiver o endereço do aplicativo consegue abri-lo, mas vê apenas o aplicativo vazio e os próprios dados, no próprio aparelho.
- Quem pegar o celular **desbloqueado** consegue abrir o aplicativo e ver o histórico. A proteção aqui é o bloqueio de tela do iPhone.
- O arquivo de backup é criptografado, mas o PDF e o CSV **não são**: só os compartilhe com quem você quiser que veja o conteúdo.
- Não envie backups, PDFs ou CSVs para repositórios públicos.

-----

## Limitações conhecidas

- **Sem sincronização:** não há nuvem. Para ver os dados em outro aparelho, use o backup.
- **Armazenamentos separados:** Claude, Safari e ícone da tela de início não compartilham dados.
- **Dentro do Claude** a visualização é uma área restrita: a folha de compartilhar, os downloads e a abertura de arquivos podem ser bloqueados. O uso completo é pelo aplicativo publicado.
- **PDF sem emojis:** a fonte do PDF não tem emojis. No lugar deles, o PDF usa carinhas desenhadas (uma para cada humor), e os gráficos usam nomes e cores.
- **Folha de compartilhar:** depende do navegador e do sistema. Há alternativas de abrir, baixar ou imprimir pelo navegador quando ela não está disponível.
- **Versões do iOS:** recomendado iOS 16.4 ou mais novo, por causa de recursos como compartilhamento de arquivos e estilos modernos de CSS.
- **Senha do backup:** não há como recuperá-la.

-----

## Para quem quiser mexer no código

O aplicativo é um único arquivo HTML, com CSS no `<style>` e JavaScript puro no `<script>`, sem dependências nem etapa de compilação.

**Onde mudar o que**

- `HUMORES`: lista dos 5 humores (id, emoji, nome e cor). O nível 1 a 5 do gráfico está em `NIVEL`.
- `SENTIMENTOS`: lista fixa de sentimentos.
- Variáveis de cor e tema (claro e escuro): bloco `:root` no início do CSS.

**Principais partes do JavaScript**

|Parte         |Função                                                                                                   |
|--------------|---------------------------------------------------------------------------------------------------------|
|Armazenamento |`carregar`, `persistir`, `carregarExtras`, `persistirExtras`                                             |
|Telas         |`telaRegistrar`, `telaHistorico`, `telaRelatorio`, `render`                                              |
|Filtro e ordem|`filtrados`, `porData`, `ordenar`                                                                        |
|Gráficos      |`graficoLinha` (SVG na tela), `dadosTendencia` (dados da linha)                                          |
|PDF           |`construirPDF` (gera o PDF), `gerarPDF` (entrega o arquivo), `imprimirRelatorio`                         |
|CSV           |`gerarCSV`, `baixarCSV`                                                                                  |
|Backup        |`cifrarBackup`, `decifrarBackup`, `gerarBackupCriptografado`, `salvarBackupNoCelular`, `restaurarDeTexto`|
|Eventos       |`addEventListener('click' ...)`, `'change'`, `'input'` e `'keydown'` no elemento `#conteudo`             |

**Observações técnicas**

- O PDF é montado diretamente em JavaScript (texto em Helvetica, gráficos desenhados como vetores), sem biblioteca, e entregue como arquivo pela folha de compartilhar.
- Os gráficos da tela são SVG gerado em texto.
- A cada alteração, a tela é redesenhada com `render()`. Os campos que precisam preservar o conteúdo digitado (comentário e data) têm tratamento próprio.
- Ao alterar a estrutura dos registros, mantenha a compatibilidade com dados já salvos nos aparelhos (campos novos devem ter valor padrão).