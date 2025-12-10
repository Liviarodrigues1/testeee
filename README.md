# testeee

# Requisitos funcionais

Os requisitos funcionais descrevem as funcionalidades que o veículo deve executar para atender aos objetivos do projeto. Eles estão organizados em três dimensões principais: estrutura, que define aspectos físicos e de montagem; eletrônica, que engloba sensores, atuadores e módulos de energia/comunicação; e software, que garante o processamento de informações, controle do veículo e integração com interfaces externas. Cada requisito é acompanhado de uma prioridade, de modo a orientar o desenvolvimento com base no que é essencial para o funcionamento do protótipo.

| Nº | Requisito                                                                 | Descrição   | Prioridade |
|----|---------------------------------------------------------------------------|-------------|------------|
| 1  | O carro deve possuir dimensões de 50 cm de largura e 50 cm de comprimento | Estrutura   | Alta       |
| 2  | O carro (estrutura e motor) deve ser capaz de transportar uma carga útil mínima de 10 kg, adicionalmente ao peso de sua própria estrutura | Estrutura | Alta       |
| 3  | O veículo deve permitir montagem/desmontagem modular de sensores, placa de controle e baterias | Estrutura | Média      |
| 4  | O carro deve ser movido a energia elétrica                                | Eletrônica  | Alta       |
| 5  | Deve possuir autonomia mínima de 5 voltas                                 | Eletrônica  | Alta       |
| 6  | Medir tensão de bateria                                                   | Eletrônica  | Média      |
| 7  | Medir corrente de descarga/recarga                                        | Eletrônica  | Média      |
| 9  | Estimar “quantidade” de bateria                                           | Eletrônica  | Média      |
| 10 | Detectar baixa voltagem ou corrente alta e interromper acionamento para proteção. Registrar evento | Eletrônica | Alta       |
| 11 | Possuir sensores de distância, velocidade e câmera(s)                     | Eletrônica  | Alta       |
| 12 | Ler informações de todos os sensores instalados e disponibilizá-las ao sistema de percepção | Eletrônica | Alta       |
| 13 | Filtrar, normalizar e compensar ruído dos sensores antes de fornecer dados aos módulos de percepção | Eletrônica | Média      |
| 14 | Capturar frames de uma ou mais câmeras (RGB/mono), com sincronização temporal e metadados (timestamp, exposição) | Eletrônica | Média      |
| 15 | Detectar obstáculos no trajeto                                            | Software    | Alta       |
| 16 | Detectar placas e sinais e produzir ação para cada caso (parar, reduzir velocidade, virar) | Software | Alta       |
| 17 | Controlar a velocidade e direção dos motores de tração (frente/trás)      | Software    | Alta       |
| 18 | Controlar direção dos sistemas de direção (esquerda/direita)              | Software    | Alta       |
| 19 | Possuir módulo de rede para comunicação via Internet                      | Eletrônica  | Alta      |
| <s>20</s> | <s>Possuir módulo Bluetooth para controle manual do carro</s> | <s>Eletrônica</s> | <s>Alta</s> |
| 21 | Enviar dados/logs de sensores, energia e status para backend remoto em tempo real  | Software | Alta       |
| 22 | Possuir interface web para monitoramento                                  | Software    | Média      |
| 23 | Possuir processamento de informações embutido no carro                    | Software    | Alta       |
| 24 | Desligar motores e registrar falha para casos de emergência               | Software    | Alta       |





**Observação:** Requisito 20 foi retirado devido à interpretação errônea dos requisitos gerais da matéria. 


# Arquitetura de Software

A arquitetura de software do veículo foi projetada de forma **modular e escalável**, garantindo integração eficiente com os subsistemas de Estrutura e Eletrônica. O software é responsável pelo **processamento de dados, tomada de decisão, controle do veículo e interface com sistemas externos**, assegurando operação autônoma e segura.

## Subsistema de visão computacional

Este subsistema interpreta os dados fornecidos pelo subsistema de percepção para gerar ações concretas e autônomas. Inclui:  
- Reconhecimento de placas de Pare/Siga, curvas, faixa de pedestre e cones.  
- Identificação de obstáculos dinâmicos e estáticos ao longo do trajeto.  
- Definição de comandos de movimentação e ajustes de velocidade baseados nas regras de trânsito simuladas.

## Subsistema de Navegação

Responsável por **executar as decisões do software** convertendo-as em comandos para o subsistema de atuação (eletrônica). 
- Processamentos dos dados recebidos pelos sensores e visão computacional.
- Controle da velocidade.
- Controle de direção do veículo.

## Subsistema de Telemetria

Responsável pelo **monitoramento remoto e armazenamento de dados**:  
- Transmissão de dados de status, energia e eventos para backend remoto via MQTT.  
- Interface web para acompanhamento em tempo real da telemetria.  
- Registro e exportação de logs para análise posterior, incluindo eventos críticos, falhas e dados de desempenho.

