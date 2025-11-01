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
