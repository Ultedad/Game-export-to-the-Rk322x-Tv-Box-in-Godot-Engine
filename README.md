# Game-export-to-the-Rk322x-Tv-Box-in-Godot-Engine 

* Nesse repositorio irei instrui-lo como rodar um jogo feito da Engine Godot para funciona numa Tv-Box com modelo Rk322x de 32 bits no sistema operacional LINUX.
* Vale mencionar que, o Godot não tem nenhum exportação oficial para Arm, logo teremos que improvisa. Durante as minhas pesquisas ate o momento atual, so achei suporte não oficial para o Raspberry Pi no Godot, no entanto, nenhum para a Tv-box.
* Se sua TV-Box não é de 32 bits, vá na seção de - [Referencias](#referencia) e utilize os repositorios.

## Pré-Requisitos

Por acaso, voce não instalou nenhuma interface grafica na Tv-box te recomendo ao links mostrado abaixo:
* [FORUM DO AMBIAN COM GUIA PARA INSTALAÇÃO](https://forum.armbian.com/topic/12656-csc-armbian-for-rk322x-tv-boxes/)
* [VÍDEO SEGUINDO O PASSO A PASSO DO FÓRUM](https://www.youtube.com/watch?v=R0zjwQG2iE4&list=PLk7NllGoUvyyPn9xPIZo8to9teh4or7hy&index=9)
-- obs: ele instala uma imagem já com desktop inclusa.
* [VÍDEO COM INSTALAÇÃO INDO MAIS AFUNDO SOBRE O ARMBIAN-CONFIG](https://youtu.be/R0zjwQG2iE4?si=2xLfhHuFDLLQuAaK)
-- (INCLUINDO INSTALAÇÃO DO DESKTOP)
* LINKS DE LOCAIS PARA BAIXAR IMAGENS (TIRADO DIRETO DO GUIA DO FORUM NA PARTE "Installation (via SD card)")
	- https://imola.armbian.com/dl/rk322x-box/archive/
	- https://github.com/armbian/community
	- https://users.armbian.com/jock/rk322x/armbian/stable

### Configurações do sistema da Tv-Box
```
Distribuição Linux: Debian/Ubuntu
Versão da Distribuição: 11
Nome do Kernel: rk332x-box 
Versão do Kernel: 4.4.194-legacy-rk332x
Arquitetura: armv7l
Nome do modelo: Cortex-A7
CPU: 4
CPU max MHz: 1200,00
CPU min MHz: 408,00
```

## Instalações

Primeiramente, instale o Godot 2.1.6 no computador de sua preferencia, pois para exportar o jogo, não é necessario que instale o Godot na Tv-box. Após isso, vá na sua TV-Box e acesse nesse link https://docs.godotengine.org/en/3.6/development/compiling/compiling_for_x11.html e faça uma leitura para melhor entendimento. Instale os requisitos como o (GCC+, Clang+, Python e entres outros), verifique qual distro do linux que esta instalado na Tv-Box, copie e execute no prompt de comando. Feito isso, não vai ser mais necessario realizar os seguintes passos do documento.

Segundamente, ainda na Tv-Box, acesse nesse link https://downloads.tuxfamily.org/godotengine/, encontre a pasta "2.1.6", e instale a pasta "godot-2.1.6-stable.tar.xz" na sua TV-Box. Em seguida, renomei a pasta que extraiu para "godot" (Opcional). Inicie um terminal, vá para o diretório raiz da pasta "godot" e digite:
```
scons platform=x11 target=release tools=no use_llvm=yes CCFLAGS="-mcpu=arm1176jzf-s -mtune=arm1176jzf-s -mfpu=vfp -mfloat-abi=hard -mlittle-endian -munaligned-access" -j1
```
Essa linha de comando vai criar um modelo de exportação que será utilizado no Godot 2.1.6. OBS: Isso pode demorar alguns minutos ou horas dependendo do hardware da TV-Box, no meu caso, demorou muito kkk. Outra observaçao, o arquivo gerado vai esta na pasta do "godot" -> "bin", e caso a extensão do arquivo esteja 'lvmn' ou outro nome, renomei a extensão para 'bin'.

Com pendrive, leve esse arquivo para o seu computador na qual esta instalado o Engine Godot, e no momento de exportação do jogo faça:

#### Como exportar um jogo usando os modelos de exportação
- No Editor, vá para `Export`.
- Selecione o `Linux/X11`.
- Em `Debug`, Desmaque `Debugging Enabled`.
- Em `Custom Binary -> Release`, selecione o arquivo que esta no Pendrive.
- Em `Binary`, Desmaque `64 bits`*.
- Click `Export`.
- Você pode usar a extensão `.32` ao nomear o jogo exportado.

#### Como exportar um arquivo PCK independente
- No Editor, vá para `Export`.
- Selecione o `Linux/X11`.
- Em `Binary`, Desmaque `64 bits`*.
- Click `Export PCK/ZIP`.
- Digite o nome do seu jogo com a extensão `.pck` na mesma pasta do jogo.
- Click `OK`.

Coloque a pasta do jogo no Pendrive e extrai na sua TV-Box. Para executa o jogo, inicie o terminal, vá ate a pasta que esta com o arquivo do jogo e faça. (Supondo que voce colocou o nome do jogo como 'Binary.32')
```
./Binary.32
```

Pronto, o seu jogo vai rodar.

## Referencias

Esses repositorios linkados nessa seção foram os que peguei para ter a noção de como rodar o jogo. Vale mencionar, que no meu caso, nenhum modelos de exportação oferecidos pelos repositorios abaixo não foram possivel rodar o jogo na minha TV-Box. Mas caso sua Tv-Box seja diferente em algum aspecto da minha, vale a pena tentar rodar o jogo com algum modelo de exportação disponivel. 

* [Unofficial-Godot-Raspberry](https://github.com/hiulit/Unofficial-Godot-Engine-Raspberry-Pi)
* [FRT](https://github.com/efornara/frt)





