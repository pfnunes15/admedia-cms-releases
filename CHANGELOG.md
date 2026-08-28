# Versões do CMS

O que cada versão trouxe. Os sites lêem o `latest.json` ao lado deste
ficheiro e avisam no painel quando há uma mais nova do que a instalada.

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
