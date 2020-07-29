# Detektor sluníčkovosti

Demo z [Czech-ULMFiT](https://github.com/simecek/Czech-ULMFiT) ve formě minimalistické webové aplikace pro Voila.

Spustit na Binderu (nutno vyčkat než se vytvoří docker image):  
https://mybinder.org/v2/gh/simecek/detektor_slunickovosti/master?urlpath=%2Fvoila%2Frender%2Fslunicko.ipynb

Spustit lokálně v nově vytvořeném environmentu:
```
  pip install -r requirements.txt
  voila slunicko.ipynb
```

## Jak to funguje?

Potkává se tu několik nástrojů, popořadě [fastai](https://docs.fast.ai/) (ta se stará o samotnou klasifikaci), [ipywidgets](https://ipywidgets.readthedocs.io/en/latest/) (tlačítka, textová oblast, interaktivita), [voila](https://voila.readthedocs.io/en/stable/using.html) (promění Jupyter notebook na webovou stránku) a [mybinder](https://mybinder.org/) (hostuje Jupyter notebook a tedy i tuto webovou stránku).

### fastai klasifikátor

Skripty použité pro natrénování klasifikátoru jsou v samostatném repu [https://github.com/simecek/Czech-ULMFiT](https://github.com/simecek/Czech-ULMFiT). Ve zkratce se jedná o neuronovou síť architektury [AWD-LSTM](https://yashuseth.blog/2018/09/12/awd-lstm-explanation-understanding-language-model/) s [sentencepiece](https://github.com/google/sentencepiece) tokenizací. Síť je nejprve natrénovaná na kompletní české [Wikipedii](https://cs.wikipedia.org/wiki/Hlavn%C3%AD_strana) a poté dotrénovaná rozpoznání sentimentu recenzí z [ČSFD](https://www.csfd.cz/). 

Použití klasifikátoru je demonstrováno v tomto [colab notebooku](https://colab.research.google.com/drive/1IAWBejZWvXDUirxA8RpBlV1sH3Mv8Uka?usp=sharing). Slovník pro tokenizaci je uložený v [https://github.com/simecek/detektor_slunickovosti/tree/master/tmp](https://github.com/simecek/detektor_slunickovosti/tree/master/tmp), samotná neuronová síť v 63MB souboru [https://github.com/simecek/detektor_slunickovosti/blob/master/cs_csfd_2classes_945.pkl](https://github.com/simecek/detektor_slunickovosti/blob/master/cs_csfd_2classes_945.pkl).

### ipywidgets

*IPyWidgets* umožňují přidat do Jupyter notebooku HTML elementy, jako tlačítko nebo textový vstup, a interaktivitu (když se zmáčkne tlačítko, spusť tuhle Python funkci na textový vstup a výsledkem přepiš textový výstup). Jak jsou použity zde se můžete podívat do [slunicko.ipynb](https://github.com/simecek/detektor_slunickovosti/blob/master/slunicko.ipynb). Pozor, *IPyWidgets* nefungují v Google Colabu.

### voila

*Voila* server umožňuje běžet Jupyter notebook jako by to byla webová stránka. Díky HTML elementům z *ipywidgets* není v našem případě poznat, že se jedná o Jupyter notebook (nejsou vidět jednotlivé buňky). *Voila* můžete spustit lokálně, v cloudu (AWS, GCP, Digital Ocean, ...) nebo prostřednictvím *Binderu*. 

### mybinder

Primární účel [mybinder.org](https://mybinder.org/) je reprodukovatelná analýza. Na základě informací v [requirements.txt](https://github.com/simecek/detektor_slunickovosti/blob/master/requirements.txt) sestaví docker image, v kterém je možné spustit skripty a notebooky z příslušného GitHub repozitáře, tedy i výše uvedené [slunicko.ipynb](https://github.com/simecek/detektor_slunickovosti/blob/master/slunicko.ipynb) pomocí *Voila*.

## Acknowledgements

Tento trik jsem se naučil na Practical Deep Learning for Coders kurzu z roku 2020. K českému jazykovému modelu a klasifikátoru jsem se po roce vrátil díky spolupráci se Zdenkem Hrubým.
