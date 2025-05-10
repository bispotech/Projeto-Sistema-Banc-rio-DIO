from datetime import datetime

menu = '''

[d] Depositar
[s] Sacar
[e] Extrato
[q] Sair

=> '''

saldo = 0
limite = 500
extrato = ""
numero_saques = 0
LIMITE_SAQUES = 3

while True:

    opcao = input(menu)

    if opcao == "d":
        print("Depósito")
        valor_deposito = float(input("Informe o valor do depósito: "))
        
        if valor_deposito > 0:
                saldo += valor_deposito
                data_hora = datetime.now().strftime("%d/%m/%Y, %H:%M:%S")
                extrato += f"[{data_hora}] Depósito: R${valor_deposito:.2f}\n"
                print("Depósito realizado com sucesso!")
        else:
                print("Operação falhou! Deposite um valor válido")

    elif opcao == "s":
        print("Saque")
        valor_saque = float(input("Informe o valor do saque: "))

        excedeu_saldo = valor_saque > saldo
        excedeu_limite = valor_saque > limite
        excedeu_saques = numero_saques >= LIMITE_SAQUES
    
        if excedeu_saldo:
            print("Você não tem saldo suficiente.")

        elif excedeu_limite:
            print("Operação falhou: O valor do saque é maior que o limite permitido.")

        elif excedeu_saques:
            print("Operação falhou: Você excedeu o limite de saques diário.")

        elif valor_saque > 0:
            saldo -= valor_saque
            numero_saques += 1
            data_hora = datetime.now().strftime("%d/%m/%Y, %H:%M:%S")
            extrato += f"[{data_hora}] Saque: R$ {valor_saque:.2f}\n"
            print("Saque realizado com sucesso!\n")

        else:
            print("Operação falhou: O Valor informado é inválido.")

    elif opcao == "e":
        print("\n=========================Extrato=========================")
        print("Não foram realizadas movimentações." if not extrato else extrato)
        print(f"\nSaldo: R$ {saldo:.2f}")
        print("===========================================================")

    elif opcao == "q":
        break

    else:
        print("Operação inválida, por favor selecione novamente a operação desejada")