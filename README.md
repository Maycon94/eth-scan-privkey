# eth-scan-privkey-
from web3.auto import w3
from eth_account import Account
from termux import api

def generate_eth_key():
    """
    Gera uma nova chave privada Ethereum e retorna a chave privada e o endereço da conta.
    """
    account = Account.create()
    private_key = account.privateKey.hex()
    address = account.address
    return private_key, address

def get_eth_balance(address):
    """
    Obtém o saldo ETH de uma determinada conta Ethereum.
    """
    balance = w3.eth.getBalance(address)
    return balance

# Gerar uma nova chave privada e mostrar o endereço e o saldo da conta
private_key, address = generate_eth_key()
print("Endereço da conta:", address)
balance = get_eth_balance(address)
print("Saldo da conta:", balance)

# Verificar se a conta tem saldo e pausar o script se tiver
if balance > 0:
    message = f"A conta {address} tem um saldo de {balance} wei. Deseja continuar?"
    response = api.dialog.create("Chave privada encontrada!", message, ["Sim", "Não"]).get().lower()
    if response != "sim":
        exit()

# Continuar o script se a conta não tiver saldo ou o usuário optar por continuar
print("Continuando o script...")
