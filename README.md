# Recursividade
Trabalho de recursividade
def vazio(lista):
 return lista == []

def cabeca(lista):
 return lista[0]

def cauda(lista):
 return lista[1:]

def insere(lista, x):
 lista.append(x)
 return lista

def pertence(lista ,elemento):
    if vazio(lista):
        return False

    elif cabeca(lista) == elemento :
        return True

    else:
        cauda_da_lista = cauda(lista)
        resultado = pertence(cauda_da_lista,elemento)
        return resultado

def concatenacao(lista,lista_2):
    if vazio(lista_2):
        return lista

    else:
        cabeca_lista_2 = cabeca(lista_2)
        insere(lista,cabeca_lista_2)
        cauda_lista_2 = cauda(lista_2)
        return concatenacao(lista,cauda_lista_2)

def ultimo(lista):
    #caso base
    if vazio(cauda(lista)):
        return cabeca(lista)
    else:
        cauda_da_lista = cauda(lista)
        return ultimo(cauda_da_lista)

def elemento(lista,posicao):
    c = posicao - 1
    if c == 0:
        return cabeca(lista)

    else:
        lista = cauda(lista)
        return elemento(lista,posicao - 1)

def comprimento(lista):
    if vazio(lista):
        return 0

    else:
        lista_da_cauda = cauda(lista)
        comprimento_da_cauda = comprimento(lista_da_cauda)
        contador = comprimento_da_cauda + 1
        return contador

def inverte(lista):
    if comprimento(lista) == 0:
        return []
    else:
        cauda_da_lista = cauda(lista)
        return insere(inverte(cauda_da_lista),cabeca(lista))

def primeiros(lista,numero_de_elementos):
    if comprimento(lista) == numero_de_elementos:
        return lista
    else:
        lista_invertida = inverte(lista)
        Cauda_invertida = cauda(lista_invertida)
        lista_sem_ultimo = inverte(Cauda_invertida)
        return primeiros(lista_sem_ultimo,numero_de_elementos)

abertura = open('Lista.txt','a')
while True:
    lista = input('Digite sua lista: ')
    lista = lista.split(',')
    Espelho_da_lista = lista[:]
    Escolha_da_Funcao = input('''Qual funçaõ deseja usar :
    [1] Descobrir se a lista é vazia
    [2] Receber o primeiro elemento da lista
    [3] Receber a lista sem o primeiro elemento
    [4] Inserir um elemento na lista
    [5] Descobrir se o elemento pertence a lista
    [6] Concatenar 2 listas
    [7] Receber o último elemento da lista
    [8] Receber Qual elemento está na posição desejada
    [9] Receber o comprimento da lista
    [10] inverter a lista
    [11] Descobrir os "Ns" primeiros termos
    [12] Encerrar o programa
    ''')
    while Escolha_da_Funcao != '1' and Escolha_da_Funcao != '2' and Escolha_da_Funcao != '3' and Escolha_da_Funcao != '4' and Escolha_da_Funcao != '5' and Escolha_da_Funcao != '6' and Escolha_da_Funcao != '7' and Escolha_da_Funcao != '8' and Escolha_da_Funcao != '9' and Escolha_da_Funcao != '10' and Escolha_da_Funcao != '11' and Escolha_da_Funcao != '12' :
        print('Erro na escolha de função! Deve estar entre 1 e 12.')
        Escolha_da_Funcao = input('Qual funçaõ deseja usar :')

    if Escolha_da_Funcao == '1':
        print(f"O vazio da {lista} é --> {vazio(lista)}")
        abertura.write(f"(vazio',{lista} , {vazio(lista)}))\n")

    elif Escolha_da_Funcao == '2':
        print(f"A cabeca da {lista} é --> {cabeca(lista)}")
        abertura.write(f"(Cebeça ,{lista} , {cabeca(lista)})\n")

    elif Escolha_da_Funcao == '3':
        print(f"A cauda da {lista} é --> {cauda(lista)}")
        abertura.write(f"(Cauda , {lista} , {cauda(lista)})\n")
        
    elif Escolha_da_Funcao == '4':
        elemento_ = input('Digite o elemento: ')
        print(f"Inserindo {elemento_} na {Espelho_da_lista} --> {insere(Espelho_da_lista,elemento_)}")
        abertura.write(f"(Insere , {lista} , {elemento_} , {insere(Espelho_da_lista,elemento_)})\n")
        
    elif Escolha_da_Funcao == '5':
        elemento_ = input('Digite o elemento: ')
        print(f"{elemento_} pertence a {lista} é --> {pertence(lista,elemento_)}")
        abertura.write(f"(Pertence , {lista} , {elemento_} , {pertence(lista,elemento_)})\n")
        
    elif Escolha_da_Funcao == '6':
        lista_2 = input('Segunda lista: ')
        lista_2 = lista_2.split(',')
        print(f"A concatenação de {lista} e {lista_2} é --> {concatenacao(lista,lista_2)}")
        abertura.write(f"(Concatenação , {Espelho_da_lista} , {lista_2} , {concatenacao(Espelho_da_lista,lista_2)})\n")

    elif Escolha_da_Funcao == '7':
        print(f"O último elemento da lista{lista} é --> {ultimo(lista)}")
        abertura.write(f"(Último , {lista} , {ultimo(lista)})\n")

    elif Escolha_da_Funcao == '8':
        posicao = int(input('Digite a posição:'))
        while posicao < 0 or posicao > comprimento(lista):
            print('Não existe elementos nessa posição!')
            posicao = int(input('Digite a posição:'))
        print(f"O elemento da posição {posicao} da lista {lista} é --> {elemento(lista,posicao)}")
        abertura.write(f"(Elemento , {lista} , {posicao} , {elemento(lista,posicao)})\n")

    elif Escolha_da_Funcao == '9':
        print(f"O comprimento da lista {lista} é --> {comprimento(lista)}")
        abertura.write(f"(Comprimento , {lista} , {comprimento(lista)})\n")
        
    elif Escolha_da_Funcao == '10':
        print(f"A lista {lista} invertida é --> {inverte(lista)}")
        abertura.write(f"(Inverte , {lista} , {inverte(lista)})\n")
        
    elif Escolha_da_Funcao == '11':
        Quantidade_dos_elementos = int(input('Digite a quantidade de elementos: '))
        while Quantidade_dos_elementos < 0 or Quantidade_dos_elementos > comprimento(lista):
            print('Erro! Quantidades de elementos inválidos! ')
            Quantidade_dos_elementos = int(input('Digite a quantidade de elementos: '))
        print(f"Os {Quantidade_dos_elementos} primeiros elementos da lista {lista} são --> {primeiros(lista,Quantidade_dos_elementos)}")
        abertura.write(f"(Primeiros , {lista} , {Quantidade_dos_elementos} , {primeiros(lista,Quantidade_dos_elementos)})\n")
        
    elif Escolha_da_Funcao == '12':
        break
