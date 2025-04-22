# Passo a Passo para Realização dos Testes Automatizados no Campo "Nome" do Formulário de Cadastro

1. **Definição dos Casos de Teste**
   - Cria uma lista de casos de teste para o campo "Nome", que inclui:
     - Campo vazio.
     - Nome muito curto (menos que 3 caracteres).
     - Nome com caracteres inválidos (como números e símbolos).
     - Nome válido (com pelo menos 3 caracteres e apenas letras e espaços).

2. **Função para Realizar os Testes de Exceções**
   - Para cada caso de teste:
     - Limpa o campo de nome.
     - Insere o valor de teste no campo "Nome".
     - Submete o formulário clicando no botão de envio.
     - Verifica se uma mensagem de erro aparece na página e, caso apareça, captura e imprime o texto da mensagem de erro.
     - Aguarda 2 segundos entre os testes para evitar execução muito rápida.

3. **Função para Realizar o Teste de Carga (opcional)**
   - Executa um teste de carga, simulando o envio de 50 nomes válidos (de "Nome Teste 1" até "Nome Teste 50").
   - Para cada nome:
     - Insere o nome no campo "Nome".
     - Submete o formulário e verifica se há mensagens de erro.
     - Aguarda 1 segundo entre as submissões para simular um comportamento mais realista.

4. **Execução dos Casos de Teste**
   - Chama a função de testes de exceções para verificar como o sistema lida com entradas inválidas.
   - Chama a função de testes de carga para verificar se o sistema pode processar múltiplas entradas válidas sem falhas.

5. **Conclusão dos Testes**
   - Após a execução dos testes de exceções e carga, imprime mensagens no console indicando que os testes foram finalizados.
