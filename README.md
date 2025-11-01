# ☕️ Roteamento de Failover com Amazon Route 53

### 🌩️ Projeto AWS — Escola da Nuvem  
**Instrutor:** Professor Victor  
**Autora:** Carine Almeida  
**Duração:** ~45 minutos  
**Nível:** Intermediário  
**Serviços AWS Utilizados:** Route 53, EC2, SNS, CloudFormation  

---

## 📘 Descrição do Projeto

Este projeto demonstra como configurar **roteamento de failover no Amazon Route 53** para manter a **alta disponibilidade** de um aplicativo web.  

A aplicação escolhida foi o **site do Café ☕️**, hospedado em duas instâncias **Amazon EC2** em **Zonas de Disponibilidade diferentes**.  

A configuração do **Amazon Route 53** garante que:
- Se o **servidor principal** ficar indisponível,  
- O tráfego seja automaticamente redirecionado para o **servidor secundário**  
- E o sistema envie **alertas por e-mail** via **Amazon SNS**.  

---

## 🧠 Conceitos Aprendidos

| Conceito | Descrição |
|-----------|-----------|
| **Alta Disponibilidade (HA)** | Capacidade de um sistema permanecer funcional mesmo diante de falhas. |
| **Amazon Route 53** | Serviço DNS escalável e altamente disponível da AWS. |
| **Health Checks** | Verificações automáticas de integridade de endpoints HTTP. |
| **Failover Routing** | Estratégia de roteamento DNS que alterna entre recursos primários e secundários. |
| **Amazon SNS** | Serviço de mensageria usado para enviar alertas automáticos. |
| **Multi-AZ Deployment** | Implantação redundante em múltiplas zonas de disponibilidade para tolerância a falhas. |

---

## 🧩 Arquitetura do Projeto


📷 **Descrição:**
- **Café 1**: instância EC2 principal, rodando em `us-west-2a`
- **Café 2**: instância EC2 secundária, rodando em `us-west-2b`
- **Route 53**: realiza health check e roteamento DNS
- **SNS**: envia alertas quando o site primário estiver inativo  

---

## 🎯 Objetivos do Laboratório

- ✅ Criar e configurar uma **verificação de integridade (Health Check)** no Route 53  
- ✅ Configurar **roteamento de failover** entre duas instâncias EC2  
- ✅ Configurar **notificações por e-mail** via SNS  
- ✅ Simular falha no servidor primário e verificar failover automático  

---

## ⚙️ Etapas do Projeto

### **1️⃣ Confirmar os sites do Café**
- Duas instâncias EC2 já criadas:  
  - `CafeInstance1` → Zona de Disponibilidade **us-west-2a**  
  - `CafeInstance2` → Zona de Disponibilidade **us-west-2b**  
- Acesse cada URL para confirmar que o aplicativo está funcionando.  
- Exemplo:

- 
---

### **2️⃣ Configurar a Verificação de Integridade (Health Check)**

- **Nome:** `Primary-Website-Health`
- **Tipo:** Endpoint HTTP  
- **Endereço IP:** público da instância `CafeInstance1`
- **Caminho:** `/cafe`
- **Intervalo de verificação:** 10 segundos  
- **Falhas permitidas:** 2  
- **Notificação:**  
- Criar novo tópico SNS: `Primary-Website-Health`  
- Inserir e-mail pessoal e **confirmar inscrição via link do e-mail**  

---

### **3️⃣ Criar os Registros DNS no Route 53**

#### 🔸 Registro Primário
| Campo | Valor |
|--------|--------|
| Nome do registro | `www` |
| Tipo | A (IPv4) |
| Valor | IP da instância Café 1 |
| Política de roteamento | Failover |
| Tipo de registro | Primário |
| Health Check | Primary-Website-Health |

#### 🔸 Registro Secundário
| Campo | Valor |
|--------|--------|
| Nome do registro | `www` |
| Tipo | A (IPv4) |
| Valor | IP da instância Café 2 |
| Política de roteamento | Failover |
| Tipo de registro | Secundário |
| Health Check | *(não aplicável)* |

---

### **4️⃣ Testar o Failover**

1. Acesse o site principal:

2. Confirme que está rodando a partir da **AZ primária**.  
3. No Console EC2, pare a instância **CafeInstance1**.  
4. Aguarde o Health Check mudar para **Unhealthy**.  
5. Atualize o site no navegador — ele agora deve carregar a instância **Café 2** (secundária).  
6. Verifique seu e-mail — um alerta SNS deve ter sido recebido.  

---

## 📬 Resultados

- ✅ Failover automático entre Zonas de Disponibilidade  
- ✅ Alerta SNS recebido por e-mail  
- ✅ Site do Café disponível mesmo após falha do servidor primário  
- ✅ Arquitetura resiliente e tolerante a falhas  

---

## ☁️ Tecnologias Utilizadas

| Serviço | Função |
|----------|--------|
| **Amazon EC2** | Hospedagem das instâncias do site Café |
| **Amazon Route 53** | Roteamento DNS e failover |
| **Amazon SNS** | Envio de alertas automáticos |
| **AWS CloudFormation** | Criação automatizada da infraestrutura |
| **LAMP Stack (Linux, Apache, MySQL, PHP)** | Ambiente do aplicativo web |

---

## 🧩 Estrutura de Pastas Sugerida



