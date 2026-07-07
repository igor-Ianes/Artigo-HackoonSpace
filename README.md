# Como os computadores "ouvem" a música: Aplicação da Transformada de Fourier na Análise de Áudio Digital 
## Intrudução
A música está presente no cotidiano de milhões de pessoas e, com o avanço da tecnologia, passou a ser analisada, processada e reproduzida por sistemas computacionais de maneira cada vez mais sofisticada. Aplicações como serviços de streaming, afinadores digitais, assistentes virtuais, softwares de edição de áudio e sistemas de reconhecimento de músicas demonstram que computadores são capazes de interpretar informações sonoras com grande precisão. Embora essas aplicações pareçam muito distintas entre si, todas compartilham um mesmo desafio: transformar um sinal de áudio em informações que possam ser compreendidas e processadas por um computador.

Diferentemente dos seres humanos, que percebem naturalmente características como notas musicais, timbre e intensidade sonora, os computadores recebem apenas uma sequência de valores numéricos obtidos pela digitalização do som. A partir desses dados, torna-se necessário utilizar técnicas capazes de identificar quais frequências compõem o sinal analisado, permitindo reconhecer padrões, separar componentes sonoros e extrair informações relevantes.

Nesse contexto, a Transformada de Fourier destaca-se como uma das ferramentas matemáticas mais importantes do Processamento Digital de Sinais (PDS). Seu princípio consiste em converter um sinal representado no domínio do tempo para o domínio da frequência, possibilitando identificar os diferentes componentes espectrais presentes em um áudio. Essa abordagem constitui a base de inúmeras aplicações modernas, incluindo equalizadores, afinadores eletrônicos, sistemas de reconhecimento de voz, compressão de áudio em formatos como MP3 e serviços de identificação musical.

Diante desse cenário, este artigo tem como objetivo apresentar os fundamentos da Transformada de Fourier aplicados à análise de áudio digital, estabelecendo a relação entre conceitos de processamento de sinais e aplicações musicais. Inicialmente, são discutidos os princípios físicos do som, sua representação digital e os fundamentos da Transformada de Fourier e da Transformada Rápida de Fourier (FFT). Em seguida, na segunda etapa do trabalho, será apresentada uma implementação computacional capaz de analisar arquivos de áudio e identificar suas frequências predominantes, demonstrando, na prática, como computadores podem "ouvir" e interpretar informações musicais.
Diante desse cenário, este artigo tem como objetivo apresentar os fundamentos da Transformada de Fourier aplicados à análise de áudio digital, estabelecendo a relação entre conceitos de processamento de sinais e aplicações musicais. Inicialmente, são discutidos os princípios físicos do som, sua representação digital e os fundamentos da Transformada de Fourier e da Transformada Rápida de Fourier (FFT).

Por fim, na segunda etapa do trabalho, será apresentada uma implementação computacional capaz de analisar arquivos de áudio e identificar suas frequências predominantes, demonstrando, na prática, como computadores podem "ouvir" e interpretar informações musicais. Dessa forma, busca-se integrar os fundamentos teóricos e a implementação computacional, evidenciando a importância da Transformada de Fourier no processamento digital de sinais de áudio.

## No mundo fisico

## O Som e as Ondas Sonoras
O som é um fenômeno físico produzido pela propagação de vibrações mecânicas em um meio material, como o ar, a água ou sólidos. Quando um instrumento musical é tocado ou uma pessoa fala, ocorre a vibração de um corpo, provocando variações de pressão que se propagam pelo meio na forma de ondas sonoras. Essas ondas transportam energia e, ao alcançarem o ouvido humano, são interpretadas pelo cérebro como diferentes sons.

As ondas sonoras podem ser descritas por diversas características físicas, sendo as mais importantes a frequência, a amplitude e o período. A frequência corresponde ao número de oscilações realizadas pela onda em um segundo e é medida em hertz (Hz). Essa grandeza está diretamente relacionada à percepção da altura do som: frequências mais elevadas são percebidas como sons agudos, enquanto frequências menores produzem sons graves. A amplitude representa a intensidade da vibração da onda e está associada ao volume percebido pelo ouvinte, enquanto o período corresponde ao tempo necessário para que uma oscilação completa seja realizada.

Na música, cada nota possui uma frequência fundamental característica. Como exemplo, a nota Lá da quarta oitava (A4), utilizada como referência para afinação de instrumentos musicais, possui frequência de 440 Hz. Entretanto, instrumentos diferentes podem produzir essa mesma nota apresentando características sonoras distintas. Isso ocorre porque, além da frequência fundamental, o som produzido é composto por diversas frequências adicionais, conhecidas como harmônicos, cuja combinação determina o timbre característico de cada instrumento.

Embora o sistema auditivo humano consiga distinguir naturalmente essas diferentes componentes sonoras, os computadores não interpretam o áudio da mesma maneira. Para um sistema computacional, um som é representado inicialmente apenas como uma sequência de valores numéricos que descrevem a variação da amplitude ao longo do tempo. Dessa forma, torna-se necessário utilizar técnicas matemáticas capazes de identificar as frequências presentes nesse sinal, permitindo sua análise e processamento, tema que será abordado nas próximas seções.

## Representação Digital do Áudio
Embora o som seja um fenômeno contínuo no mundo físico, os computadores somente conseguem processar informações em formato digital. Dessa forma, para que um sinal sonoro possa ser armazenado, analisado ou reproduzido por um sistema computacional, é necessário convertê-lo em uma sequência de valores numéricos por meio de um processo denominado digitalização do áudio.

A digitalização é realizada principalmente por duas etapas: a amostragem e a quantização. A amostragem consiste na captura periódica dos valores de amplitude do sinal analógico em intervalos de tempo regulares. O número de amostras coletadas por segundo é denominado taxa de amostragem e é medido em hertz (Hz). Quanto maior essa taxa, maior será a capacidade de representar fielmente o sinal original. Um exemplo bastante conhecido é o padrão utilizado em CDs de áudio, que emprega uma taxa de amostragem de 44.100 Hz, permitindo registrar frequências dentro da faixa audível pelo ser humano.

Após a amostragem, cada valor obtido passa pelo processo de quantização, no qual a amplitude do sinal é convertida para um valor discreto representável digitalmente. O conjunto dessas amostras forma uma sequência numérica que descreve a variação da amplitude do sinal ao longo do tempo. Para o computador, portanto, uma música não é inicialmente composta por notas musicais ou instrumentos, mas sim por milhares de valores organizados em sequência.

Esses dados podem ser armazenados em diferentes formatos de arquivo de áudio. Entre eles, destaca-se o formato WAV, amplamente utilizado em aplicações de processamento digital de sinais por armazenar o áudio sem perdas de qualidade decorrentes de compressão. Essa característica preserva as informações originais do sinal, tornando-o adequado para análises espectrais e experimentos computacionais.

Uma vez representado digitalmente, o sinal de áudio pode ser submetido a diferentes técnicas de processamento. Entre elas, destaca-se a Transformada de Fourier, capaz de converter a representação do sinal no domínio do tempo para o domínio da frequência, permitindo identificar as componentes espectrais que caracterizam o conteúdo musical analisado.

## Transformada de Fourier
Após a digitalização, o sinal de áudio passa a ser representado por uma sequência de amostras que descrevem sua variação ao longo do tempo. Embora essa representação seja suficiente para armazenar e reproduzir o som, ela não permite identificar de forma direta quais frequências compõem o sinal. Para realizar essa análise, utiliza-se a Transformada de Fourier, uma das ferramentas matemáticas mais importantes do Processamento Digital de Sinais.

A Transformada de Fourier consiste em um método capaz de converter um sinal do domínio do tempo para o domínio da frequência. Enquanto no domínio do tempo é possível observar apenas como a amplitude do sinal varia ao longo dos instantes, no domínio da frequência torna-se possível identificar quais componentes espectrais estão presentes e qual a intensidade de cada uma delas.

De forma intuitiva, a Transformada de Fourier pode ser compreendida como um processo de decomposição de um sinal complexo em um conjunto de ondas senoidais mais simples, cada uma associada a uma frequência específica. Assim, um trecho musical executado por diferentes instrumentos pode ser analisado como a combinação de diversas frequências fundamentais e de seus respectivos harmônicos, permitindo compreender a estrutura espectral do áudio.

Essa mudança de representação é fundamental para diversas aplicações computacionais. Ao identificar as frequências presentes em um sinal, torna-se possível reconhecer notas musicais, analisar timbres, remover ruídos, aplicar filtros, desenvolver equalizadores e implementar sistemas capazes de identificar músicas ou comandos de voz. Em vez de trabalhar apenas com uma sequência de valores numéricos, o computador passa a interpretar as características espectrais do áudio, tornando sua análise significativamente mais eficiente.

No contexto deste trabalho, a Transformada de Fourier representa o principal mecanismo utilizado para extrair informações musicais de sinais digitalizados. Sua aplicação permitirá, na etapa prática da pesquisa, identificar as frequências predominantes presentes em arquivos de áudio e relacioná-las às respectivas notas musicais, demonstrando como computadores podem analisar e interpretar sinais sonoros de maneira automatizada.

## Transformada Rápida de Fourier (FFT)


## Aplicações da Transformada de Fourier na Música

## Referências

1. [Fundamental of music processing - https://www.audiolabs](https://www.audiolabs-erlangen.de/content/05_fau/professor/00_mueller/04_bookFMP/02_slides/Mueller_FMP_Preface.pdf)
   
2. [Identification and Analysis of Instrument Frequencies in Monophonic Music Based on FFT](https://dl.acm.org/doi/10.1145/3784013.3784045?__cf_chl_f_tk=BmoLl9memGZjwB.Lmh9CI6Ava_UvmjeU6m0ptQK7t9w-1783352165-1.0.1.1-0vqSEPitmUX_d.cekhBffcSZg34sdWVBQm9wXGdQnPs)
  
3. [Transformada de Fourier de Curto Prazo Explicada Facilmente - Youtube](https://www.youtube.com/watch?v=-Yxj3yfvY-4&t=1148)
   
4. [everything you need to know about fourier transform  | towards data science](https://towardsdatascience.com/everything-you-need-to-know-about-fourier-transform/)
   
5. [Transformada rapida de Fourier - Wikipedia](https://en.wikipedia.org/wiki/Fast_Fourier_transform)
    
6. [But what is the Fourier Transform? A visual introduction.](https://www.youtube.com/watch?v=spUNpyF58BY
)
7. [COOLEY, James W.; TUKEY, John W. An algorithm for the machine calculation of complex Fourier series. Mathematics of Computation, v. 19, n. 90, p. 297-301, 1965.](https://web.stanford.edu/class/cme324/classics/cooley-tukey.pdf)
    
8. [RAO, K. R.; KIM, Do Nyeon; HWANG, Jae Jeong. Fast Fourier Transform: algorithms and applications. Nova York: Springer, 2010.](https://www.researchgate.net/publication/392265666_Fourier_Transforms_Fourier_Series_and_the_FFT_Algorithm)
    
9. [BRACEWELL, Ronald N. The Fourier transform and its applications. 3. ed. Boston: McGraw-Hill, 2000.](https://scispace.com/pdf/the-fourier-transform-and-its-applications-iursr090ke.pdf)
    
10. [STEWART, James. Cálculo: volume 2. 8. ed. São Paulo: Cengage Learning, 2016.](https://www.stewartcalculus.com/)
