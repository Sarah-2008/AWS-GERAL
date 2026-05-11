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

Esse módulo mostra como criar uma vpc utilizando uma instância

## Objetivos do Laboratório
* Criar uma VPC personalizada
* Configurar sub-redes públicas e privadas
* Implementar conectividade com Internet Gateway e NAT Gateway
* Configurar regras de segurança com Security Groups
* Provisionar uma instância EC2 com servidor web
* 

### Recursos Criados
## * VPC
CIDR: 10.0.0.0/16
DNS habilitado
## * Sub-redes
*Tipo	CIDR	AZ
*Pública	10.0.0.0/24	us-east-1a
*Pública	10.0.2.0/24	us-east-1b
*Privada	10.0.1.0/24	us-east-1a
Privada	10.0.3.0/24	us-east-1b

## Segurança

Security Group: Web Security Group

## Tipo	Porta	Origem
* HTTP	80	0.0.0.0/0
* EC2 (Servidor Web)
* Nome: Web Server 1
*AMI: Amazon Linux 2023
*Tipo: t2.micro
*Sub-rede: Pública
*IP público: Ativado

## User Data Script
#!/bin/bash
dnf install -y httpd wget php mariadb105-server
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCLFO-2/2-lab2-vpc/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/
chkconfig httpd on
service httpd start

## Acesso à Aplicação

* ## Após a inicialização da instância:

* Copiar o Public IPv4 DNS
* Acessar via navegador:
* http://<public-dns>

## Resultado: 
Página web com informações da instância exibida com sucesso.

---

# Códigos para usar quando ouver que fazer uma API com uma instância (linux):
## Atualizar e instalar Node.js 18
* curl -sL https://rpm.nodesource.com/setup_18.x | sudo bash -
* sudo yum install -y nodejs

## Criar pasta do projeto
* mkdir lab-livros && cd lab-livros
* npm init -y
* npm install express
* nano (nome da pasta)

## Salvar o pojeto em uma instância seria assim:
* cntrl+O enter

## Voltar para o terminal
* ctrl x

## Código para programar uma api exemplo:
<img width="1572" height="571" alt="image" src="https://github.com/user-attachments/assets/46784a4e-b0ef-4585-9246-3a7a1b549edf" />

---

# Lab 4: Trabalhando com EBS

## Visão Geral
Este laboratório demonstra como utilizar o Amazon EBS com instâncias EC2.

Você irá aprender a:
- Criar um volume EBS
- Anexar a uma instância EC2
- Criar um sistema de arquivos
- Criar snapshots (backup)
- Restaurar volumes a partir de snapshots

## O que é o Amazon EBS?

O Amazon EBS é um armazenamento persistente para instâncias EC2.

### Características:
- Persistente (independente da instância)
- Alta disponibilidade
- Alta confiabilidade
- Suporte a snapshots (backup)
- Tamanhos de 1 GB até 16 TB

## 1. Criar Volume EBS

1. Acesse **EC2 > Volumes**
2. Clique em **Create Volume**

Configuração:
- Tipo: `gp2`
- Tamanho: `1 GiB`
- Availability Zone: mesma da instância

Tag:
- Key: `Name`
- Value: `My Volume`

## 2. Anexar Volume

1. Selecione **My Volume**
2. Actions → **Attach Volume**
3. Instância: `Lab`
4. Device: `/dev/sdb`

##  3. Conectar na Instância

1. EC2 → Instances
2. Selecione a instância
3. Clique em **Connect**
4. Use **Session Manager**

```bash
sudo su -l ec2-user
```

## 4. Configurar Sistema de Arquivos

Ver discos:
```bash
df -h
```

Criar sistema de arquivos:
```bash
sudo mkfs -t ext3 /dev/sdb
```

Criar diretório:
```bash
sudo mkdir /mnt/data-store
```

Montar volume:
```bash
sudo mount /dev/sdb /mnt/data-store
```

Automatizar montagem:
```bash
echo "/dev/sdb /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

Verificar:
```bash
df -h
```

Criar arquivo:
```bash
sudo sh -c "echo algum texto foi escrito > /mnt/data-store/file.txt"
```

Ver conteúdo:
```bash
cat /mnt/data-store/file.txt
```

## 5. Criar Snapshot

1. EC2 → Volumes
2. Selecione **My Volume**
3. Actions → **Create Snapshot**

Tag:
- Name: `My Snapshot`

## 6. Deletar Arquivo

```bash
sudo rm /mnt/data-store/file.txt
ls /mnt/data-store/
```

## 7. Restaurar Snapshot

### Criar novo volume:
1. EC2 → Snapshots
2. Selecione **My Snapshot**
3. Clique em **Create Volume**

Configuração:
- Mesma AZ
- Nome: `Restored Volume`

### Anexar volume restaurado:
1. EC2 → Volumes
2. Selecione **Restored Volume**
3. Attach:
   - Instância: Lab
   - Device: `/dev/sdc`

### Montar volume restaurado:

```bash
sudo mkdir /mnt/data-store2
sudo mount /dev/sdc /mnt/data-store2
```

Verificar arquivo:
```bash
ls /mnt/data-store2/
```

## Observação

Snapshots são armazenados no Amazon S3 e permitem recuperar dados mesmo após exclusão do volume original.

---

# Laboratório 5 - Amazon RDS com Aplicação Web

##  Objetivo
Neste laboratório foi criada uma instância de banco de dados gerenciada utilizando o Amazon RDS e realizada a integração com uma aplicação web hospedada em uma instância EC2.

# Etapa 1 - Criar Security Group do Banco

## Configurações

| Campo | Valor |
|---|---|
| Nome | DB Security Group |
| Descrição | Permit access from Web Security Group |
| VPC | Lab VPC |

## Regra de Entrada

| Tipo | Porta | Origem |
|---|---|---|
| MySQL/Aurora | 3306 | Web Security Group |

# Etapa 2 - Criar DB Subnet Group

## Configurações

| Campo | Valor |
|---|---|
| Nome | DB-Subnet-Group |
| Descrição | DB Subnet Group |
| VPC | Lab VPC |

## Sub-redes Selecionadas

```text
10.0.1.0/24
10.0.3.0/24
```

## Availability Zones

```text
us-east-1a
us-east-1b
```

# Etapa 3 - Criar Instância RDS

## Configuração do Banco

| Campo | Valor |
|---|---|
| Engine | MySQL |
| Template | Dev/Test |
| Disponibilidade | Multi-AZ |
| DB Identifier | lab-db |
| Usuário | main |
| Senha | lab-password |

## Classe da Instância

```text
db.t3.micro
```

## Armazenamento

| Campo | Valor |
|---|---|
| Tipo | General Purpose SSD |
| Tamanho | 20 GB |

## Conectividade

| Campo | Valor |
|---|---|
| VPC | Lab VPC |
| Security Group | DB Security Group |

## Configuração Adicional

| Campo | Valor |
|---|---|
| Initial Database Name | lab |
| Backups Automáticos | Desativado |
| Criptografia | Desativada |

# Etapa 4 - Conectar Aplicação Web ao Banco

## Dados de Conexão

```text
Endpoint: lab-db.xxxx.us-east-1.rds.amazonaws.com
Database: lab
Username: main
Password: lab-password
```
