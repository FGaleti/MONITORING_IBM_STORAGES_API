# 📊 Zabbix Template: IBM Storage Monitor via REST API

Um template completo e avançado para Zabbix focado no monitoramento de Storages IBM nativamente via **API REST**. Desenvolvido para eliminar a dependência de scripts externos no sistema operacional e contornar as limitações do SNMP tradicional, entregando dados granulares de hardware, capacidade e conectividade. 

Acompanha um dashboard interativo para Grafana focado em observabilidade em tempo real.

## 🖧 Equipamentos Compatíveis
Este template foi desenvolvido consumindo os endpoints da API REST `/rest/v1/` do IBM Storage Virtualize, tornando-o amplamente compatível com o ecossistema de blocos da IBM. 

Testado e homologado para:
* **IBM FlashSystem Series:** FS5000, FS5015, FS5035, FS5200, FS5300, FS7200, FS7300, FS9200, FS9500.
* **IBM SAN Volume Controller (SVC).**
* **IBM Storwize Series:** V5000, V5100, V7000 (Requer firmware com suporte à API REST v1).

## ✨ Recursos e Descobertas (LLD)
O template utiliza requisições HTTP nativas do Zabbix (via JavaScript) para autenticar e coletar dados da API do Storage. Ele descobre e monitora automaticamente:

* **📦 Storage Pools:** Capacidade total, usada, livre, real e virtual, além do status operacional.
* **💽 Volumes (VDisks):** Mapeamento de capacidade, snapshots e status de acesso lógico.
* **🔌 Drives (MDisks):** Capacidade, tecnologia e saúde física dos discos.
* **🖥️ Hosts:** Status de comunicação, portas ativas e cluster.
* **🏗️ Enclosures:** Monitoramento global do chassi, inventário (Serial Number) e refrigeração (Fans).
* **🧠 Canisters (Controladoras):** Status de redundância e tipo dos nós.
* **⚡ PSUs (Fontes de Alimentação):** Monitoramento de entrada de energia e status de falha de hardware.

## 🚨 Triggers (Alertas Inteligentes)
O template já vem configurado com gatilhos críticos para operação contínua:
* Alerta de esgotamento de capacidade física no Pool (< 500GB livres).
* Perda de redundância de controladoras (Canister Offline) ou energia (PSU Offline).
* Falha de comunicação com Hosts (0 portas ativas).
* Discos (Drives) em falha ou degradados.

## ⚙️ Pré-requisitos
* Zabbix 6.2 ou superior (testado na versão 6.2).
* Storage IBM com a API REST v1 habilitada e acessível pela rede do Zabbix Server/Proxy.
* Usuário no Storage com permissão de leitura (Monitor).

## 🚀 Instalação e Configuração no Zabbix

1.  Faça o download do arquivo `zabbix/zabbix_ibm_storage_api.yaml`.
2.  No Zabbix, vá em **Data collection > Templates** e clique em **Import**.
3.  Vincule o template `TEMPLATE API STORAGE FS` ao host do seu Storage.
4.  No host, configure as seguintes **Macros**:
    * `{$API.URL}`: URL base da API. 
    * `{$API.USER}`: Seu usuário da API.
    * `{$API.PASS}`: Sua senha da API.

## 📈 Integração com Grafana
Para uma visualização gerencial:
1.  Garanta que o plugin do Zabbix no Grafana (Alexander Zobnin) está configurado.
2.  Vá em **Dashboards > Import** no Grafana.
3.  Faça o upload do arquivo `grafana/ibm_storage_dashboard.json`.
4.  Selecione o seu Data Source do Zabbix e aproveite!

## 📸 Preview do Dashboard

<img width="1280" height="571" alt="image" src="https://github.com/user-attachments/assets/1a6c6dca-8804-4b53-8b6c-fc9547bca684" />


---
*Desenvolvido com ☕ e foco em alta disponibilidade.*
