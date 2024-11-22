import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Configuração do driver do navegador
driver = webdriver.Chrome()  # Certifique-se de ter o driver do Chrome instalado
driver.maximize_window()

# URL do CMSP
url = "https://estudante.cmsp.sp.gov.br/"  # Insira o link correto do CMSP

try:
    # Acessar o site
    driver.get(url)

    # Login
    print("Fazendo login...")
    wait = WebDriverWait(driver, 10)
    usuario = wait.until(EC.presence_of_element_located((By.ID, "username")))  # Substitua pelo ID do campo correto
    senha = driver.find_element(By.ID, "password")  # Substitua pelo ID do campo correto

    usuario.send_keys("seu_usuario")  # Insira o usuário
    senha.send_keys("sua_senha")  # Insira a senha
    senha.send_keys(Keys.RETURN)

    # Aguardar a página inicial carregar
    print("Aguardando carregamento da página principal...")
    wait.until(EC.presence_of_element_located((By.CLASS_NAME, "dashboard")))  # Substitua pela classe/ID correto

    # Navegar para as lições
    print("Acessando as lições...")
    licoes_menu = driver.find_element(By.XPATH, "//a[@href='/licoes']")  # Substitua pelo XPATH correto
    licoes_menu.click()

    # Esperar a lista de lições carregar
    print("Carregando lista de lições...")
    wait.until(EC.presence_of_element_located((By.CLASS_NAME, "lesson-card")))  # Substitua pelo seletor correto

    # Selecionar uma lição
    print("Selecionando uma lição...")
    primeira_licao = driver.find_element(By.CLASS_NAME, "lesson-card")  # Substitua pelo seletor correto
    primeira_licao.click()

    # Preencher respostas (Exemplo)
    print("Respondendo questões...")
    questoes = wait.until(EC.presence_of_all_elements_located((By.CLASS_NAME, "question")))  # Substitua pelo seletor correto
    for questao in questoes:
        resposta = questao.find_element(By.TAG_NAME, "input")  # Substitua pelo seletor correto
        resposta.send_keys("Resposta automática")  # Insira a resposta desejada
        time.sleep(1)  # Pequena pausa entre respostas

    # Submeter a lição
    print("Submetendo a lição...")
    botao_enviar = driver.find_element(By.ID, "submit-button")  # Substitua pelo ID correto
    botao_enviar.click()

    print("Lição concluída!")
except Exception as e:
    print(f"Ocorreu um erro: {e}")
finally:
    # Encerrar o navegador
    print("Finalizando...")
    driver.quit()
<!---
Jxjshbr/Jxjshbr is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
