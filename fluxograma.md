~~~mermaid
flowchart TD

%% INÍCIO
A([Início do Aplicativo]) --> B[Usuário inicia diagnóstico]

%% PERMISSÕES
B --> C{Permissões concedidas?}
C -->|Não| C1["Solicitar permissões necessárias<br/>(Telefone, SMS, Rede)"]
C1 --> C
C -->|Sim| D[Coletar informações do dispositivo]

%% COLETA DE CONTEXTO
D --> D1[Tipo de rede atual]
D1 --> D2[Estado do VoLTE]
D2 --> D3[Qualidade de sinal]
D3 --> E[Selecionar tipo de teste]

%% SELEÇÃO DE TESTES
E -->|Teste de SMS| F[Teste de envio e recebimento de SMS]
E -->|Teste de Ligações| G[Teste de chamadas]
E -->|Teste de Dados| H[Teste de conectividade e latência]

%% TESTE SMS
F --> F1[Enviar SMS para número padrão / Short Code / Broker]
F1 --> F2{SMS entregue?}
F2 -->|Não| F3[Registrar falha de SMS]
F2 -->|Sim| F4[Registrar sucesso de SMS]

%% TESTE LIGAÇÕES
G --> G1[Realizar chamada de saída]
G1 --> G2{Chamada estabelecida?}
G2 -->|Não| G3[Registrar falha de chamada]
G2 -->|Sim| G4[Testar áudio e duração]
G4 --> G5{Queda ou erro?}
G5 -->|Sim| G6[Registrar erro de ligação]
G5 -->|Não| G7[Registrar sucesso de ligação]

%% TESTE DADOS
H --> H1[Teste de latência]
H1 --> H2[Teste de perda de pacotes]
H2 --> H3{Conectividade estável?}
H3 -->|Não| H4[Registrar falha de dados]
H3 -->|Sim| H5[Registrar sucesso de dados]

%% COLETA DE LOGS
F3 --> I
F4 --> I
G3 --> I
G6 --> I
G7 --> I
H4 --> I
H5 --> I

I[Coletar logs e métricas]
I --> I1[Eventos de rede]
I1 --> I2[Erros]
I2 --> I3[Timestamp e contexto]

%% RELATÓRIO
I3 --> J[Gerar relatório técnico]
J --> J1[Resumo dos testes]
J1 --> J2[Detalhamento técnico]
J2 --> J3[Identificação de falhas]

%% FINAL
J3 --> K([Exportar relatório])
K --> L([Encerrar diagnóstico])
