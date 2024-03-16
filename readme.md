# Ponderada 3

## Introdução

Esse repositório serve como relatório para a ponderada Simulação de ataques usando MQTT. O autoestudo foca em simular ataques a um servidor MQTT, baseando-se nos 3 pilares da segurança da informação: Confidencialidade, Integridade e Disponibilidade. Esses pilares são conhecidos com CIA triad.

## Pilares

1. Disponibilidade: A disponibilidade é a garantia de que os recursos estarão disponíveis para o uso legítimo. No caso de um servidor MQTT, a disponibilidade é garantida pela capacidade de processamento e pela capacidade de rede. Aqui  encomtramos uma vulnerabilidade no docker-compose.yml, onde o servidor MQTT está exposto na porta com pouca memória e processamento alocado, facilitando um ataque de negação de serviço, já que o sistema facilmente ficará sobrecarregado. Para evitar essa vulnerabilidade deve haver uma configuração de limites de memória e processamento coerente com a possível demanda do serviço.

2. Confidencialidade: A confidencialidade é a garantia de que a informação será acessível apenas por pessoas autorizadas. No caso de um servidor MQTT, a confidencialidade é garantida pela autenticação e criptografia. Aqui encontramos uma vulnerabilidade no arquivo de configuração do servidor MQTT, onde a autenticação está desabilitada, permitindo que qualquer pessoa acesse o servidor e leia e escreva mensagens. O arquivo mosquitto.conf deve remover o comentário das linhas `allow_anonymous false` e `password_file /mosquitto/config/passwd` para habilitar a autenticação. Além disso deve haver um  usuário e senha fortes.

3. Integridade: A integridade é a garantia de que a informação não foi alterada por pessoas não autorizadas. No caso de um servidor MQTT, é necessário garantir que as mensagens não sejam alteradas durante a transmissão. Aqui encontramos uma vulnerabilidade na ausência de um banco de dados para realizar persistência das mensagens. O arquivo de configuração do servidor MQTT deve ser alterado para incluir a linha `persistence true` para habilitar a persistência das mensagens. Além disso, deve haver um backup das mensagens para garantir a integridade das mensagens. Além disso o banco deve ter um sistema de criptografia para garantir a integridade das mensagens. Além disso, sem verificação de usuário e senha, qualquer pessoa pode se tornar um publisher e mandar falsas mensagens.

## Códigos citados

Segue uma lista dos códigos citados no relatório:

- ```bash docker-compose.yml```: Arquivo de configuração do docker-compose: ```bash           cpus: '0.01'
          memory: 100M```
- ```bash mosquitto.conf```: Arquivo de configuração do servidor MQTT: ```bash allow_anonymous false``` e ```bash password_file /mosquitto/config/passwd```
- ```bash mosquitto.conf```: Arquivo de configuração do servidor MQTT: ```bash persistence true```
