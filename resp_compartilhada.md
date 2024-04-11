# Responsabilidade compartilhada #

A AWS utiliza o modelo de responsabilidade compartilhada para gerenciamento de segurança de seus serviços. Ou seja, a AWS e o cliente possui uma parcela de responsabilidade no processo de segurança. 

Cabe a AWS garantir a segurança dos locais e dispositivos físicos onde os servidores estão instalados, além de disponibilidade e conexão dos serviços.

Já o cliente é responsável por garantir a segurança dos recursos hospedados nos serviços da amazon. Ou seja, os sistemas, regras de segurança de um servidor hospedado, criptografia, acessos e outros são responsabilidade do cliente. 

## Base geral do modelo ##

<img src="/media/resp_compartilhada_1.png" width="500">

## Exemplo do modelo em ambientes diferentes (on premisses, IaaS, PaaS e SaaS) ##

<img src="/media/resp_compartilhada_2.png" width="500">

## Exemplo do modelo em diferentes serviços AWS ##

<img src="/media/resp_compartilhada_3.png" width="500">

Uma observação interessante é a proporção inversa entre controle e segurança por parte do cliente. Plataformas em IaaS possuem maior controle por parte do usuário, mas consequentemente o cliente tem maior responsabilidade compartilhada, já soluções SaaS, possuem menor controle com mais responsabilidade de segurança por parte da AWS.
