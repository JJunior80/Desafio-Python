# Sistema Bancário em Python

## Descrição
Este projeto consiste em um sistema bancário simples desenvolvido em Python. Ele permite ao usuário realizar operações básicas como depósito, saque e exibição de extrato. O objetivo deste projeto é oferecer uma experiência prática no desenvolvimento de software financeiro, consolidando conceitos fundamentais da linguagem Python.

## Funcionalidades
- **Depósito**: Permite adicionar saldo à conta, registrando a transação no extrato.
- **Saque**: Permite retirar dinheiro da conta, respeitando o saldo disponível, o limite por saque e o número máximo de saques diários.
- **Extrato**: Exibe todas as transações realizadas na conta, bem como o saldo atual.

## Como Usar
1. Execute o programa no terminal.
2. Escolha uma opção do menu exibido:
   - `[d]` para Depositar
   - `[s]` para Sacar
   - `[e]` para visualizar o Extrato
   - `[q]` para Sair
3. Siga as instruções para cada operação.

## Código-Fonte
```python
def exibir_menu():
    """Exibe o menu de opções do sistema."""
    return """
    [d] Depositar
    [s] Sacar
    [e] Extrato
    [q] Sair
    
    => """

def depositar(saldo, extrato):
    """Realiza um depósito na conta."""
    valor = float(input("Informe o valor do depósito: "))
    
    if valor > 0:
        saldo += valor
        extrato.append(f"Depósito: R$ {valor:.2f}")
        print("Depósito realizado com sucesso!")
    else:
        print("Operação falhou! O valor informado é inválido.")
    
    return saldo, extrato

def sacar(saldo, extrato, numero_saques, limite, LIMITE_SAQUES):
    """Realiza um saque da conta respeitando regras de saldo e limite."""
    valor = float(input("Informe o valor do saque: "))
    
    if valor <= 0:
        print("Operação falhou! O valor informado é inválido.")
    elif valor > saldo:
        print("Operação falhou! Você não tem saldo suficiente.")
    elif valor > limite:
        print("Operação falhou! O valor do saque excede o limite diário.")
    elif numero_saques >= LIMITE_SAQUES:
        print("Operação falhou! Número máximo de saques excedido.")
    else:
        saldo -= valor
        extrato.append(f"Saque: R$ {valor:.2f}")
        numero_saques += 1
        print("Saque realizado com sucesso!")
    
    return saldo, extrato, numero_saques

def exibir_extrato(saldo, extrato):
    """Exibe o extrato das movimentações da conta."""
    print("\n================ EXTRATO ================")
    if not extrato:
        print("Não foram realizadas movimentações.")
    else:
        for movimento in extrato:
            print(movimento)
    print(f"\nSaldo: R$ {saldo:.2f}")
    print("==========================================")

def main():
    saldo = 0
    limite = 500
    extrato = []
    numero_saques = 0
    LIMITE_SAQUES = 3
    
    while True:
        opcao = input(exibir_menu()).strip().lower()
        
        if opcao == "d":
            saldo, extrato = depositar(saldo, extrato)
        elif opcao == "s":
            saldo, extrato, numero_saques = sacar(saldo, extrato, numero_saques, limite, LIMITE_SAQUES)
        elif opcao == "e":
            exibir_extrato(saldo, extrato)
        elif opcao == "q":
            print("Obrigado por utilizar nosso sistema bancário. Até logo!")
            break
        else:
            print("Operação inválida, por favor selecione novamente a operação desejada.")

if __name__ == "__main__":
    main()
```

## Requisitos
- Python 3.x instalado
- Terminal para executar o programa

## Autor
Este projeto foi desenvolvido para fins educacionais e pode ser aprimorado com novas funcionalidades no futuro.
