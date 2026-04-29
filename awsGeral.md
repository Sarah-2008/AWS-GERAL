# AWS-GERAL

## Introdução à AWS (Amazon Web Services)
### 📌 O que é a AWS?

* ## A Amazon Web Services (AWS) é uma plataforma de computação em nuvem criada pela Amazon que oferece uma ampla variedade de serviços, como:

Armazenamento de dados
Computação (servidores virtuais)
Bancos de dados
Redes
Inteligência artificial
Segurança

Esses serviços são disponibilizados pela internet, permitindo que empresas e desenvolvedores utilizem infraestrutura de TI sem precisar investir em hardware físico.

🌍 Infraestrutura Global da AWS

A AWS possui uma infraestrutura global altamente distribuída, composta por:

🗺️ Regiões (Regions)

As Regiões são áreas geográficas separadas onde a AWS mantém seus data centers.

Exemplos:

América do Sul (São Paulo)
América do Norte (Virgínia)
Europa (Irlanda)

Cada região é isolada das outras, garantindo maior segurança e estabilidade.

🏢 Zonas de Disponibilidade (Availability Zones - AZs)

Cada região contém várias Zonas de Disponibilidade, que são:

Data centers fisicamente separados
Conectados por redes de alta velocidade
Projetados para alta disponibilidade e tolerância a falhas

💡 Isso significa que, se uma zona falhar, outras podem continuar operando normalmente.

💰 Economia da Nuvem
⚙️ Modelo Pay-as-you-go

A AWS utiliza o modelo “pague pelo uso” (pay-as-you-go), onde você:

Paga apenas pelos recursos utilizados
Não precisa de investimento inicial
Pode escalar recursos conforme a demanda

Exemplo:

Usou um servidor por 2 horas → paga apenas por 2 horas
Armazenou 10 GB → paga apenas por esse espaço
📈 Economia de Escala

A AWS consegue oferecer preços competitivos graças à economia de escala, que funciona assim:

A Amazon opera data centers gigantescos ao redor do mundo
Quanto mais clientes utilizam a plataforma, menor o custo por unidade de recurso
Parte dessa redução de custo é repassada aos clientes

👉 Mesmo com preços reduzidos, a empresa gera lucro devido ao alto volume de usuários e uso contínuo dos serviços.

---

### Básico do Amazon EC2

Criar e configurar uma instância
Monitorar desempenho
Ajustar segurança
Redimensionar recursos
Testar proteções e limites

## Principais atividades
* 1. Criar uma instância EC2
Nome: Web Server
AMI: Amazon Linux 2023
Tipo: t2.micro
Configuração de rede na VPC do laboratório
Criar grupo de segurança sem regras iniciais
Ativar proteção contra encerramento
Adicionar script (user data) para:
Instalar Apache
Iniciar servidor web
Criar página HTML simples
* 2. Monitorar a instância
Verificar status (2/2 checks)
Acompanhar métricas no CloudWatch
Consultar:
Logs do sistema
Captura de tela da instância
* 3. Liberar acesso ao servidor web
Problema: site não abre inicialmente
Solução:
Editar grupo de segurança
Liberar porta HTTP (80) para qualquer IP
Resultado: página “Hello From Your Web Server!” aparece
* 4. Redimensionar recursos
Parar a instância
Alterar:
Tipo: de t2.micro → t2.small
Disco: de 8 GB → 10 GB
Reiniciar a instância
* 5. Explorar limites do EC2
Usar Service Quotas
Ver limites de instâncias por região
Entender restrições da conta AWS
* 6. Testar proteção contra interrupção
Tentativa de parar a instância falha (proteção ativa)
Desativar proteção
Parar instância com sucesso

## Duração
Aproximadamente 35 minutos

## Conclusão

Criar e configurar servidores na nuvem
Controlar acesso com segurança
Monitorar desempenho
Ajustar capacidade conforme necessidade
Evitar erros com proteções

---

### AWS LAMBDA

Criar uma função no AWS Lambda que automaticamente interrompe uma instância do Amazon EC2 a cada minuto. Para isso, a função usará permissões definidas por uma role do IAM.

## Principais etapas:

* Criar a função Lambda
* Nome: myStopinator
* Runtime: Python 3.11
* Usar a role existente: myStopinatorRole
* Configurar o gatilho
* Criar uma regra no EventBridge chamada everyMinute
* Usar a expressão rate(1 minute) para executar a função a cada minuto
* Editar o código da função
* Colar um script em Python que usa o boto3 para parar instâncias EC2
* Substituir:
* Região (<REPLACE_WITH_REGION>)
* ID da instância (<REPLACE_WITH_INSTANCE_ID>)
* Implantar e monitorar
* Salvar e implantar a função
* Acompanhar execuções e erros na aba “Monitorar”
* Verificar funcionamento
* Confirmar no EC2 se a instância foi parada
* Se reiniciar a instância, ela será parada novamente em até 1 minuto

## Objetivo:
* Automatizar o desligamento de uma instância EC2 usando Lambda + EventBridge, sem precisar de servidor dedicado.

---

### VPC E EC2
