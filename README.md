# IMPULSO — Conquiste seu tempo

Aplicativo pessoal instalável para Android, iPhone e computador, feito com HTML, CSS e JavaScript, sem serviços externos ou dependências.

## O que faz

- Hábitos personalizáveis por **tempo dedicado** ou **quantidade realizada** (minutos, páginas, mililitros...).
- Metas diárias, recompensa em minutos, categorias, ativar/desativar e editar/excluir hábitos.
- Cronômetro de produtividade (iniciar, pausar, concluir), inclusive ao trocar de aba.
- Lazer por sessão cronometrada ou lançado manualmente.
- **Banco de tempo**: créditos acumulados não expiram; o lazer desconta créditos.
- **Bônus por exceder a meta**: configurável (padrão 50%).
- **Limites diário e semanal**: apenas restringem consumo; não apagam o banco.
- Estatísticas e gráficos dos últimos 7 dias, metas do dia, sequência e histórico.
- Exportação/restauração de backup JSON e suporte offline após primeiro carregamento bem-sucedido.

## Como são feitos os cálculos

A base é calculada de forma **cumulativa por hábito, dia e regra**, arredondando o total anterior e o posterior ao registro, e creditando somente a diferença. Isso evita ganhar mais minutos simplesmente dividindo a mesma atividade em vários registros.

O bônus usa a mesma lógica cumulativa de arredondamento, apenas sobre a parte da atividade que ultrapassou a meta diária.

`crédito do registro = base + bônus`.

`banco = soma dos créditos de todos os registros produtivos − soma de todo o lazer consumido`.

`lazer disponível para começar uma sessão = máximo(0, mínimo(banco, limite diário − lazer de hoje, limite semanal − lazer nesta semana))`.

Cada registro ganha crédito apenas uma vez; não há crédito adicional por não gastar. Sobras já permanecem no banco e podem ser usadas em outros dias, sempre respeitando os limites de consumo.

**Exemplo**: Estudar 25 minutos vale +10 min; meta diária de 100 minutos. Se você estudar 125 minutos de uma vez, recebe 50 minutos-base, mais 5 minutos de bônus na parcela adicional (50% de 10 minutos), totalizando 55 minutos.

O lazer usado é informado pelo usuário; não é detectado automaticamente e não bloqueia aplicativos ou sites.

## Arquivos

```text
impulso-app/
├── index.html           ← página inicial
├── styles.css           ← visual e responsividade
├── app.js               ← dados, cálculos e interações
├── manifest.webmanifest ← configuração de instalação
├── sw.js                ← funcionamento offline
├── .nojekyll            ← evita processamento especial do Pages
├── README.md            ← estas instruções
└── icons/
    ├── icon-192.png
    ├── icon-512.png
    └── icon-maskable-512.png
```

## Tutorial mais rápido: publicação gratuita pelo GitHub Pages

### Pré-requisitos

- Um computador conectado à internet.
- Um celular Android com Chrome ou iPhone com Safari.
- Uma conta gratuita em https://github.com/.
- **Não precisa baixar Node.js, Android Studio, Java, VS Code ou instalar dependências** para usar esta versão.

### Passo 1 — Descompactar

1. Baixe o arquivo `impulso-app.zip` entregue junto com esta documentação.
2. No Windows, abra **Explorador de Arquivos > Downloads**.
3. Clique com o botão direito no ZIP → **Extrair Tudo...** → **Extrair**.
4. Abra a pasta `impulso-app`. Confirme que `index.html`, `styles.css`, `app.js`, `sw.js`, `manifest.webmanifest` e a pasta `icons` estão nela.

### Passo 2 — Criar o repositório

1. Entre em https://github.com/ e crie ou acesse sua conta.
2. Clique no botão **+** no canto superior direito → **New repository** (Novo repositório).
3. Em **Repository name**, digite `impulso-app`.
4. Selecione **Public** (no plano gratuito, para GitHub Pages por branch).
5. Deixe **Add a README file** desmarcado (o projeto já contém um `README.md`).
6. Clique em **Create repository**.

### Passo 3 — Enviar os arquivos (atenção à estrutura)

1. No repositório vazio, clique no link **uploading an existing file** na tela de início. Se o repositório já tiver arquivos, use **Add file → Upload files**.
2. Na pasta descompactada `impulso-app` do Windows, selecione os arquivos internos e a pasta `icons` e arraste-os juntos para a área de upload do GitHub. Não arraste o ZIP.
3. Confirme que os arquivos estão na **raiz do repositório** e que os PNG ficam em `icons/`.
4. No final da página, escreva `Versão inicial do Impulso` em **Commit changes** e confirme o botão **Commit changes**.
5. Se arquivos ocultos não forem enviados, não tem problema: `.nojekyll` é opcional nesta versão. O essencial é a página, JavaScript, CSS, manifest, service worker e a pasta de ícones.

### Passo 4 — Publicar como site instalável

1. No repositório, clique em **Settings** (Configurações).
2. Na barra lateral esquerda, em **Code and automation**, clique em **Pages**.
3. Em **Build and deployment → Source**, escolha **Deploy from a branch**.
4. Em **Branch**, selecione `main` e, ao lado, `/(root)`.
5. Clique em **Save**.
6. Aguarde o GitHub concluir a publicação e recarregue a tela de **Pages**: ela mostrará **Visit site** e a URL do seu aplicativo.
7. O formato da URL costuma ser `https://SEU_USUARIO.github.io/impulso-app/` (substitua SEU_USUARIO pelo login do GitHub).
8. Clique em **Visit site** e teste no computador.

### Passo 5 — Instalar no Android

1. Abra o link publicado no **Chrome do celular**.
2. Toque nos três pontinhos **⋮** do Chrome.
3. Toque em **Instalar app**, caso disponível. Se não aparecer, use **Adicionar à tela inicial** (a redação depende do aparelho/navegador).
4. Confirme em **Instalar/Adicionar**.
5. Volte à tela inicial do celular: procure pelo ícone verde **Impulso** e abra.
6. Faça um teste: registrar 25 min de estudo, começar um lazer de alguns minutos e consultar o saldo.

### Passo 5B — Instalar no iPhone (alternativa)

1. Abra o link publicado pelo **Safari**.
2. Toque em **Compartilhar** (quadrado com seta para cima, ou Menu da página → Compartilhar).
3. Selecione **Adicionar à Tela de Início**.
4. Ative **Abrir como App**, quando exibido, e toque em **Adicionar**.
5. Abra o Impulso pelo novo ícone da tela inicial.

### Passo 6 — Testar o modo offline

1. Com internet, abra o aplicativo publicado e espere carregar completamente.
2. Feche o aplicativo, ative o modo avião e abra pelo ícone da tela inicial.
3. Se o conteúdo abrir, a instalação e o cache local funcionaram. Se não, abra novamente com internet e repita o teste.

## Testar ou editar no computador (opcional)

Para abrir a aplicação como PWA localmente você precisa de um servidor HTTP local (abrir o `index.html` diretamente por `file://` não instala corretamente o service worker). Se tiver Python:

1. Abra a pasta extraída no Explorador.
2. Clique na barra de endereço da pasta, digite `cmd` e pressione Enter.
3. Rode `py -m http.server 8000` (ou `python -m http.server 8000`).
4. Abra o Chrome e acesse http://localhost:8000/.
5. Edite `styles.css` para visual, `app.js` para lógica ou `index.html` para estrutura.
6. Para atualizar o site publicado: envie novamente os arquivos alterados para o GitHub. Se um ícone ou estilo antigo continuar aparecendo, feche e reabra o app e aguarde o cache atualizar.

## Exemplo de configuração pessoal

| Atividade | Tipo | Intervalo | Recompensa | Meta diária |
|---|---|---|---|---|
| Estudar | tempo | 25 min | +10 min | 100 min |
| Ler | tempo | 20 min | +10 min | 40 min |
| Treinar | tempo | 30 min | +15 min | 60 min |
| Fazer cardio | tempo | 20 min | +10 min | 30 min |
| Beber água | quantidade | 250 ml | +1 min | 2.000 ml |

É tudo configurável. Uma recompensa de lazer não é uma obrigação: você pode descansar sem ganhar minutos quando precisar. O objetivo é ajudar a manter hábitos, não punir necessidades básicas.

## Backup, privacidade e limites

- Em **Ajustes → Exportar JSON**, baixe um backup periódico e guarde em pasta privada.
- Em outro aparelho, abra o aplicativo e escolha **Ajustes → Importar JSON**. Isso substitui o histórico local desse aparelho. Não há sincronização automática entre celulares.
- Os dados ficam no armazenamento do navegador naquele dispositivo/origem. Limpar dados do site, desinstalar a PWA ou trocar de navegador/aparelho **pode apagar os registros**. Faça backup antes.
- O código enviado ao GitHub fica público, mas **seu histórico pessoal não é enviado ao repositório** — a menos que você publique o próprio arquivo do backup manualmente. Não envie backups para repositórios públicos.
- O banco é calculado pelo histórico. Excluir um ganho já gasto pode deixar saldo negativo; novas atividades recuperam o saldo.
- É uma ferramenta pessoal de autocontrole: não detecta o que você faz fora do app, não bloqueia Instagram/TikTok/jogos e não envia notificações push.
- Como as metas são diárias, um registro feito após a meia-noite conta para o novo dia. Sessões de lazer são vinculadas ao dia em que começaram.
- Por segurança, apps Web precisam ser publicados em **HTTPS** (ou executados em localhost) para instalação completa.

## Problemas comuns

**Não aparece "Instalar app"**: abra a URL HTTPS publicada (não `file://`) no Chrome Android; teste **Adicionar à tela inicial**; confirme que ícones e manifest estão presentes.

**Tela sem estilo / ícones quebrados**: confira se enviou a pasta `icons` e os arquivos para a raiz do repositório, não dentro de uma pasta `impulso-app/impulso-app/`.

**GitHub Pages mostra 404**: em Settings → Pages confirme `main / (root)`; confira se o `index.html` está na raiz; use a URL completa incluindo `/impulso-app/`; revise o histórico em **Actions**.

**App não atualiza após publicar novas alterações**: feche o app, conecte a internet, abra o site novamente e recarregue. Os recursos offline podem demorar uma visita para atualizar.

**Saldo parece errado**: abra **Progresso → Histórico**, confira os lançamentos positivos e negativos e lembre que o banco não é o mesmo que o limite disponível hoje.

## Licença

Projeto fornecido para uso pessoal e livre adaptação.
