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

1. **Correr os sites todos**: `php bin/verifica-sites.php`, no repositório do
   pacote. Os sites instalam-no por symlink e saltam para a versão nova no
   instante em que ele muda — não há `composer update` a servir de porta, e um
   site que ninguém abra é um site onde a regressão só aparece quando o cliente
   lá for.
2. Subir o `Version::CURRENT` no pacote.
3. Publicar a versão no repositório do CMS (etiqueta ou zip).
4. Só depois, actualizar o `latest.json` aqui e escrever o `CHANGELOG.md`.

Ao contrário nos dois últimos, os sites anunciam durante uns minutos uma versão
que ainda não existe para descarregar. Sem o primeiro, anunciam uma que existe
e os parte.
