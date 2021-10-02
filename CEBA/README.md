## Chrome Extension Behavior Analysis

O *setup* da ferramenta é igual aquele descrito em: <https://github.com/adewes/chrome-extension-behavior-analysis>

Esta ferramenta é dinâmica, abre o *chromium*, navega *websites* e regista todos os *websites* secundários acedidos. 

A aplicação percorre a *Chrome Web Store* e faz o *download* das extensões a analisar, no entanto como neste estudo estão a ser analisadas sempre as mesmas extensões este passo é feito manualmente e apenas a análise é feita com a ferramenta. Para ser utilizada apenas a análise é necessário primeiro:
1. Alterar o ficheiro ***data/extensions.json***, de forma a analisar as extensões deste estudo o ficheiro deve ser substituído por aquele presente nesta diretoria;
2. Colocar os ficheiros *crx* na diretoria ***data/extensions***, o nome dos ficheiros *crx* tem de ser alterado, pois é esperado com a constistuição ***id-timestamp*** (para o *timestamp* foram colados números de 0 a 14). Para analisar as extensões presentes neste estudo, substituir a pasta ***data/reports*** pela ***reports*** presente nesta diretoria;

Os *websites* percorridos são aqueles enumerados no ficheiro ***extensions/test.py***:
- <https://en.wikipedia.org/wiki/List_of_wikis>;
- <https://www.uni-tuebingen.de>;
- <https://www.uni-sb.de>;
- <https://www.eff.org>;
- <https://www.mozilla.org>;
- <https://www.arbeitsagentur.de>;
- <https://www.tagesschau.de>;
- <https://www.inria.fr>;
- <https://www.google.de/?gfe_rd=cr&ei=dr9fWKHfJc7i8AeutpSwAg#q=test>;
- <https://www.facebook.com/Speicherstadt-Kaffeer\%C3\%B6sterei-118962444840064/>;
- <https://www.youtube.com/watch?v=WhU1ZXLsKCg>;
- <https://www.google.de/maps/@49.3428062,6.78282,13z?hl=en>;
- <https://twitter.com/josephfcox>.
