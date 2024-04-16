# Mini-SO

Objetivo do SO: 
  - Criar um sistema de desenhos através de comandos interativos parecidos com a IDE "SuperLogo".
  - Não será desenvolvido um sistema completo de arquivos, apenas um sistema onde é possível salvar, editar ou excluir arquivos.
  - Não será desenvolvido drivers, pois serão utilizados os recursos diretamente da BIOS na arquitetura de 16 bits.
  - O sistema será desenvolvido de forma didática para pessoas que querem entender como funciona um sistema operacional simples e para crianças começarem a interagir com este mundo.

Ferramentas utilizadas:
  - O sistema será executado em um pendrive ou diskette, rodando em máquina real ou virtual.
  - Serão utilizados o Nasm para manipulações em Assembly, o Fergo Raw para criação de arquivos de imagem e Rufus 3.9.
  - Link do Nasm: https://www.nasm.us/pub/nasm/releasebuilds/2.14.03rc2/win64/
  - Link do Fergo Raw: https://www.fergonez.net/softwares/fraw
  - Link do Rufus: https://rufus.ie/downloads/
  - Será utilizado também um editor chamado Notepad++

Desenvolvimento 1ª aula:
  - Primeiramente fazemos o download do Nasm, do Fergo Raw e do Rufus 3.9. Em seguida, efetuamos a instalção do Nasm, inicializamos o Rufus 3.9 e extraimos o Zip do Fergo Raw. Entretanto, já encontramos um problema tentando abrir o arquivo extraído do Zip em questão. Aparece uma mensagem alegando que o componente "MSCOMCTL.OCX" ou uma de suas dependências não está corretamente registrada: um arquivo está faltando ou é inválido. Foi sugerido o uso de uma máquina virtual, porém os respectivos autores deste repositório não conseguiram solucionar ainda este problema. Evidentemente, será buscado uma solução futura para este problema.
  - Após a solução deste problema, deve-se configurar as variáveis de ambiente. Onde pegamos primeiramente o diretório do Nasm, abrimos as propriedades do computador e procuramos variáveis de ambiento no buscador e selecionamos o mesmo, posteriormente selecionamos a variável de sistema chamada de "path" e colamos o diretório do Nasm no campo chamado de "Valor da variável:" seguido de um clique no botão "ok". Após essa operação, feche as abas e abra o CMD e digite "nasm version" e será possível visualizar que agora o Nasm é uma variável de ambiente e poderá ser executada em qualquer lugar do computador.
  - Em seguida devemos organizar os arquivos do nosso SO, onde criamos uma pasta chamada "OSFiles" contendo outras duas pastas chamadas de "FergoRaw" e "Rufus", pasta essas que deverão conter as suas respectivas ferramentas detalhadas anteriormente.
  - Após isso, abrimos o editor Notepad++ para criar o BAT, onde executamos as instruções realizadas no vídeo. Por fim, no final do segundo vídeo o autor ensina como montar arquivos .ASM pelo Nasm.
  - No terceiro vídeo, é ensinado como baixar e instalar o Rufus 2.18 e máquina virtual da Oracle. O autor em seguida, mostra a execução e configuração do VirtualBox, a criação de uma máquina virtual e confuguração do USB. Por fim, o apresentador do vídeo demonstra como visualizar o número do pendrive pelo Windows e como gerar o arquivo .vmdk que conecta no USB. E por última instância, o autor revisa as configurações do VirtualBox.

Desenvolvimento 2ª aula *:

  - Como mencionado anteriormente, estávamos encontrando um problema na abertura do arquivo extraído do Fergo Raw. Felizmente, um colega de turma trouxe à sala uma solução para o problema, permitindo que, com alguns passos, o Fergo Raw pudesse ser efetivamente aberto.

  Passos utilizados:

  1 - O erro inicial (falta de registro do "MSCOMCTL.OCX") pôde ser solucionado com a instalação de uma biblioteca e uma ativação do tipo "Controle ActiveX", ambos foram       encontrados em uma série de tutoriais disponíveis virtualmente, como no link: https://www.youtube.com/watch?v=ZSJnJULnrng; Em computadores com o sistema operacional de 64 bits, deve-se utilizar as seguintes linhas de comando, no cmd acessado como administrador:
 
  Linhas de comando:
  1. cd C:\Windows\SysWOW64
  2. C:\Windows\SysWOW64 regsvr32 mscomctl.ocx

  Após a instalação da DLL através do cmd, utilize o instalador ascentive-library.

  Os arquivos mencionados para essa solução estão disponíveis em: https://drive.google.com/drive/folders/1Me89gAlCFmDR34rhr4ZKV8aXrGuqkbcI?usp=sharing

  2 - Após a solução do primeiro erro, uma nova mensagem é exibida, agora indicando que o componente "COMDLG32.OCX" estaria ausente, assim, podemos resolver de maneira parecida com o anterior. O vídeo https://www.youtube.com/watch?v=_Fpp6lYpS-U traz uma boa explicação sobre como resolver esta questão, sendo necessário instalar um arquivo de ativação através do link https://web.archive.org/web/20190402051129/http://www.bioinformatics.org/snp-tools-excel/install_comdlg32.htm. Ao instalar o arquivo, em computadores com o sistema operacional de 64 bits, devemos transferir o documento até a pasta de origem "SysWOW64", após, deve-se utilizar as seguintes linhas de comando, no cmd acessado como administrador:

  Linhas de comando:
  1. cd C:\Windows\SysWOW64
  2. C:\Windows\SysWOW64 regsvr32 comdlg32.ocx

  Os arquivos mencionados para essa solução estão disponíveis em: https://drive.google.com/drive/folders/1gI9B59-HFAmwxaWLpeQTu-fW07-RxkaL?usp=sharing

*Obs: caso seu computador tenha um sistema operacional de 32 bits, utilize o caminho C:\Windows\System32

Desenvolvimento 3ª aula:
  - Continuando o aplicado anteriormente, temos alguns passos para seguir:
     - Instalar uma versão compatível do Rufus, a 2.18, disponível através do link https://rufus-portable.br.uptodown.com/windows/post-download/1678016. 
     - Instalar a VirtualBox, versão 5.2.44, disponível através do link https://www.virtualbox.org/wiki/Download_Old_Builds_5_2, clicando em "Windows hosts".
     - Com isso, precisamos que a máquina virtual reconheça nosso pendrive usado, para isso, devemos utilizar linhas de comando no cmd:
    
      Linhas de comando
        1. cd %programfiles%\oracle\virtualbox
        2. VBoxManage internalcommands createrawvmdk -filename "%USERPROFILE%"\.VirtualBox\usb.vmdk -rawdisk \\.\PhysicalDrive [numero]

    - Substitua o campo [numero] pelo número do disco.
    - Agora crie sua máquina virtual com os dados desejados, selecionando a opção "Utilizar um disco rígido virtual existente", escolhemos o pendrive e confirmamos.
    - Utilizando a plataforma Notepad++, criamos um código inicial boot.asm para ser utilizado em nossa máquina virtual, o código pode ser conferido nos diretórios deste repositório.
    - Agora, com o código pronto, abrimos o FergoRaw, selecionamos como output um arquivo imagem a ser criado, com o nome System, como file, o código boot.bin, e adicionamos este a posição 1. Create file!
    - Usamos, neste momento, o Rufus 2.18 para capturar essa imagem System e colocar dentro do pendrive, criando o disco botável em "Imagem DD".
      
    - Importante ressaltar que, para gerar o boot.bin, devemos transformar boot.asm através do nasm, com o código no cmd:

      Linhas de comando
        1. nasm -f bin boot.asm -o boot.bin

Autores:
  -Emilaine Prado Correia Fagundes, João Vitor Souza Ribeiro e Vinicius Ferreira Couto.
