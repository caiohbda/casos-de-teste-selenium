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


```from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

# Configurações para o navegador Chrome (opções de inicialização).
options = Options()
options.add_argument("--start-maximized")  # Maximiza a janela do navegador ao iniciar.
options.add_experimental_option("detach", True)  # Mantém o navegador aberto após o script terminar.

# Inicializando o driver do Chrome com as opções configuradas e o ChromeDriver gerenciado automaticamente.
driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()), options=options)

# Acessando a página local do formulário (assumindo que o servidor local está rodando).
driver.get("http://127.0.0.1:5500/index.html")

# Configura uma espera explícita, que vai aguardar até 10 segundos pela presença de um elemento.
wait = WebDriverWait(driver, 10)

# Definindo os casos de teste (entradas de nome e suas descrições)
testes = [
    ("", "Campo vazio"),  # Testa quando o campo de nome está vazio.
    ("Jo", "Nome muito curto"),  # Testa quando o nome é muito curto (menos que 3 caracteres).
    ("Ana3!", "Nome com caracteres inválidos"),  # Testa quando o nome contém caracteres não permitidos.
    ("João da Silva", "Nome válido"),  # Testa um nome válido.
]

# Função para realizar os testes de exceção, verificando as respostas do sistema para entradas inválidas.
def teste_excecoes():
    for i, (nome, descricao) in enumerate(testes, 1):  # Loop que percorre os casos de teste (com número de ciclo)
        print(f"\n[Ciclo {i}] Testando: {descricao}")  # Imprime a descrição do teste atual

        # Espera até que o campo de nome esteja presente e obtém o elemento pelo ID 'name'
        nome_input = wait.until(EC.presence_of_element_located((By.ID, "name")))

        # Limpa o campo de nome e insere o nome para testar
        nome_input.clear()
        nome_input.send_keys(nome)

        # Localiza o botão de envio (assumido pela classe 'redirect-button') e clica nele.
        submit_button = driver.find_elements(By.CLASS_NAME, "redirect-button")[0]
        submit_button.click()

        # Espera até que a mensagem de erro (caso exista) seja exibida no elemento #error-message
        try:
            # Verifica se a mensagem de erro está presente no campo de erro da página (com ID 'error-message')
            error_message = wait.until(EC.presence_of_element_located((By.ID, "error-message")))
            
            # Se houver uma mensagem de erro, captura o texto e imprime.
            if error_message.text.strip():
                print(f"→ Mensagem de erro capturada: '{error_message.text}'")  # Imprime o texto da mensagem de erro

        except:
            print("→ Nenhuma mensagem de erro - envio aparentemente válido")  # Caso nenhuma mensagem de erro seja mostrada, imprime uma mensagem

        # Atraso de 2 segundos entre os testes para evitar execução muito rápida.
        time.sleep(2)
        
# Função para realizar o teste de carga a respeito do campo nome
def teste_carga():
    for i in range(1, 51):  # Executa 50 iterações, enviando "Nome Teste 1", "Nome Teste 2", ..., "Nome Teste 50"
        nome = f"Nome Teste {i}"
        print(f"\nEnviando nome: {nome}")  # Imprime o nome que está sendo enviado no teste

        # Espera até que o campo de nome esteja presente e obtém o elemento pelo ID 'name'
        nome_input = wait.until(EC.presence_of_element_located((By.ID, "name")))

        # Limpa o campo de nome e insere o nome de teste gerado dinamicamente
        nome_input.clear()
        nome_input.send_keys(nome)

        # Exibe o nome enviado para a verificação no formulário
        print(f"→ Nome enviado: '{nome}'")  # Aqui mostramos o nome que está sendo enviado no formulário

        # Localiza o botão de envio (assumido pela classe 'redirect-button') e clica nele.
        submit_button = driver.find_elements(By.CLASS_NAME, "redirect-button")[0]
        submit_button.click()

        # Espera até que a mensagem de erro (caso exista) seja exibida no campo de erro da página (com ID 'error-message')
        try:
            # Verifica se a mensagem de erro está presente no campo de erro da página
            error_message = wait.until(EC.presence_of_element_located((By.ID, "error-message")))
            
            # Se houver uma mensagem de erro, captura o texto e imprime.
            if error_message.text.strip():
                print(f"→ Mensagem de erro capturada: '{error_message.text}'")  # Imprime o texto da mensagem de erro

        except:
            print("→ Nenhuma mensagem de erro - envio aparentemente válido")  # Caso nenhuma mensagem de erro seja mostrada, imprime uma mensagem

        # Atraso de 1 segundo entre os testes para evitar execução muito rápida.
        time.sleep(1)

# Chama a função de testes de exceções
teste_excecoes()
print("\nTestes de exceções finalizados!")  # Imprime uma mensagem indicando que os testes de exceção foram concluídos.

# Chama a função de testes de carga
teste_carga()
print("\nTestes de carga finalizados!")  # Imprime uma mensagem indicando que os testes de carga foram concluídos.
```
