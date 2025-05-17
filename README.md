import getpass
import json

senha_correta = "Aluno"
tentativas = 3  # Número máximo de tentativas

while tentativas > 0:
    senha_usuario = getpass.getpass("Digite sua senha: ")

if senha_usuario == senha_correta:
    print("Acesso concedido! Bem-vindo(a).")
        
nome = input("Digite seu nome completo: ")
RA = input("Digite seu RA: ")

NotaA = float(input("Informe a nota da NP1: "))
NotaB = float(input("Informe a nota da NP2: "))
mediafinal = (NotaA + NotaB) / 2
situacao = ""

if mediafinal >= 7.0:
    situacao = "Aprovado"
    print(f"Sua média foi: {mediafinal:.1f} - {situacao}!")
else:
    situacao = "Exame"
    print(f"Sua média foi {mediafinal:.1f} - Você está de exame!")

    NotaExame = float(input("Informe a nota do exame: "))
    nova_media = (mediafinal + NotaExame) / 2

if nova_media >= 5.0:
    situacao = "Aprovado após exame"
    print(f"Sua nova média foi: {nova_media:.1f} - {situacao}!")
else:
    situacao = "Reprovado"
print(f"Sua nova média foi: {nova_media:.1f} - {situacao}!")

# Criação do dicionário com os dados do aluno
dados_aluno = {
"nome": nome,
"RA": RA,
"Nota NP1": NotaA,
"Nota NP2": NotaB,
"Média Final": mediafinal,
"Situação": situacao
}

if situacao in ["Aprovado após exame", "Reprovado"]:
    dados_aluno["Nota Exame"] = NotaExame
    dados_aluno["Nova Média"] = nova_media

# Salva os dados no arquivo JSON
with open(f"{RA}_{nome.replace(' ', '_')}.json", "w", encoding="utf-8") as arquivo_json:
    json.dump(dados_aluno, arquivo_json, ensure_ascii=False, indent=4)

print("Dados salvos com sucesso no arquivo JSON.")
