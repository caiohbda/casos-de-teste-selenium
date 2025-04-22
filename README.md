# Passo a Passo para Realização dos Testes Automatizados no Campo "Nome" do Formulário de Cadastro

Este documento descreve o passo a passo do código utilizado para realizar os testes automatizados no campo "Nome" de um formulário de cadastro utilizando o Selenium.

## 1. **Configuração do Selenium e Abertura do Navegador**

   - Inicialize o navegador Chrome utilizando o Selenium.
   - Utilize o `ChromeDriverManager` para gerenciar o driver do Chrome automaticamente.
   - Configure as opções do navegador, como maximizar a janela e manter o navegador aberto após o término do script.

## 2. **Acessando a Página Local**

   - Abra o navegador e acesse a URL local do formulário de cadastro (`http://127.0.0.1:5500/index.html`), onde o formulário está hospedado.

## 3. **Configuração de Espera Explícita**

   - Defina uma espera explícita para garantir que o Selenium aguarde até 10 segundos pela presença de elementos na página, como o campo de "Nome" e a mensagem de erro.

## 4. **Definição dos Casos de Teste**

   - Defina uma lista de casos de teste com entradas para o campo "Nome", que inclui:
     1. **Campo vazio**: Testa o comportamento quando o campo de "Nome" é deixado vazio.
     2. **Nome muito curto**: Testa quando o nome tem menos de 3 caracteres.
     3. **Nome com caracteres inválidos**: Testa quando o nome contém números ou caracteres especiais.
     4. **Nome válido**: Testa quando o nome é válido, com pelo menos 3 caracteres e apenas letras e espaços.

## 5. **Função de Testes de Exceções**

   - Para cada caso de teste, realize os seguintes passos:
     1. **Limpar o campo de nome**: Antes de cada teste, limpe o campo de "Nome" para garantir que o valor anterior não interfira.
     2. **Inserir o nome a ser testado**: Insira o valor de teste correspondente a cada caso.
     3. **Submeter o formulário**: Localize e clique no botão de envio do formulário.
     4. **Verificar Mensagens de Erro**: Após o envio, espere até que a mensagem de erro seja exibida e capture o texto. Se o texto estiver presente, ele será impresso no console.
     5. **Atraso entre os testes**: Após cada teste, adicione um pequeno atraso de 1 a 2 segundos para evitar que o script execute muito rapidamente.

## 6. **Função de Testes de Carga (opcional)**

   - Simule o envio de 50 entradas válidas com nomes sequenciais, de "Nome Teste 1" até "Nome Teste 50".
     1. **Inserir nomes sequenciais**: Em cada iteração, insira um nome dinâmico gerado automaticamente.
     2. **Submeter o formulário**: Após inserir o nome, clique no botão de envio do formulário.
     3. **Verificar se há mensagens de erro**: Mesmo que o nome seja válido, verifique se o sistema retorna alguma mensagem de erro.
     4. **Atraso entre as submissões**: Após cada envio, adicione um atraso de 1 segundo entre os testes para simular um comportamento mais realista.

## 7. **Execução dos Casos de Teste**

   - Chame a função de testes de exceções, que irá verificar como o sistema lida com entradas inválidas.
   - Chame a função de testes de carga (se necessário) para garantir que o sistema consiga processar múltiplos envios válidos de uma vez.
   
## 8. **Conclusão dos Testes**

   - Após a execução de todos os testes, o script imprime uma mensagem no console indicando que os testes de exceções e carga foram finalizados.
