## Iniciando ##

https://docs.aws.amazon.com/

&xrArr; Os serviços AWS são compostos por regiões, zonas de disponibilidade (AZ), e zonas locais. Uma mesma região possui vários data centers, as zonas de disponibilidade, que garantem a disponibilidade dos serviços. Em caso de falha ou manutenção de uma AZ, as demais da mesma região podem suprir a demanda. As zonas locais servem para reduzir a latência entre os data centers e os clientes. 

Alguns serviços não estão disponíveis em todas regiões. 

https://aws.amazon.com/pt/about-aws/global-infrastructure/

### Boas Práticas ###

Ao iniciar uma conta na AWS algumas ações de boas práticas são recomendadas. 

&xrArr; Configurar autenticação de dois fatores (IAM)

&xrArr; Alterar política de senha

&xrArr; Criar uma conta administrativa 

Para a conta administrativa, deve ser criado também um grupo com as permissões de administrador, o qual essa conta pertencerá.

A criação desta conta se faz necessária uma vez que não é uma boa prática utilizar o usuário root.

---

### AWS CLI ###

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

---

## Amazon Elastic Compute Cloud (Amazon EC2) ##

https://aws.amazon.com/pt/ec2/

&xrArr; As instâncias EC2 são instâncias redimensionáveis de infraestrutura computacional. Funcionam como servidores computacionais. 

São 6 grupos, com diferentes objetivos de desempenho.

### Tipos de instâncias atuais de sexta geração (2024) ###

* Uso geral (Recursos balanceados, carga de RAM e CPU balanceadas e medianas): 

    M6a, M6g, M6gd, M6i, M6id, M6idn, M6in, M7a, M7g, M7gd, M7i, M7i-flex e T4g

* Otimizadas para computação (Maior uso de CPU, foco no processamento de dados): 

    C6a, C6g, C6gd, C6gn, C6i, C6id, C6in, C7a, C7g, C7gd, C7gn, C7i

* Otimizadas para memória (Maior uso de RAM): 
  
    R6a, R6g, R6gd, R6i, R6id, R6idn, R6in, R7a, R7g, R7gd, R7i, R7iz, X2gd, X2idn, X2iedn

* Otimizadas para armazenamento (Uso para bases de dados): 

    I4g, I4i, Im4gn, Is4gen

* Computação acelerada: 
    DL2q, G5g, Inf2, P5, Trn1, Trn1n

* Computação de alta performance: 
    Hpc6a, Hpc6id, Hpc7a, Hpc7g

https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/instance-types.html

&xrArr; No console web é possível ver todos os tipos e suas características, bem como filtrar de acordo com o desejado.

Serviços &rarr;  Computação &rarr; EC2 &rarr;  Instâncias &rarr; Tipos de instâncias

---

### Modalidades de contrato ###

&xrArr; O contrato por instâncias EC2 podem ser de 3 tipos.

_O armazenamento é sempre cobrado a parte, inclusive quando não está ocorrendo uso._

* On-Demand (padrão, todos cálculos de economia são feitos usando este método como base):

    Cobrado apenas o uso, ou seja, caso a máquina esteja desligada, não ocorrerão cobranças. A cobrança é feita por hora. Cada hora parcial é cobrada por segundo (a partir de 60 em máquinas linux) ou a hora completa para as demais.

* Reservadas:

    Pode ser feita de 3 formas, Padrão, que não permite alteração e possibilita até 72% de economia, Conversíveis, que permite alterações e até 54% de economia e Programadas, que permite realizar reservas por um curto de período de tempo. 

    Pagamento NoUpfront (sem pagamento no início de uso, faturamento mensal), Partitial Upfront (parte do pagamento no início) e Full Upfront (Pagamento total no início). 

    Contrato de 1 a 3 anos e não cancelável. A cobrança é feita independente do uso.

* Spot:

    Descontos de até 90%, porém pode ser interrompida a qualquer momento. A AWS informa 2 minutos antes da interrupção. Recomendada para aplicações tolerante a falhas, ambientes de testes e outros. Na contratação o valor máximo para pagamento pode ser definido e podem ser definidas instâncias por determinadas cargas de trabalho.

Calculadora de custos: https://calculator.aws/#/

* Savings Plan:

    Além dos faturamentos indicados, o Savings Plan é um modelo de preços flexíveis que oferece preços até 72% mais baixos em troca de um compromisso mensal de uso mínimo específico por um período de 1 a 3 anos. 

    Atende o serviço EC2 individualmente ou em com conjunto com o AWS Fargate e AWS Lambda (pacote Compute Savings Plan) e individualmente o serviço Amazon SageMaker (pacote Machine Learning Savings Plan). 

    Para usar é necessário habilitar o serviço Cost Explorer, um serviço que monitora e faz previsões de gastos, indicando formas otimizadas de uso dos serviços. Para seu funcionamento é necessário atentar que ele precisa de uma base para cálculo, portanto, o uso dos serviços já precisa ocorrer há um tempo. 

    Com o aumento da utilização, é possível contratar Planos de Poupança adicionais, aumentando o recurso disponível. 

    Os planos Compute e EC2 Instance se aplicam a instâncias que fazem parte dos clusters da Amazon EMR, EKS e ECS, porém cobrem apenas as instâncias EC2 são cobertas pelo plano.

---

### Iniciando uma instância ###

&xrArr; A inicialização de uma instância pode ser feita no console web. Serviços &rarr; EC2 &rarr; Instâncias &rarr; Executar uma instância.

&xrArr; É necessário selecionar uma imagem da AWS (AMI) para a máquina, o tipo de instância, criar um par de chaves (login, que deve ser baixado e armazenado para acesso), gerenciar informações de rede e armazenamento dentre outros. 

&xrArr; Este processo também pode ser feito via terminal.

`$ aws ec2 run-instances --image-id ami-xxxx --count 1 --instance-type 'tipo_instancia' --key-name 'nome_par_chave' --security-group-ids sg-xxxx --subnet-id subnet-xxxx`

Os valores de security-group-ids e subnet-id podem ser encontrados respectivamente em EC2 &rarr; Rede e Segurança &rarr; Grupos de Segurança e VPC &rarr; Nuvem Privada Virtual &rarr; Sub-redes.

&xrArr; Para acessar a instância é necessário utilizar o endereço público da máquina e adicionar o agente ssh (utilizando o arquivo de par de chaves baixado anteriormente). É necessário alterar a permissão do arquivo para privada, uma vez que sem esse procedimento todos acessos e usuários da máquina possuem permissão para o arquivo. O usuário a ser utilizado para acessar a máquina é o usuário ec2-user

`$ sudo chmod 400 'arquivo_chave_par'`

`$ ssh -i 'arquivo_chave_par' ec2-user@ip_publico`

Após a criação é possível nomear a instância.

`$ aws ec2 create-tags --resources 'id_instancia' --tags Key=Name,Value=´nome´`

&xrArr; Para listar as instâncias:

`aws ec2 describe-instances`

---

### Desligamento e Encerramento - Shutdown Behavior e Terminate Protection ###

&xrArr; Ao finalizar o uso de uma máquina criada ela pode ser interrompida ou encerrada. A máquina encerrada não pode ser utilizada novamente e tem os dados excluídos. Já a máquina interrompida pode ser reiniciada.

&xrArr; Na configuração de uma máquina é possível editar o comportamento no desligamento da máquina com a opção Shutdown Behavior, que define se a máquina irá interromper (stop) ou encerrar (terminate). 

&xrArr; Também é possível habilitar a proteção contra interrupção (Stop Protection), assim não é possível desligar a máquina no terminal. 

&xrArr; Outra proteção existente é a proteção contra encerramento (Termination Protection). 

&xrArr; Todas configurações podem ser feitas na criação da máquina e editadas na janela de ações da máquina. 

&xrArr; Os três recursos atuam no console web, porém caso a máquina esteja com o comportamento de encerrar no desligamento, ao desligar a máquina no terminal de uma máquina ligada a máquina virtual, a máquina ira encerrar e não poderá ser utilizada novamente. Portanto é ideal marcar a proteção contra encerramento e deixar o comportamento no desligamento como interromper. 

&xrArr; É possível remover instâncias via AWS CLI.

`$ aws ec2 terminate-instances --instance-ids 'id_instancia'`

---

### AMI's - Criação e compartilhamento ###

&xrArr; Além das imagens de sistemas operacionais já disponibilizadas pela AWS ou disponíveis no Marketplace, também é possível criar imagem de uma máquina feita pelo usuário. 

&xrArr; O processo é feito com a criação de uma instância normal, porém como já se espera que alguns recursos da máquina estejam pré-configurados de acordo com a personalização do usuário, podem ser inseridos comandos para inicialização da máquina através do campo Dados do Usuário no item de Detalhes Avançados. 

<img src="./media/user_data.png" width="500">

Os comandos acima indicam o terminal bash para executar os códigos que realizam a atualização do sistema e instalam e executam o servidor |Apache (httpd). Para funcionamento é necessário que o Grupo de Segurança esteja configurado para HTTP na Regra de Entrada através da porta 80. (EC2 &rarr; Grupos de Segurança). Após início da máquina com o servidor é possível testar digitando o endereço IP em um browser ou acessando a máquina via SSH no terminal e executar comandos para verificar a instalação e execução do serviço (necessário sudo) 

`$ rpm -qa | grep httpd`.

`$ systemctl status httpd`

&xrArr; Uma vez com a máquina criada com a configuração desejada, é possível criar a imagem no menu de ações da instância. Ações &rarr; Imagens e modelos &rarr; Criar imagem. Na tela de criação de imagem existe uma flag de não reinicialização. Máquinas criadas com imagens que reinicializam (flag desmarcada) iniciam mais rápido.

&xrArr; Após a criação é possível visualizar a AMI criada. EC2 &rarr; Imagens &rarr; AMIs.

&xrArr; Ao localizar a AMI e selecioná-la, basta marcar a opção de executar instância dessa imagem. Também é possível informar a imagem desejada no processo comum de instância. 
