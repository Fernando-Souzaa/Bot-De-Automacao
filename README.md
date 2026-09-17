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
def cpf_existe(self, cpf):
    return self.cursor.execute("SELECT 1 FROM clientes WHERE cpf = ?", (cpf,)).fetchone() is not None

def inserir_cliente(self, nome, cpf):
    if self.cpf_existe(cpf):
        return None
    self.cursor.execute("INSERT INTO clientes (nome, cpf) VALUES (?, ?)", (nome, cpf))
    self.conn.commit()
    return self.cursor.lastrowid

def inserir_conta(self, numero, cliente_id):
    self.cursor.execute("INSERT INTO contas (numero, cliente_id) VALUES (?, ?)", (numero, cliente_id))
    self.conn.commit()

def atualizar_saldo(self, numero, saldo):
    self.cursor.execute("UPDATE contas SET saldo = ? WHERE numero = ?", (saldo, numero))
    self.conn.commit()

def registrar_extrato(self, numero, op, valor):
    self.cursor.execute("INSERT INTO extratos (numero_conta, operacao, valor) VALUES (?, ?, ?)", (numero, op, valor))
    self.conn.commit()

def buscar_conta_com_cliente(self, numero):
    return self.cursor.execute("""
        SELECT c.numero, c.saldo, cli.nome, cli.cpf FROM contas c
        JOIN clientes cli ON c.cliente_id = cli.id WHERE c.numero = ?
    """, (numero,)).fetchone()

def obter_extrato(self, numero):
    return self.cursor.execute("""
        SELECT operacao, valor, data FROM extratos
        WHERE numero_conta = ? ORDER BY data
    """, (numero,)).fetchall()

def excluir_cliente_por_cpf(self, cpf):
    c = self.cursor
    cliente = c.execute("SELECT id FROM clientes WHERE cpf = ?", (cpf,)).fetchone()
    if not cliente:
        return False
    cliente_id = cliente[0]
    contas = c.execute("SELECT numero FROM contas WHERE cliente_id = ?", (cliente_id,)).fetchall()
    for (num,) in contas:
        c.execute("DELETE FROM extratos WHERE numero_conta = ?", (num,))
    c.execute("DELETE FROM contas WHERE cliente_id = ?", (cliente_id,))
    c.execute("DELETE FROM clientes WHERE id = ?", (cliente_id,))
    self.conn.commit()
    return True
