# Bot-De-Automação
Esse projeto foi desenvolvido após eu aprender a criar bots de automação em Python, bastante utilizados em empresas para realizar tarefas como cadastro de produtos. Resolvi colocar em prática o que eu aprendi criando meu próprio bot. A diferença é que o meu bot não faz grandes operações, ele simplesmente abre o navegador e pesquisa sobre o melhor time de todos os tempos, o meu Mengão.

# Funcionalidades
Automatiza a abertura do navegador  
Realiza pesquisas automaticamente  

# Código
import pyautogui  
import time  

pyautogui.PAUSE = 0.5   

pyautogui.press("win")  
pyautogui.write("edge")  
pyautogui.press("enter")  
pyautogui.write("flamengo")  
pyautogui.press("enter")  
