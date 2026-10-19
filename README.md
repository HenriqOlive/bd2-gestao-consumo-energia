 Sistema Inteligente de Gestão e Monitoramento de Consumo de Energia

Nome oficial da solução:** Sistema Inteligente de Gestão e Monitoramento de Consumo de Energia

Nome dos Integrantes: Leonardo Santos/Muriel Masseo/Henrique Olivera/Rodrigo Yudi/Arthur Bastos

Ling dos Gits: https://github.com/HenriqOlive // https://github.com/arthurbastos-02 // https://github.com/zeolihn // https://github.com/rodrigoyudisec

##  Descrição

O gerenciamento ineficiente de energia elétrica, a carência de monitoramento em tempo real e a complexidade na aplicação de regras tarifárias dinâmicas geram desperdícios para consumidores e distribuidoras.

Este projeto propõe uma plataforma integrada capaz de gerenciar a infraestrutura de medição inteligente (*smart meters*), controlar perfis cadastrais e geográficos de unidades consumidoras e processar telemetrias de consumo de forma automatizada[cite: 3, 5]. A solução calcula faturas com base no histórico de tarifas vigentes, monitora limites contratuais e emite alertas quando parâmetros de consumo são violados[cite: 3, 5].

---

##  Objetivo

O objetivo principal da solução é centralizar e automatizar a ingestão, o processamento e a auditoria dos dados de consumo elétrico, combinando a integridade transacional dos registros cadastrais e financeiros com a escalabilidade necessária para a coleta contínua de telemetria IoT[cite: 3, 5].

---

##  Tecnologias Utilizadas

- **MySQL**
- **MySQL Workbench**
- **MongoDB**
- **MongoDB Compass**
- **GitHub**

---

##  Arquitetura de Dados

A arquitetura do projeto emprega **Persistência Poliglota**, distribuindo os dados entre um banco relacional e um banco orientado a documentos:

### 1. Banco Relacional (MySQL)
Destinado a dados estruturados, transacionais e sujeitos a regras de integridade referencial:
- **Cadastros e Localização:** Tabelas `clientes`, `endereco`, `zona_municipal`, `tipo_imovel` e `unidade_consumo`[cite: 3, 5].
- **Dispositivos e Operações:** Tabelas `sensor`, `modelo_sensor`, `status_sensor` e `funcionario`[cite: 3, 5].
- **Tarifação e Contabilidade:** Tabelas `tarifa`, `consumo`, `fatura`, `meta_consumo` e `regra_alerta`[cite: 3, 5].

### 2. Banco Não Relacional (MongoDB)
Destinado a dados telemétricos flexíveis, de alto volume e rápida ingestão:
- **Telemetria de Sensores IoT:** Séries temporais em formato JSON com medições instantâneas (potência, corrente, tensão e kWh acumulado por leitura).
- **Logs de Diagnóstico:** Registros de eventos de rede, oscilações de conexão e integridade dos sensores.
- **Histórico de Alertas em Tempo Real:** Documentos de disparos de notificações gerados quando os limites diários ou mensais são ultrapassados[cite: 3, 5].

---

## 📂 Estrutura do Repositório

```text
├── docs/
│   ├── dicionario_de_dados.pdf         # Dicionário de dados formal com tipos e restrições
│   └── especificacao_requisitos.pdf    # Regras de negócio e escopo técnico
├── diagramas/
│   ├── der_relacional.png              # Diagrama Entidade-Relacionamento exportado
│   └── modelo_der_consumo_energia.mwb  # Modelo conceitual/físico do MySQL Workbench
├── sql/
│   └── modelo_consumo_energia.sql      # Script DDL de criação do banco e tabelas no MySQL
├── nosql/
│   ├── schemas/                        # Validações JSON Schema das collections do MongoDB
│   └── seeds/                          # Documentos JSON para carga inicial de telemetria
└── README.md                           # Documentação principal da solução
