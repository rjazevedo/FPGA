# Instalação  

## OSS CAD Suite  

O **OSS CAD Suite** é um conjunto de ferramentas open source para design de hardware. Ele inclui ferramentas para síntese, simulação, verificação e build para diversas FPGAs. O tutorial abaixo é baseado no repositório oficial do [OSS CAD Suite no GitHub](https://github.com/YosysHQ/oss-cad-suite-build).  

1. Baixe o pacote de instalação do [OSS CAD Suite](https://github.com/YosysHQ/oss-cad-suite-build/releases/tag/2025-02-19). Eu utilizei especificamente esta [versão](https://github.com/YosysHQ/oss-cad-suite-build/releases/download/2025-02-19/oss-cad-suite-linux-x64-20250219.tgz). Caso haja uma versão mais recente disponível no dia em que você seguir este tutorial, recomendo verificar a seção de releases no GitHub para baixar a versão mais atualizada.  

2. Crie uma pasta chamada **eda** (abreviação de *Electronic Design Automation*) no seu diretório home e descompacte o arquivo nela, com o nome **oss-cad-suite**.  

3. Adicione o **oss-cad-suite** ao seu PATH, incluindo uma entrada no seu `.bashrc` ou `.zshrc`, como mostrado abaixo:  

   ```bash
   export PATH=$PATH:~/eda/oss-cad-suite/bin
   ```

Esse passo a passo pode ser resumido nos seguintes comandos:  

```bash
mkdir -p ~/eda
cd ~/eda
wget https://github.com/YosysHQ/oss-cad-suite-build/releases/download/2025-02-19/oss-cad-suite-linux-x64-20250219.tgz
tar xvf oss-cad-suite-linux-x64-20250219.tgz
# Para usuários de Bash
echo "export PATH=\$PATH:~/eda/oss-cad-suite/bin" >> ~/.bashrc
# Para usuários de Zsh
echo "export PATH=\$PATH:~/eda/oss-cad-suite/bin" >> ~/.zshrc
rm oss-cad-suite-linux-x64-20250219.tgz
```

---

## Plugins do VSCode  

Alguns plugins são recomendados para o VSCode. A maneira mais simples de instalá-los é pesquisando pelo nome dentro do próprio editor, mas os links diretos também estão disponíveis abaixo:  

1. [Verilog HDL/SystemVerilog](https://marketplace.visualstudio.com/items?itemName=mshr-h.VerilogHDL&ref=learn.lushaylabs.com)  
2. [WaveTrace](https://marketplace.visualstudio.com/items?itemName=wavetrace.wavetrace&ref=learn.lushaylabs.com)  
3. [Serial Monitor](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-serial-monitor)  
4. [DigitalJS](https://marketplace.visualstudio.com/items?itemName=yuyichao.digitaljs)  

---

## Ajuste de permissões para acessar a USB sem ser root  

Se precisar acessar dispositivos USB sem permissões de superusuário (*root*), execute o seguinte comando:  

```bash
curl -sSL https://raw.githubusercontent.com/lushaylabs/openfpgaloader-ubuntufix/main/setup.sh | sh
```
