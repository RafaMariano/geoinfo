# Instalação do QGIS para Linux Ubuntu


## Descobrindo sua Versão do Linux Ubuntu

Para saber o nome da sua distribuição Linux, utilize o comando `lsb_release`, como indicado abaixo:
```bash
$ lsb_release -a
```

A saída do comando acima apresentará o codenome (`Codename`) da sua distribuição:
```
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 18.04.3 LTS
Release:	18.04
Codename:	bionic
```


## Acrescentando o Repositório do QGIS no Sistema de Pacotes do Ubuntu

Edite o arquivo `/etc/apt/sources.list` e adicione o repositório do QGIS, conforme indicado abaixo. Lembre-se de substituir o nome `bionic` pela distribuição que você está usando (`bionic`, `buster`, `cosmic`, `jessie`, `precise`, `stretch`, `trusty`, `xenial`).

Para edição do arquivo, você pode utilizar o `vi`:
```bash
$ sudo vi /etc/apt/sources.list
```
ou, se preferir, pode usar o `gedit`:
```bash
$ sudo gedit /etc/apt/sources.list
```

Acrescente o seguinte conteúdo ao final do arquivo:
```
# QGIS
deb         http://qgis.org/ubuntu-ltr bionic main
deb-src     http://qgis.org/ubuntu-ltr bionic main
```

Após salvar o conteúdo acima, adicione a chave pública do repositório:

```bash
$ wget -O - https://qgis.org/downloads/qgis-2019.gpg.key | gpg --import

$ gpg --fingerprint 51F523511C7028C3
```

O último comando acima deverá produzir uma saída como:
```
pub   rsa4096 2019-08-08 [SCEA] [expires: 2020-08-08]
      8D5A 5B20 3548 E500 4487  DD19 51F5 2351 1C70 28C3
uid           [ unknown] QGIS Archive Automatic Signing Key (2019) <qgis-developer@lists.osgeo.org>
```

Após verificar o *fingerprint*, adicione a chave com o seguinte comando:
```bash
$ gpg --export --armor 51F523511C7028C3 | sudo apt-key add -
```

Atualize seu sistema de pacotes e verifique se não houveram erros introduzidos pelas modificações realizadas nos passos acima:

```bash
$ sudo apt-get update
```

O resultado desse último comando dever indicar sucesso:
```
...
Reading package lists... Done
```

**Observação:** Caso você tenha recebido uma mensagem como mostrada abaixo, trata-se de um indicativo de que a configuração do seu sistema  encontra-se incorreta. Neste caso, revise as instruções anteriores.
```
...
Reading package lists... Done
W: GPG error: http://qgis.org/ubuntu-ltr bionic InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 51F523511C7028C3
E: The repository 'http://qgis.org/ubuntu-ltr bionic InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```


## Instalação da Versão 3.4.x LTR

No curso, utilizaremos a versão estável 3.4 LTR (Long Term Release). Utilize o seguinte comando para instalação:

```bash
$ sudo apt-get install qgis qgis-plugin-grass qgis-server
```

Mais informações sobre a instalação no `Linux Ubuntu` podem ser encontradas em: [QGIS Installers](https://www.qgis.org/en/site/forusers/alldownloads.html#debian-ubuntu).