Liner2 SOAP API Vagrant and Ansible configuation
============

The goal of this project is to give you one command to run the machine with all needed by [Liner2](http://nlp.pwr.wroc.pl/narzedzia-i-zasoby/narzedzia/liner2) SOAP API tools installed and configured.

Tu run the machine first install VirtualBox, Vagrant and ansible. Next run
```
vagrant up
```
in the main repo directory and that's all. If it failed, because of some timeout or network issues, you can run it again on the running machine using
```
vagrant provision
```
If it succeded you can use the SOAP API with 6 models (timex1, timex4, event8, ner-n82, ner-names, ner-top9) running on your localhost on port 8080.

### Python example
```python
from zeep import Client

c = Client('http://localhost:8080/nerws/ws/nerws.wsdl')

res = c.service.Annotate(text='W połowie stycznia 2013 Teodorczyk podpisał kontrakt z Lechem Poznań, który miał wejść w życie 1 lipca[1]. 18 lutego 2013 poznański klub poinformował, że piłkarz wzmocni jego szeregi już wiosną. W zespole Lecha zadebiutował 24 lutego 2013 w wygranym 4:0, ligowym meczu z Ruchem Chorzów, zaliczając dwie asysty.', input_format='plain:wcrft', output_format='tuples', model='timex4')

c.service.GetResult(token=res.msg)
```

## Components

- Ubuntu 12.04 (because of Boost dependencies)
- [Corpus2](http://www.nlp.pwr.wroc.pl/redmine/projects/corpus2/wiki)
- [Morfeusz-SGJP](http://sgjp.pl/morfeusz/)
- [Toki](http://www.nlp.pwr.wroc.pl/redmine/projects/toki/wiki)
- [Maca](http://www.nlp.pwr.wroc.pl/redmine/projects/libpltagger/wiki)
- [Wccl](http://www.nlp.pwr.wroc.pl/redmine/projects/joskipi/wiki)
- [Wcrft](http://www.nlp.pwr.wroc.pl/redmine/projects/wcrft/wiki)
- [Ner-Ws](http://www.nlp.pwr.wroc.pl/redmine/projects/ner-ws/wiki)
- [Liner2](http://nlp.pwr.wroc.pl/narzedzia-i-zasoby/narzedzia/liner2)

Most from the list (except Ubuntu and Morfeusz) are made by Grupa Technologii Językowych G4.19 Politechniki Wrocławskiej (Language Technologies Group G4.19 of Wroclaw Univeristy of Technology).

Base for this project is an instruction (in Polish) [here](http://nlp.pwr.edu.pl/redmine/projects/skrypt-instalujacy-narzedzia-nlp/wiki/Instalacja_krok_po_kroku#Instalacja-dodatkowych-modu%C5%82%C3%B3w)
