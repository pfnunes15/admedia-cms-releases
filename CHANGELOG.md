# Versões do CMS

O que cada versão trouxe. Os sites lêem o `latest.json` ao lado deste
ficheiro e avisam no painel quando há uma mais nova do que a instalada.

## 2.29.0

**O CMS passa a actualizar-se pelo próprio backoffice.** Em
**Definições › O CMS**: envia-se o `.zip` da versão e ele instala-se — sem
FTP, e sem linha de comandos para as migrações.

O ficheiro é **enviado por quem está autenticado** e não descarregado pelo
site. Um site que vai buscar código à internet por sua conta é um site que
qualquer pessoa que consiga responder por esse endereço passa a poder
reescrever; e ir buscá-lo ao repositório do CMS, que é privado, obrigaria a
ter uma senha de leitura do código-fonte todo no `config` de cada site.

Recusa-se, **sem escrever nada**: um ficheiro que não seja este pacote, um que
traga uma versão mais antiga do que a instalada, um de número maior diferente,
e um que leve caminhos para fora da pasta dele.

A versão anterior fica guardada em `vendor/admedia/cms.previous`. Se alguma
coisa estiver errada, troca-se o nome das duas pastas e o site volta ao que
era.

A instalação é em dois passos — os ficheiros primeiro, as migrações e os
ficheiros do backoffice a seguir — porque entre um e outro o PHP está a correr
metade de cada versão. Quem fechar o separador a meio encontra o ecrã a dizer
o que falta quando voltar: isso é lido do disco e da base de dados, e não de
uma marca na sessão.

## 2.4.0 – 2.28.0

**Este ficheiro esteve vinte e cinco versões sem ser escrito.** O `latest.json`
ficou na 2.3.1 enquanto o pacote chegava à 2.28.0, e por isso o «Verificar
agora» do painel respondeu «está actualizado» a toda a gente durante esse
tempo — com confiança, e sem nada que o denunciasse. Está dito aqui porque um
aviso que mente é pior do que não haver aviso, e porque a ordem de publicar
que está no README existe precisamente para isto e não foi seguida.

As versões vão agrupadas pelo que mudam, e não uma a uma: vinte e cinco
secções seriam um registo que ninguém lê. Nada no meio disto obriga a mexer
num site — todas se instalam por cima.

### O editor de páginas passou a ser a página

Era uma lista de blocos com os nomes por baixo, e quem montava uma página não
conseguia ver o que estava a montar.

- A página é desenhada inteira, cada bloco com o conteúdo real e o desenho do
  site, uns encostados aos outros como ficam lá fora.
- Os blocos arrastam-se para a página a partir de uma coluna à direita, e
  abre-se um espaço no sítio onde vão cair antes de se largar.
- **Escreve-se directamente na página.** Carrega-se num título e muda-se ali;
  guarda-se sozinho quando o cursor sai. Um campo que o desenho do site parta
  ao meio antes de o imprimir continua a editar-se no formulário, de
  propósito: mais vale não deixar editar do que guardar um quarto de um
  título.
- O nome, a descrição e a estrutura da página desceram para baixo da folha,
  em abas.

### Achar uma coisa entre muitas

- A lista de páginas procura por nome e por endereço, filtra por estado, e
  **agrupa pela zona do site** — num site com uma página por vinho, isso é
  «Os nossos vinhos 66» ao lado de «11 fora destas». O agrupamento sai do
  endereço, sem ninguém ter de etiquetar nada.
- O cabeçalho das tabelas acompanha quem faz scroll.
- O selector de blocos ganhou procura e títulos: trinta e quatro blocos
  deixaram de ser uma parede.
- Os utilizadores também procuram e filtram, com a mesma forma e as mesmas
  palavras — dois ecrãs iguais são uma coisa para aprender e não duas.

### Os campos escrevem-se sempre da mesma maneira

- Uma data é sempre um calendário e uma hora é sempre um relógio. Uma caixa
  onde se escreve uma data é uma caixa onde 3/5 é Março para uns e Maio para
  outros.
- Um ficheiro é sempre um botão de carregar, nunca um caminho escrito à mão.
  Isso vale para fotografias e passou a valer para documentos — uma ementa em
  PDF, uma lista de preços.
- O texto formatado abre o editor em todo o lado. Havia dois sítios onde a
  caixa dizia ser um editor e não era: ficavam a HTML em cru.

### As secções longas passaram a abas

Um só componente em todo o backoffice: as definições, o editor de um bloco, o
editor de uma página, as visitas. A aba escolhida fica no endereço — dá para
mandar uma ligação para a parte que interessa — e é lembrada, para que gravar
não devolva ninguém ao princípio.

### Funcionalidades: a loja instala-se por um botão

Em **Definições › Funcionalidades**. Um site sem loja só ganhava uma se
alguém lhe pusesse um ficheiro por FTP e corresse as migrações numa linha de
comandos que o alojamento partilhado não tem.

Desligar muda o nome ao ficheiro e **não apaga tabela nenhuma**: uma loja que
recebeu uma encomenda guarda essa encomenda, o cliente e o dinheiro cobrado.
Voltar a ligar repõe a configuração que o site tinha.

### A loja, as línguas e o correio

- **Contas de cliente**, com porta própria e sessão separada da do pessoal.
  Um cliente e um funcionário podem estar os dois com sessão aberta no mesmo
  navegador sem se confundirem.
- As páginas de erro e o selector de língua deixaram de estar em português
  fixo, e o `hreflang` deixou de anunciar traduções que não existem.
- **O correio que o CMS envia sobrevive à viagem.** Ia em 8-bit sem o
  declarar, o que dá a qualquer servidor pelo caminho o direito de lhe cortar
  os acentos, e com linhas acima do que a norma permite, que o mesmo servidor
  pode partir a meio de uma etiqueta. E o «Responder» de um pedido de
  contacto passa a chegar a quem o escreveu.

### O que um site pode declarar por si

Sem forçar nada em quem não declarar nada:

- as entradas que acrescenta à barra lateral (`config/admin-nav.php`);
- as folhas de estilo dos ecrãs que traz de seu (`config/admin.php`);
- as folhas que o editor usa para desenhar um bloco (`config/preview.php`) —
  sem isto o editor adivinhava três nomes e desenhava a página sem estilo
  nenhum nos sites onde não acertava;
- de onde aceita ser posto dentro de um frame.

### Correcções que vale a pena nomear

- **O backoffice esteve sem uma única linha de contorno** e ninguém percebia
  porquê: três cores dependiam de uma variável que nunca foi definida.
- **O atributo `hidden` não escondia**, por causa de uma regra de `display`
  que lhe ganhava — e por isso a procura no selector de blocos não filtrava
  nada.
- `bin/cms-publish.php`, que copia os ficheiros do backoffice para o site. O
  README já mandava corrê-lo e o ficheiro não existia.

## 2.3.1

Só o backoffice, e só à vista. Nada mudou de forma; instala-se por cima.

- **As gavetas «Definições avançadas» abrem e fecham com movimento.** Um
  `<details>` abre de repente: o conteúdo aparece todo de uma vez e a página dá
  um salto por baixo dele — e quem carregou fica sem saber de onde veio aquilo.
  Agora a caixa cresce da altura fechada até à aberta, em pouco mais de um
  quarto de segundo, e encolhe pelo mesmo caminho. A seta ao lado do título
  roda em vez de trocar de desenho.
- Quem tiver pedido ao sistema para não haver movimento continua a ter a gaveta
  a abrir de uma vez, como antes.

## 2.3.0

Aditivo. Nada do que existia mudou de forma, e a versão instala-se por cima.

- **A loja inteira passa a ser do pacote.** Faltava metade dela: o cesto, o
  checkout, o aviso de pagamento, o modelo da encomenda e o backoffice de
  produtos e encomendas viviam dentro de um dos sites. O segundo site a vender
  obrigava a copiá-los, e a partir daí eram duas lojas a divergir. Montam-se
  agora em três chamadas — `Shop::routes()`, `Shop::adminRoutes()` e
  `Shop::callbackRoutes()` —, e a ordem por que se registam deixa de ser
  conhecimento de cada projecto.
- **Os endereços da loja são de cada site.** `/loja` e `/carrinho` estavam
  escritos dentro do controlador, o que fazia dele um controlador português.
  Declaram-se em `config/shop.php`; o que não for declarado fica em inglês, que
  é o que o pacote traz. A assinatura das encomendas — o `QM-` de
  `QM-2026-0007` — passa pelo mesmo sítio.
- **Um catálogo de frases.** O que o CMS diz ao visitante sai dos controladores
  para `lang/{código}.php`, o do pacote com o do site por cima, e pede-se por
  `__('shop.cart.empty')`. Um site muda uma linha escrevendo só essa linha. Sem
  isto, subir a loja para o pacote era dar português a quem não o fala.
- **A confirmação da encomenda vai na língua em que foi comprada.** A coluna
  `locale` já estava gravada e nunca tinha sido lida.
- **Nav, Booking, Phone e Colour** — e a lista de redes sociais — sobem também.
  Nenhum deles sabia nada do site onde estava.

Duas correcções:

- o aviso de pagamento importava `Admedia\Core\Mailer`, uma classe que deixou
  de existir quando o correio passou a serviço. Como o envio apanha
  `\Throwable`, o erro fatal era engolido em silêncio e **a confirmação de uma
  encomenda paga nunca chegava a sair**. Quem tiver a loja a funcionar deve
  actualizar por causa disto e mais nada;
- a barra do backoffice mostrava «Produtos» e «Encomendas» em sites sem loja, a
  apontar para rotas que ninguém registou. Passa a depender do site ter loja, e
  ganha o catálogo e os portes, que faltavam.

## 2.2.0

Aditivo: nada do que existia mudou de forma.

- **IVA.** O preço guardado já o inclui e a decomposição é feita para trás —
  a 23%, doze e trinta contêm 2,30 e não 2,83. A taxa fica no produto e cai
  para a da loja quando não é dita; a encomenda guarda taxa e valor por linha,
  como foram no dia.
- **Reserva de stock.** O que está no cesto de quem já foi pagar fica apartado
  por vinte minutos, para a última garrafa não ser vendida duas vezes. A
  reserva expira sozinha e não desce o stock — quem o desce continua a ser o
  pagamento confirmado.
- **Categorias no lado público.** Uma categoria mostra também o que está nas
  categorias abaixo dela.
- O envio de e-mail passou a serviço, para poder ser lido num teste em vez de
  enviado.

## 2.1.0

Tudo aditivo: nada do que já existia mudou de forma, por isso o número maior
mantém-se e a versão instala-se por cima.

**Loja, como camada opcional.** Um site liga-a tendo um `config/shop.php`
seu; sem esse ficheiro, as tabelas da loja nem são criadas. Traz:

- catálogo com categorias em árvore, etiquetas, características inventadas
  no backoffice e produtos relacionados — escolhidos à mão, ou os da mesma
  categoria quando ninguém escolhe;
- portes por zonas e escalões, que cobram por peso, por número de artigos
  ou um valor fixo, com países por zona;
- pagamentos atrás de um contrato, com o Stripe como primeira
  implementação. Acrescentar outro fornecedor é escrever uma classe e
  listá-la.

**Menus por página.** Uma página escolhe que menu mostra no cabeçalho. Os
menus declaram-se em `config/menus.php`. Num site que não declare nenhum, o
campo nem aparece e tudo fica como estava.

**Aviso de actualização.** É o que está a ler isto.

**Uma terceira linha de texto** nos itens de um bloco, para cartões que
precisam de nome, subtítulo e legenda.

## 2.0.0

O CMS extraído do site da Quinta da Moscadinha e transformado em pacote
partilhado, com duas camadas: `Core`, o mínimo que todos os sites usam, e
`Cms`, as páginas e os blocos, que são opcionais.
