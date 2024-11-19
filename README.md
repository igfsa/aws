# Iniciando #

https://docs.aws.amazon.com/

&xrArr; Os serviços AWS são compostos por regiões, zonas de disponibilidade (AZ), e zonas locais. Uma mesma região possui vários data centers, as zonas de disponibilidade, que garantem a disponibilidade dos serviços. Em caso de falha ou manutenção de uma AZ, as demais da mesma região podem suprir a demanda. As zonas locais servem para reduzir a latência entre os data centers e os clientes. 

Alguns serviços não estão disponíveis em todas regiões. 

https://aws.amazon.com/pt/about-aws/global-infrastructure/

## Boas Práticas ##

Ao iniciar uma conta na AWS algumas ações de boas práticas são recomendadas. 

&xrArr; Configurar autenticação de dois fatores (IAM)

&xrArr; Alterar política de senha

&xrArr; Criar uma conta administrativa 

Para a conta administrativa, deve ser criado também um grupo com as permissões de administrador, o qual essa conta pertencerá.

A criação desta conta se faz necessária uma vez que não é uma boa prática utilizar o usuário root.

---

## AWS CLI ##

https://docs.aws.amazon.com/pt_br/cli/latest/userguide/cli-chap-welcome.html

O AWS CLI é o aplicativo de linha de comando para gerenciamento da plataforma através da máquina local. 

&xrArr; Para instalar no Linux (todos comandos devem ser executados na mesma pasta)

Baixar e descompactar o arquivo 

`$ wget https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip -O awscliv2.zip` 
    
O parâmetro -O indica um nome  personalizado para o arquivo baixado.

`$ unzip awscliv2.zip`

`$ sudo ./aws/install`

&xrArr; É necessário criar um usuário AWS para acesso no CLI (IAM). 

Na criação deste usuário a flag de acesso para o console de gerenciamento deve estar desmarcada e o usuário deve ser incluído em um grupo de acordo com suas necessidades. 

Após a criação é necessário criar uma access key para o usuário, que será utilizada como parâmetro para conexão no AWS CLI

&xrArr; O ambiente utilizado no AWS CLI deve ser configurado via terminal. 

`$ aws configure`

Serão pedidos a access key, a secret access key, a zona (informar a zona indicada no console central) e o formato de saída (sugerido o JSON).

&xrArr; Para máquinas com mais de uma conexão é possível adicionar várias configurações utilizando perfis através do parâmetro profile para a função configure. Caso o parâmetro não seja informado o perfil atribuído será default.

`$ aws configure --profile ´nome´`

&xrArr; Após configurar a conexão pode ser testada.

`$ aws sts get-caller-identity`

Caso a máquina tenha mais de uma conexão pode ser utilizado o parâmetro default, assim como no comando configure.

`$ aws sts get-caller-identity --profile ´nome´`
