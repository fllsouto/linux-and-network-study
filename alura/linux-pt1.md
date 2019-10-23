# Linux Parte 1

[Link](https://cursos.alura.com.br/course/linux-ubuntu)

- [Artigos para ler](#artigos-para-ler)
- [Referência interessantes](#refer%c3%aancia-interessantes)
- [Aula 1](#aula-1)
- [Aula 2](#aula-2)
- [Alura 3](#alura-3)
  - [Compactar arquivos](#compactar-arquivos)
  - [Compactar arquivos recursivamente](#compactar-arquivos-recursivamente)
  - [Compactar arquivos recursivamente e sem output](#compactar-arquivos-recursivamente-e-sem-output)
  - [Lista os arquivos dentro do zip](#lista-os-arquivos-dentro-do-zip)
  - [Descompactar arquivos com ou sem output](#descompactar-arquivos-com-ou-sem-output)
- [Aula 4](#aula-4)
  - [Comandos tar para empacotamento e compressão](#comandos-tar-para-empacotamento-e-compress%c3%a3o)
  - [Comandos tar para desempacotamento e descompressão com gzip](#comandos-tar-para-desempacotamento-e-descompress%c3%a3o-com-gzip)
  - [Comandos tar para desempacotamento e descompressão (gzip) em outro diretório](#comandos-tar-para-desempacotamento-e-descompress%c3%a3o-gzip-em-outro-diret%c3%b3rio)
  - [Comandos tar compressão e descompressão (bzip2)](#comandos-tar-compress%c3%a3o-e-descompress%c3%a3o-bzip2)
  - [Impressão de arquivos](#impress%c3%a3o-de-arquivos)
- [Aula 5](#aula-5)

## Artigos para ler

- [How do the internals of sudo work?](https://unix.stackexchange.com/questions/80344/how-do-the-internals-of-sudo-work)

## Referência interessantes

- [About Unix sudo and su commands](https://kb.iu.edu/d/amyi%20%27%27referencia%27%27)
- [How to List Users in Linux](https://linuxize.com/post/how-to-list-users-in-linux/)
- [How To Create a Sudo User on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart)

## Aula 1

A primeira aula apresenta os comandos básicos do linux e qual a utilidade de cada um deles:

- `pwd`: para descobrir o diretório atual.
- `ls`: para listar arquivos e diretórios, vimos as opções `-l` e `-la`, que listam além dos arquivos e diretórios ocultos, informações extras sobre cada um deles.
- `echo` para imprimir mensagens e o operador `>` para modificar o destino da mensagem.
- `clear` para limparmos o terminal.
- `man` para consultar o manual sobre determinado comando.
- setas para cima e para baixo para navegador no histórico de comandos do terminal.

## Aula 2

- Podemos descobrir qual diretório que estamos, utilizando o `pwd`
- O cat em conjunto com o asterisco imprime o conteúdo de todos os arquivos que derem match, por exemplo: `cat "*.txt"`
- Existe o comando rmdir para apagar diretórios desde que estejam vazios

## Alura 3

Posso usar o comando zip para diversas coisas: 

### Compactar arquivos

```bash
# comando: zip - qr nome-do-arquivo.zip nome-do-alvo

zip workspace.zip nome-da-pasta/
```

Esse comando fará com que o arquivos nessa pasta no primeiro nível seja adicionados, mas o que estiver dentro de pastas não serão, **pois o comando não é recursivo**. Para adicionar de forma recursiva precisamos adicionar o parâmetro `-r`.

### Compactar arquivos recursivamente

```shell
zip -r workspace.zip nome-da-pasta/

# ou

zip --recursive workspace.zip nome-da-pasta/
```



Ao executar a compressão de uma pasta várias informações aparecerão no terminal, o que muitas vezes pode ser um pouco incomodo. Podemos pedir para que essa saída seja omitida, através da flag `-q` ,que serve para diminuir a output do programa.

### Compactar arquivos recursivamente e sem output

```shell
zip -qr workspace.zip nome-da-pasta/
```

Oposto a operação de compressão de arquivos, podemos descomprimir, utilizando o programa **unzip**. Temos alguns comandos úteis:

### Lista os arquivos dentro do zip

```shell
$ unzip -l work.zip 
Archive:  work.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
        0  2016-02-17 13:41   workspace/
        0  2016-02-17 12:35   workspace/projetos-java/
       10  2016-02-17 12:34   workspace/projetos-java/bemvindo.txt
        0  2016-02-17 12:35   workspace/projetos-c#/
       10  2016-02-17 12:35   workspace/projetos-c#/bemvindo.txt
       10  2016-02-17 12:35   workspace/bemvindo.txt
    29877  2016-02-17 12:44   workspace/google.txt
        0  2016-02-17 12:35   workspace/projetos-php/
       10  2016-02-17 12:34   workspace/bemvindo2.txt
---------                     -------
    29917                     9 files
```

### Descompactar arquivos com ou sem output

```shell
$ unzip work.zip 
Archive:  work.zip
   creating: workspace/
   creating: workspace/projetos-java/
 extracting: workspace/projetos-java/bemvindo.txt  
   creating: workspace/projetos-c#/
 extracting: workspace/projetos-c#/bemvindo.txt  
 extracting: workspace/bemvindo.txt  
  inflating: workspace/google.txt    
   creating: workspace/projetos-php/
 extracting: workspace/bemvindo2.txt
 
 #Não tem saída
 $ unzip -q work.zip
```

## Aula 4

O comando **tar** é usado para compactar arquivos na extensão tar, o que é bastante comum no Linux. Na verdade o tar serve para empacotar os arquivos em um só lugar, para facilitar a transferência de um ponto para o outro. Podemos usar ele associado ao **gzip ou bzip2**.

### Comandos tar para empacotamento e compressão

```shell
 # Cria um arquivo empacotado, com quase o mesmo tamanho do original
 $ tar -c workspace/ > work-tar.tar
 
 # Agora empacotaremos e compactaremos
 $ tar -cz workspace/ > work-tar.tar.gz
 
 # Podemos também definir o nome do arquivo, sem ter que usar o redirecionamento
 # O parâmetro f tem que ser o último pois ele referencia o que vem logo em seguida
 $ tar -czf workspace.tar.gz workspace/
 
 # Podemos também manipular o nível de verbosidade da saída
$ tar -czv -f workspace2.tar.gz workspace 

workspace/
workspace/google.txt
workspace/projetos-php/
workspace/bemvindo2.txt
workspace/projetos-java/
workspace/projetos-java/bemvindo.txt
workspace/bemvindo.txt
workspace/projetos-c#/
workspace/projetos-c#/bemvindo.txt
```

### Comandos tar para desempacotamento e descompressão com gzip

Todos os comandos a seguir podem ter o sinal de **-** omitido.

```shell
# A forma mais simples de descompactar um arquivo, a opção -x significa "extract"
$ tar -zx < nome-do-arquivo.tar.gz

# Podemos também dizer através do parâmetro -f qual o arquivo que estamos descompactando, evitando assim o redirecionamento da entrada
$ tar -zxf nome-do-arquivo.tar.gz

# ou
$ tar -zx -f nome-do-arquivo.tar.gz

# Por padrão a descompactação não tem saída, caso seja necessário basta passar o parâmetro -v
$ tar -zxvf workspace2.tar.gz 
workspace/
workspace/google.txt
workspace/projetos-php/
workspace/bemvindo2.txt
workspace/projetos-java/
workspace/projetos-java/bemvindo.txt
workspace/bemvindo.txt
workspace/projetos-c#/
workspace/projetos-c#/bemvindo.txt
```

### Comandos tar para desempacotamento e descompressão (gzip) em outro diretório

Referência: [How to extract files to another directory using 'tar' command?](https://askubuntu.com/questions/45349/how-to-extract-files-to-another-directory-using-tar-command)

```shell
# Para extrair o arquivo para um pasta particular precisamos primeiro criar a nossa pasta de destino
$ mkdir pasta-foo
$ tar -zxv -f workspace.tar.gz -C pasta-foo/
# Ainda teremos o primeiro nível da nossa pasta
$ ls pasta-foo 
workspace

# Esse comando pode ser feito em apenas uma linha
$ mkdir pasta-bar && tar -zxv -f workspace.tar.gz -C pasta-bar/

# Podemos também remover o primeiro nível da nossa pasta
$ mkdir pasta-bar && tar -zxv -f workspace2.tar.gz -C pasta-bar/ --strip-components=1
workspace/google.txt
workspace/projetos-php/
workspace/bemvindo2.txt
workspace/projetos-java/
workspace/projetos-java/bemvindo.txt
workspace/bemvindo.txt
workspace/projetos-c#/
workspace/projetos-c#/bemvindo.txt

$ ls
pasta-bar  workspace

$ ls pasta-bar 
bemvindo2.txt  bemvindo.txt  google.txt  projetos-c#  projetos-java  projetos-php
```

### Comandos tar compressão e descompressão (bzip2)

Para mudar o tipo de compressão basta trocar o parâmetro por **-j**. A vantagem do bzip2 sobre o gzip é sua maior capacidade em gerar arquivos menores, só que isso aumenta também o tempo necessário para descompactar.

```shell
$ tar -cjv -f workspace.tar.bz2 workspace/
workspace/
workspace/google.txt
workspace/projetos-php/
workspace/bemvindo2.txt
workspace/projetos-java/
workspace/projetos-java/bemvindo.txt
workspace/bemvindo.txt
workspace/projetos-c#/
workspace/projetos-c#/bemvindo.txt

```

### Impressão de arquivos

Temos diversos comandos para visualizar arquivos:

- `cat`: imprime todo o arquivo no terminal
- `less`: mostra o arquivo no terminal, de forma procedural
- `head`: mostra o começo do arquivo
- `tail`: mostra o fim do arquivo

Esses comandos aceitam diversos parâmetros, como por exemplo o `tail --lines 10`, que imprime as ultimas 10 linhas do arquivo. 

## Aula 5
- No VI podemos copiar linhas com o comando `yy` e colar com o comando  `p`
- Podemos repetir um determinado comando colocando um numero na frente dele, por exemplo `6yy` ou `8p`
- Podemos também navegar entre o primeiro e o ultimo carácter de uma linha, com `0` e `$` respectivamente
