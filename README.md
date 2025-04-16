<h1 align="center">Atividade Prática 3 | Compass UOL</br>
Projeto de Migração com AWS & Kubernetes</h1>

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=aws,kubernetes" />
  </a>
</p>

</br>

## Tecnologias:
- AWS
- Kubernetes

<br>

## Objetivos:
- Realizar uma migração Lift-and-Shift da seguinte infraestrutura **on-premise** para a nuvem:
  - 01 servidor - Banco de Dados MySQL (500GB de dados, 10Gb de RAM, 3 Core CPU);
  - 01 servidor - Frontend utilizando React (5GB de dados, 2Gb de RAM, 1 Core CPU);
  - 01 servidor - Backend com 3 APIs, com o Nginx servindo de balanceador de carga e que armazena estáticos (5GB de dados, 4Gb de RAM, 2 Core CPU).
- Após a migração, modernizar esta infraestrutura AWS para a implementação de um ambiente **Kubernetes**, seguindo os seguintes requisitos:
  - Banco de dados gerenciado (PaaS e Multi AZ);
  - Backup de dados;
  - Sistema para persistência de objetos (imagens, vídeos etc);
  - Segurança.

<br>

## Índice:
- [Passo 1. Migração Lift-and-Shift](#passo-1-migração-lift-and-shift)
  - [I. Atividades Necessárias para a Migração](#i-atividades-necessárias-para-a-migração)
  - [II. Ferramentas Utilizadas](#ii-ferramentas-utilizadas)
  - [III. Diagrama da Infraestrutura na AWS](#iii-diagrama-da-infraestrutura-na-aws)
  - [IV. Requisitos de Segurança](#iv-requisitos-de-segurança)
  - [V. Processo de Backup](#v-processo-de-backup)
  - [VI. Custo da Infraestrutura na AWS](#vi-custo-da-infraestrutura-na-aws)
- [Passo 2. Modernização com Kubernetes](#passo-2-modernização-com-kubernetes)
  - [I. Atividades Necessárias para a Migração](#i-atividades-necessárias-para-a-migração-1)
  - [II. Ferramentas Utilizadas](#ii-ferramentas-utilizadas-1)
  - [III. Diagrama da infraestrutura na AWS](#iii-diagrama-da-infraestrutura-na-aws-1)
  - [IV. Requisitos de Segurança](#iv-requisitos-de-segurança-1)
  - [V. Processo de Backup](#v-processo-de-backup-1)
  - [VI. Custo da Infraestrutura na AWS](#vi-custo-da-infraestrutura-na-aws-1)
- [Conclusão](#conclusão)
  - [Benefícios Esperados](#benefícios-esperados)

<br>

## Passo 1. Migração Lift-and-Shift

- Devemos replicar a infraestrutura atual na AWS, garantindo a continuidade das operações do e-commerce durante a migração e, por fim, preparar o ambiente para a modernização na Etapa 2 (Kubernetes).


<br>

### I. Atividades Necessárias para a Migração
---

- **Análise e Planejamento**: mapeamento da infraestrutura atual e definição de requisitos;
- **Configuração do Ambiente AWS**: criação do VPC (Virtual Private Cloud) e configuração de Security Groups;
- **Migração dos Servidores**: migração do frontend (React), migração do backend (APIs) e configuração do Elastic Load Balancer (ELB);
- **Migração do Banco de Dados**: migração do MySQL para o Amazon RDS;
- **Configuração de Segurança**: AWS WAF (Web Application Firewall) e AWS Shield Standard;
- **Configuração de Backup**: AWS Backup e Versionamento no S3;
- **Testes e Validação**: testes de carga, testes funcionais e monitoramento com o Amazon CloudWatch;
- **Corte (Cutover)**: atualização dos registros DNS e monitoramento pós-migração.

<br>

### II. Ferramentas Utilizadas
---

- **Serviço de Migração:** AWS Server Migration Service (SMS);
- **Rede e Segurança:** VPC, AWS WAF, IAM e AWS Shield Standard;
- **Banco de Dados:** Amazon RDS Multi-AZ;
- **Balanceamento de Carga:** ALB (Application Load Balancer);
- **DNS e CDN:** Route 53 e AWS CloudFront;
- **Monitoramento e Logging:** Amazon CloudWatch e AWS Backup;
- **Armazenamento:** Amazon S3;
- **Ferramentas Auxiliares:** AWS CLI (Command Line Interface).

<br>

### III. Diagrama da Infraestrutura na AWS
---

<br>

![as-is-infra](/images/as-is_infra.png)

<br>

### IV. Requisitos de Segurança
---

1. **IAM (Identity and Access Management)**:
   - Criação de usuários e roles com permissões mínimas necessárias.
   - Uso de políticas de segurança restritivas.

2. **Grupos de Segurança (Security Groups)**:
   - Configuração de regras de firewall para permitir apenas tráfego necessário.
   - Bloqueio de portas não utilizadas.

3. **Proteção Contra Ataques**:
   - **AWS WAF**: Para proteção contra vulnerabilidades web.
   - **AWS Shield Standard**: Para proteção contra DDoS.

<br>

### V. Processo de Backup
---

1. **Banco de Dados (RDS)**:
   - Backups automáticos diários com retenção de 7 dias.
   - Snapshots manuais antes de grandes atualizações.

2. **Arquivos Estáticos (S3)**:
   - Versionamento habilitado no bucket S3 para manter histórico de alterações.
   - Configuração de Lifecycle Policies para armazenamento de backups em S3 Glacier.

3. **Instâncias EC2**:
   - Backup automatizado usando o AWS Backup.

<br>

### VI. Custo da Infraestrutura na AWS
---

<br>

<table>
  <thead>
    <tr align="left">
      <th>⚙️ Serviço</th>
      <th>💵 Custo mensal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Amazon CloudWatch</td>
      <td>$20,05</td>
    </tr>
    <tr>
      <td>Amazon EC2</td>
      <td>$64,15</td>
    </tr>
    <tr>
      <td>Amazon RDS for MySQL</td>
      <td>$1.028,99</td>
    </tr>
    <tr>
      <td>Amazon Route 53</td>
      <td>$15,50</td>
    </tr>
    <tr>
      <td>Amazon Simple Storage Service (S3)</td>
      <td>$3,30</td>
    </tr>
    <tr>
      <td>Amazon Virtual Private Cloud (VPC)</td>
      <td>$82,00</td>
    </tr>
    <tr>
      <td>AWS Backup</td>
      <td>$0,00</td>
    </tr>
    <tr>
      <td>AWS Web Application Firewall (WAF)</td>
      <td>$26,00</td>
    </tr>
    <tr>
      <td>Elastic Load Balancing (ELB)</td>
      <td>$16,83</td>
    </tr>
  </tbody>
   <tfoot>
    <tr>
      <td><strong>Total</strong></td>
      <td>$1.256,82 USD</td>
    </tr>
  </tfoot>
</table>

<br>

## Passo 2. Modernização com Kubernetes

- A modernização envolve **migrar** a aplicação existente para **Kubernetes** no Amazon EKS e configurar os serviços auxiliares.

<br>

### I. Atividades Necessárias para a Migração
---

- **Análise e Planejamento:** Levantar requisitos de infraestrutura, segurança e escalabilidade.  
- **Criação do Cluster EKS:** Provisionar e configurar o Amazon EKS para ambiente de produção e desenvolvimento.  
- **Containerização das Aplicações:** Criar Dockerfiles, ajustar aplicações para rodar em contêineres e armazená-los no Amazon ECR.  
- **Configuração de Rede:** Definir subnets, NAT Gateway, Internet Gateway e Security Groups.  
- **Deploy de Serviços:** Criar manifests Kubernetes (Deployment, Service, Ingress) para frontend, backend e APIs.  
- **Banco de Dados:** Configurar RDS Multi-AZ para garantir alta disponibilidade.  
- **Balanceamento de Carga:** Utilizar ALB (Application Load Balancer) para distribuir o tráfego.  
- **Segurança:** Configurar IAM, AWS WAF, AWS KMS, AWS Shield, Secrets Manager e monitoramento com CloudWatch.  
- **Backup e Disaster Recovery:** Definir estratégias de backup no AWS Backup e snapshots no RDS.  
- **Testes e Validação:** Testar desempenho, segurança e falhas antes de migrar o tráfego definitivamente.  

<br>

### II. Ferramentas Utilizadas
---

- **Orquestração de Contêineres:** Amazon EKS;
- **Gerenciamento de Contêineres:** Docker e Amazon ECR;
- **Rede e Segurança:** VPC, Security Groups, IAM, AWS WAF, AWS KMS, AWS Shield e AWS Secrets Manager;
- **Banco de Dados:** Amazon RDS Multi-AZ;
- **Balanceamento de Carga:** ALB (Application Load Balancer);
- **DNS e CDN:** Route 53 e AWS CloudFront;
- **Monitoramento e Logging:** Amazon CloudWatch, AWS Backup;
- **Armazenamento:** Amazon S3;
- **Ferramentas Auxiliares:** AWS Organizations.

<br>

### III. Diagrama da infraestrutura na AWS
---

<br>

![kubernetes-infra](/images/kubernetes_infra.png)

<br>

### IV. Requisitos de Segurança 
---

- **Controle de Acesso:** IAM com permissões mínimas necessárias para cada serviço.  
- **Proteção Contra Ataques:** AWS WAF para filtragem de tráfego malicioso, AWS Shield contra DDoS.  
- **Gerenciamento de Segredos:** AWS Secrets Manager para credenciais e chaves sensíveis.  
- **Redes Seguras:** Uso de subnets privadas para banco de dados e backend, acesso a partir de VPNs.  
- **Monitoramento e Logging:** CloudWatch para logs e métricas.
- **Criptografia:** Dados criptografados em trânsito (TLS) e em repouso (KMS no RDS e S3).
- **Backup e Disaster Recovery:** AWS Backup e snapshots automáticos no RDS.  

<br>

### V. Processo de Backup
---

- **Banco de Dados:** Snapshots automáticos no Amazon RDS com retenção configurável.  
- **Armazenamento de Objetos:** Amazon S3 versionado e com políticas de ciclo de vida.  
- **Volumes de Armazenamento:** Backup via AWS Backup para snapshots de EBS.  
- **Configuração e Logs:** Logs armazenados no CloudWatch e replicação para S3.  

<br>

### VI. Custo da Infraestrutura na AWS
---

<br>

<table>
  <thead>
    <tr align="left">
      <th>⚙️ Serviço</th>
      <th>💵 Custo mensal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Amazon CloudWatch</td>
      <td>$20,05</td>
    </tr>
    <tr>
      <td>Amazon EC2</td>
      <td>$96,23</td>
    </tr>
    <tr>
      <td>Amazon Elastic Container Registry (ECR)</td>
      <td>$2,50</td>
    </tr>
    <tr>
      <td>Amazon EKS</td>
      <td>$146,00</td>
    </tr>
    <tr>
      <td>Amazon RDS for MySQL</td>
      <td>$1.541,11</td>
    </tr>
    <tr>
      <td>Amazon Route 53</td>
      <td>$0,90</td>
    </tr>
    <tr>
      <td>Amazon Simple Storage Service (S3)</td>
      <td>$3,30</td>
    </tr>
    <tr>
      <td>Amazon Virtual Private Cloud (VPC)</td>
      <td>$452,00</td>
    </tr>
    <tr>
      <td>AWS Backup</td>
      <td>$0,00</td>
    </tr>
    <tr>
      <td>AWS IAM Access Analyzer</td>
      <td>$18,00</td>
    </tr>
    <tr>
      <td>AWS Key Management Service (KMS)</td>
      <td>$11,00</td>
    </tr>
    <tr>
      <td>AWS Secrets Manager</td>
      <td>$8,00</td>
    </tr>
    <tr>
      <td>AWS Web Application Firewall (WAF)</td>
      <td>$26,00</td>
    </tr>
    <tr>
      <td>Elastic Load Balancing (ELB)</td>
      <td>$33,65</td>
    </tr>
  </tbody>
   <tfoot>
    <tr>
      <td><strong>Total</strong></td>
      <td>$2.358,74 USD</td>
    </tr>
  </tfoot>
</table>

<br>

## Conclusão

A migração e modernização da infraestrutura do nosso e-commerce para a AWS representam um *marco estratégico* para garantir escalabilidade, segurança e alta disponibilidade.

Na primeira etapa **"Lift-and-Shift"**, replicamos a infraestrutura on-premise na AWS de forma rápida e segura, utilizando serviços como **EC2**, **RDS Multi-AZ**, **S3**, **ELB**, **WAF**, **Shield** e **Route 53**. Isso nos permitiu reduzir o risco de downtime, melhorar o desempenho e preparar o ambiente para a próxima fase. <br>
Na segunda etapa, com a **"Modernização para Kubernetes no Amazon EKS"**, avançaremos ainda mais, garantindo escalabilidade automática, resiliência, segurança reforçada e eficiência operacional.

### Benefícios Esperados
- *Alta disponibilidade*: Com o RDS Multi-AZ e o ELB, garantimos que o site esteja sempre no ar, mesmo durante falhas ou ataques.
- *Segurança robusta*: Proteção contra DDoS, injeções de SQL, XSS e outras ameaças comuns.
- *Custo otimizado*: Utilizamos instâncias adequadas e estratégias de backup para evitar gastos desnecessários.
- *Preparação para o futuro*: A arquitetura na AWS e o uso de Kubernetes nos permitem escalar rapidamente e adotar novas tecnologias.
