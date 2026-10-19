# admedia-cms-releases

O manifesto de versões do CMS da Admedia. Nada mais.

O `latest.json` diz qual é a última versão publicada. Cada site pergunta por
ela uma vez por dia e avisa no painel quando está atrasado. O código do CMS
não está aqui — está num repositório privado; aqui só está o número da
versão e o que ela trouxe, que são coisas que não fazem mal a ninguém.

Este repositório é público de propósito: assim os sites lêem-no sem token
nenhum. Um token de leitura no `config` de cada site seria um token a mais
em cada sítio onde um site está alojado, e daria acesso ao código-fonte —
não a uma lista de versões.

## Publicar uma versão

Por esta ordem, que importa:

1. **Correr os sites todos**: `php bin/check-sites.php`, no repositório do
   pacote. Ele arranca cada site com a configuração real e desenha os ecrãs
   do backoffice; um site que ninguém abra é um site onde a regressão só
   aparece quando o cliente lá for. Ele próprio recusa-se a deixar passar:
   acaba com «Do not tag a version like this».
2. Subir o `Version::CURRENT` no pacote.
3. Commit, etiqueta `vX.Y.Z` e push das duas — é a etiqueta que o Composer
   vê.
4. Em cada site: `composer update admedia/cms` e depois
   `php {pacote}/bin/cms-publish.php .`, que copia os ficheiros do
   backoffice. Sem o segundo, o site fica com o código novo e o CSS antigo.
5. **Só depois, actualizar o `latest.json` aqui e escrever o `CHANGELOG.md`.**

Ao contrário nos dois últimos, os sites anunciam durante uns minutos uma versão
que ainda não existe para descarregar. Sem o primeiro, anunciam uma que existe
e os parte.

O quinto passo é o que mais vezes fica por fazer, porque é o único que não dá
erro nenhum quando falha: o manifesto esteve vinte e cinco versões parado e o
painel de todos os sites respondeu «está actualizado» durante esse tempo
inteiro. Um aviso que mente é pior do que não haver aviso.
