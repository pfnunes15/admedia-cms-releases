# Versões do CMS

O que cada versão trouxe. Os sites lêem o `latest.json` ao lado deste
ficheiro e avisam no painel quando há uma mais nova do que a instalada.

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
