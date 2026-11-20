# Registro de Aniversários

Aplicação web simples para cadastrar aniversariantes, calcular idade/faixa etária, manter a lista organizada, compartilhar mensagens pelo WhatsApp/Telegram, importar/exportar dados em JSON e imprimir a relação.

> Este README considera a versão atual do projeto (`index_corrigido_v5.html`).

## Recursos

- Cadastro de nome e data de nascimento.
- Validação de datas no formato `dd/mm/aaaa`.
- Cálculo automático da idade.
- Classificação por faixa etária: Jovem, Meia idade, Maduro e Idoso.
- Textos de aniversário editáveis por faixa etária.
- Compartilhamento pelo WhatsApp e Telegram.
- Edição e exclusão de registros, com confirmação antes da exclusão.
- Importação e exportação da lista em JSON.
- Impressão da lista.
- Armazenamento dos dados no `localStorage` do navegador.
- Lista com área própria de rolagem.
- Interface responsiva para computador e celular.

## Arquivo principal

O projeto pode ser distribuído com o HTML renomeado para:

```text
index.html
```

Estrutura mínima:

```text
registro-aniversarios/
└── index.html
```

O HTML atual carrega a fonte Inter pelo Google Fonts. Portanto, a fonte externa depende de acesso à internet; caso ela não esteja disponível, o CSS possui fontes alternativas do sistema.

## Como executar localmente

### Opção 1 — abrir diretamente

Para um teste simples, abra `index.html` em um navegador moderno. As principais funções da aplicação são executadas no próprio navegador.

### Opção 2 — servidor local (recomendado)

Para reproduzir melhor o comportamento de um site hospedado e preparar o projeto para recursos de PWA, execute a pasta por HTTP local.

Se tiver Python instalado:

```bash
python -m http.server 8000
```

Depois acesse no navegador:

```text
http://localhost:8000/
```

## Armazenamento e backup

Os cadastros ficam salvos no `localStorage` do navegador. Isso significa que os dados pertencem ao armazenamento daquele navegador/origem e não constituem, por si só, sincronização entre computadores ou celulares.

Use **Exportar lista** periodicamente para gerar um arquivo JSON de backup. Para restaurar ou transferir uma lista, use **Importar lista**.

Antes de limpar dados do navegador, trocar de computador, reinstalar o sistema ou mudar a forma como a aplicação é hospedada, é recomendável exportar a lista.

## Instalação como aplicativo

Há duas situações diferentes:

1. **Instalar/adicionar o site como aplicativo pelo navegador**, quando o navegador oferece esse recurso.
2. **Transformar o projeto em um PWA propriamente instalável**, adicionando manifesto, ícones e, normalmente, os componentes necessários para a experiência desejada.

A versão atual é essencialmente um HTML autocontido e não inclui, neste pacote, `manifest.webmanifest`, ícones de PWA ou service worker. Para uma experiência PWA deliberadamente configurada, esses arquivos devem ser adicionados.

### Microsoft Edge — Windows/macOS

Com o projeto publicado em uma URL acessível pelo Edge:

1. Abra a página no Microsoft Edge.
2. Se o navegador identificar a página como PWA instalável, use o ícone de aplicativo disponível na barra de endereços e escolha **Instalar**.
3. O Edge também permite instalar um website pelo menu **Configurações e mais (...) > Mais ferramentas > Aplicativos > Instalar este site como um aplicativo**.
4. Aplicativos instalados podem ser gerenciados em `edge://apps`.

No Windows, um PWA instalado pelo Edge pode aparecer como aplicativo e ser fixado no menu Iniciar ou na barra de tarefas.

### Google Chrome — computador

Em sistemas/navegadores compatíveis, PWAs instaláveis podem apresentar um ícone de instalação na barra de endereços e uma opção de instalação no menu do navegador.

Para que o projeto seja reconhecido de forma consistente como PWA instalável, configure o manifesto do aplicativo e os demais requisitos de instalação da versão do navegador utilizada.

### Android

Em navegadores compatíveis com instalação de aplicações web, abra o endereço publicado do projeto e procure a opção de **Instalar** ou equivalente no menu do navegador. A disponibilidade e o texto exato da opção dependem do navegador e de o site atender aos critérios de instalação daquele navegador.

### iPhone — Safari

No Safari do iPhone:

1. Abra o endereço do aplicativo.
2. Toque em **Compartilhar**.
3. Escolha **Adicionar à Tela de Início**.
4. Ative **Abrir como App da Web**, quando a opção estiver disponível.
5. Toque em **Adicionar**.

O ícone será colocado na Tela de Início e poderá abrir o site como um aplicativo web.

## Tornando o projeto um PWA completo

Para uma instalação mais consistente, recomenda-se acrescentar estes arquivos:

```text
registro-aniversarios/
├── index.html
├── manifest.webmanifest
├── service-worker.js
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

E referenciar o manifesto no `head` do HTML:

```html
<link rel="manifest" href="manifest.webmanifest">
```

Exemplo de ponto de partida para `manifest.webmanifest`:

```json
{
  "id": "/",
  "name": "Registro de Aniversários",
  "short_name": "Aniversários",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#f8fafc",
  "theme_color": "#0c4a6e",
  "icons": [
    {
      "src": "icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

O manifesto informa ao navegador dados como nome, identidade, URL inicial, modo de exibição e ícones. Para produção, ajuste `id`, `start_url`, caminhos e ícones à URL real de hospedagem.

## Publicação

Para acesso por diferentes dispositivos e instalação via navegador, publique os arquivos em uma hospedagem web. Para os recursos modernos de PWA, prefira publicação em HTTPS.

Exemplos de tipos de hospedagem adequados:

- hospedagem estática;
- servidor web próprio;
- serviço de páginas estáticas.

A aplicação não exige banco de dados no servidor no formato atual, pois os registros ficam no armazenamento local do navegador.

## Importação e exportação

### Exportação

O botão **Exportar lista** gera um arquivo JSON contendo os registros e os textos personalizados.

### Importação

O botão **Importar lista** lê um JSON compatível. Registros duplicados são ignorados pela lógica atual quando nome e data coincidem.

## Compartilhamento

Cada registro com data válida recebe atalhos para compartilhamento de mensagem. A mensagem é montada no navegador e codificada para ser utilizada no link de compartilhamento.

O WhatsApp utiliza atualmente o endpoint direto `api.whatsapp.com/send` no projeto, preservando a codificação aplicada à mensagem, inclusive emojis.

## Impressão

Clique em **Imprimir lista** para abrir o diálogo de impressão do navegador. O CSS possui regras específicas de impressão para ocultar controles que não são necessários no papel.

## Privacidade

No formato atual, os cadastros são mantidos localmente no navegador por `localStorage`. O projeto não contém implementação própria de conta, servidor, banco de dados remoto ou sincronização em nuvem.

O uso dos botões de WhatsApp e Telegram abre serviços externos para compartilhamento. A fonte Inter também é solicitada ao Google Fonts enquanto houver conexão disponível.

## Compatibilidade

Recomenda-se utilizar versões atuais de navegadores modernos. A instalação como aplicativo varia conforme navegador, sistema operacional e configuração do website.

Para desktop, Chrome e Edge oferecem suporte a instalação de PWAs em plataformas compatíveis. No Edge, também existe a possibilidade de instalar um website pelo menu de aplicativos.

## Solução de problemas

### Meus dados desapareceram

Verifique se está usando o mesmo navegador e o mesmo endereço/origem utilizado anteriormente. Dados em `localStorage` são associados ao armazenamento local do navegador. Restaure um backup pelo botão **Importar lista**, caso possua um JSON exportado.

### A opção de instalar não aparece

Confirme que você está acessando a aplicação pela URL publicada e verifique se o navegador considera o site instalável. Para tornar a instalação PWA previsível, adicione um Web App Manifest válido, ícones e os demais componentes/requisitos aplicáveis.

### O aplicativo instalado não tem ícone apropriado

Adicione ícones apropriados ao projeto e declare-os no `manifest.webmanifest`.

### A fonte visual mudou sem internet

A página utiliza Google Fonts para carregar a fonte Inter. Sem acesso à rede, o navegador usa as fontes alternativas declaradas no CSS.

## Manutenção

Ao atualizar o projeto:

1. Faça backup dos registros importantes.
2. Substitua os arquivos publicados pela nova versão.
3. Teste cadastro, edição, exclusão, importação/exportação, impressão e compartilhamento.
4. Se houver PWA/service worker no futuro, controle a versão do cache para garantir que os usuários recebam os arquivos atualizados.

## Fontes de referência para instalação/PWA

- Microsoft Learn — uso e instalação de PWAs no Edge.
- Microsoft Support — instalação e gerenciamento de sites como aplicativos no Edge.
- web.dev — instalação de Progressive Web Apps.
- Chrome for Developers — manifesto e instalação de aplicações web.
- Apple Support — adicionar um site à Tela de Início e abri-lo como aplicativo web no iPhone.

## Licença

Nenhuma licença foi definida neste projeto. Caso o código seja distribuído publicamente, escolha e inclua uma licença apropriada às condições de uso desejadas.
