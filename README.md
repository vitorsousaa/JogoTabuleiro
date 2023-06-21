# JogoTabuleiro
def exibir_tabuleiro(tabuleiro):
    print("\nTabuleiro:")
    for linha in tabuleiro:
        print(" | ".join(linha))
        print("-" * 9)

def realizar_jogada(jogador, tabuleiro):
    linha = int(input("Digite a linha para mover o marcador (0-2): "))
    coluna = int(input("Digite a coluna para mover o marcador (0-2): "))

    if tabuleiro[linha][coluna] == " ":
        tabuleiro[linha][coluna] = jogador
    else:
        print("Essa posição já está ocupada. Tente novamente.")
        realizar_jogada(jogador, tabuleiro)

def verificar_vitoria(tabuleiro, jogador):
    for linha in tabuleiro:
     if linha.count(jogador) == 3:
            return True

    for coluna in range(3):
        if tabuleiro[0][coluna] == jogador and tabuleiro[1][coluna] == jogador and tabuleiro[2][coluna] == jogador:
            return True

    if tabuleiro[0][0] == jogador and tabuleiro[1][1] == jogador and tabuleiro[2][2] == jogador:
        return True

    if tabuleiro[0][2] == jogador and tabuleiro[1][1] == jogador and tabuleiro[2][0] == jogador:
        return True

    return False

def jogar():
    tabuleiro = [[" ", " ", " "], [" ", " ", " "], [" ", " ", " "]]
    jogadores = ["X", "O"]
    jogador_atual = 0
    fim_de_jogo = False
     while not fim_de_jogo:
        exibir_tabuleiro(tabuleiro)
        jogador = jogadores[jogador_atual]
        print(f"Vez do jogador {jogador}")
        realizar_jogada(jogador, tabuleiro)

        if verificar_vitoria(tabuleiro, jogador):
            exibir_tabuleiro(tabuleiro)
            print(f"Jogador {jogador} venceu!")
            fim_de_jogo = True

        if " " not in tabuleiro[0] and " " not in tabuleiro[1] and " " not in tabuleiro[2]:
            exibir_tabuleiro(tabuleiro)
            print("Empate!")
            fim_de_jogo = True

        jogador_atual = (jogador_atual + 1) % 2

jogar()
