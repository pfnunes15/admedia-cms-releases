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

1. Subir o `Version::CURRENT` no pacote.
2. Publicar a versão no repositório do CMS (etiqueta ou zip).
3. Só depois, actualizar o `latest.json` aqui e escrever o `CHANGELOG.md`.

Ao contrário, os sites anunciam durante uns minutos uma versão que ainda não
existe para descarregar.
