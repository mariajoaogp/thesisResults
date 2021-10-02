## Project Neto

A descrição da instalação está presente em: <https://github.com/ElevenPaths/neto>. Existem duas opções de instalação com e sem ***sudo***, com a opção ***sudo*** não ocorrem problemas na instalação e foi essa a opção utilizada.

O comando no documento ***README.md*** está errado, não é ***neto analysis***, mas sim ***neto analyser***. Apesar de só ter como exemplo ficheiros *xpi*, também aceita ficheiros *crx*.
    
Como o *ExtAnalyzer*, a ferramenta *Project Neto* faz uma análise estática, estas ferramentas analisam as mesmas características de uma extensão com algumas diferenças, mas estas não são relevantes para a análise de extensões maliciosas. 
<br /> Existem duas diferenças a ter em conta. O *Project Neto* para além das características da *ExtAnalyzer*, também procura um conjunto de *strings* suspseitas, por exemplo, “*GET*”, “*POST*”, “*paypal*”, etc. A outra diferença é que a *ExtAnalyzer* para além de enumerar as permissões descreve qual o impacto da mesma e também alerta para vulnerabilidades de funções como *jquery*. Outro ponto menos relevante é que o design gráfico da *ExtAnalyzer* é bastante mais apelativo e simples de navegar.
