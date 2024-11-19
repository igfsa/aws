## VPC ##

### Security Groups ###

&rarr; Security Groups atuam com firewalls virtuais que controlam o tráfego entre recursos AWS. Controla tanto o tráfego de entrada quanto de saída das instâncias, dessa maneira verifica quem pode ou não acessar um recurso e o que está saindo.

&rarr; Todas as regras são criadas como PERMISSIVAS. 

&rarr; Por padrão os Security Groups permitem todo tráfego de saída. Atenção para possíveis falhas de vulnerabilidade.

&rarr; Cada regra deve possuir os seguintes componentes: 

* Protocolo
* Intervalo de portas
* Tipo de código ICMP
* Origem ou destino 
* Descrição (Opcional) 

