---
title: "Guía de Setup de Estilos"
date: 2024-01-19
#description: "Welcome to my blog!"
#summary: "Learn more about me and why I am starting this blog."
#tags: ["welcome", "new", "about", "first"]
draft: true
series: ["Guía de Setup"]
series_order: 2

#date: 2023-01-10
#description: "Welcome to my blog!"
#summary: "Learn more about me and why I am starting this blog."
# description: "Learn how to build Blowfish manually."
# slug: "advanced-customisation"
# tags: ["advanced", "css", "docs"]
---

## Introducción

Este post es la continuación de la Guía de Setup de Programas, en este post encontrarán una guía de configuración que yo he utilizado para poder personalizar el estilo de mi editor de código (VSCode), así como de mi terminal (Git Bash, Bash y Fish).



Por último, indicaré cuales son mis configuraciones de personalización, principalmente estéticas, que suelo utilizar. Por ejemplo, fuentes y colores de terminal, y de editor de código.


## Personalización de Terminal
Para personalizar el aspecto de la terminal, utilizaré el repositorio de Oh My Posh (https://ohmyposh.dev/). En este caso me interesá instalar tanto en Windows (Git Bash) como en Linux (WSL; bash y fish). En este caso deberé instalar el repositorio tanto en Windows como en Linux.

Lo primero que deberemos hacer es instalar una Nerd Font (https://www.nerdfonts.com/) compatible con los temas para la terminal, en mi caso instalaré CaskaydiaCove Nerd Font (Cascadia Code)  que es una fuente que posee ligaduras de diversos símbolos y me gusta cómo se ve. En este caso se descarga la fuente desde el navegador, se descomprime la carpeta y, se seleccionan todos los elementos y con click derecho de instalan. Alternativamente podemos instalar las fuentes con el comando oh-my-posh font install, una vez instalado en los pasos siguientes.

A continuación, podemos ir a la configuración de Windows Terminal, y en el perfil de valores predeterminados ir a apariencia. Aquí cambiamos la fuente que acabamos de instalar, y otras configuraciones adicionales como el tamaño. En esta misma sección, en el apartado de Transparencia, me gusta habilitar el material acrícilico y seleccionar una opacidad del 60%. De esta forma la terminal trasluce ligeramente el fondo que hay ‘detrás’.

### Configuración en Linux
Lo primero será instalar Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"

test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bashrc



(https://docs.brew.sh/Homebrew-on-Linux) 
Luego, lo utilizaremos para instalar el ejecutable oh-my-posh y los temas 
brew install jandedobbeleer/oh-my-posh/oh-my-posh
brew update && brew upgrade oh-my-posh

Para aplicar oh-my-posh a bash, utilizando un tema en particular deberemos hacer lo siguiente. Deberemos modificar el archivo ~/.bashrc, agregando la siguiente línea de código al final del archivo
eval "$(oh-my-posh init bash --config $(brew --prefix oh-my-posh)/themes/{nombre-tema-escogido}.omp.json)"
En {nombre-tema-escogido} colocaremos el tema (https://ohmyposh.dev/docs/themes) de oh-my-posh que nosotros querramos, en mi caso utilizaré powerline.
Podemos llamar a exec bash para actualizar los cambios

Para aplicar oh-my-posh a fish, deberemos tener primero una versión compatible. Para ello nos aseguraremos de instalar la última versión. Por defecto APT (Advanced Packaginf Tool) tiene desactualizada las versiones disponicles de fish. Deberemos, entonces, agregar manualmente la referencia al repositorio de fish a la versión de release actualizada como un PPA (Personal Package Archive). Ejecutaremos la siguiente línea
sudo add-apt-repository ppa:fish-shell/release-3
sudo apt update
sudo apt install fish

Como ya agregamos el tema especifico para Bash, deberemos indicar la siguiente línea en el archivo ~/.config/fish/config.fish, que en caso de no existir, deberemos crearlo

oh-my-posh init fish | source

Esta línea de código utiliza la misma sintaxis de fish, el cual no es compatible con POSIX. Esto es algo importante para tener en consideración al trabajar con él. Para actualizar fish, podemos ejecutar exec fish

Por último, en fish ejecutaremos fish_config y agregaremos las opciones que querramos. En mi caso seleccionaré los colores ayu mirage.









### Configuración en Windows
En mi caso preferiré realizar la instalación mediante scoop, que es un instalador para windows mediante linea de comandos. Debido a que los instalará dentro de una ruta conocida, para luego poder detallarla explícitamente. Dentro PowerShell ejecutaremos los siguientes comandos

> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

Luego, desde bash, instalaremos el repositorio 
scoop install https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/oh-my-posh.json
scoop update oh-my-posh

Luego, para configurar el tema en git bash, seguiremos un paso análogo para bash en Linux, pero actualizando la ruta donde se hayan instalados los temas. Para saber la ruta, podemos llamar a la variable de entorno POSH_THEMES_PATH, podemos imprimirla en bash anteponiendo $. En este caso la línea de código que debemos agregar al archivo ~/.bashrc, desde Git bash:
eval "$(oh-my-posh --init --shell bash --config {ruta_indicada_en_la_variable}/{nombre-tema-escogido}.omp.json)"
Luego, reiniciamos la terminal o ejecutamos exec bash
Mi personalización de VSCode se basa en utilizar la misma fuente de Cascadia Code en tamaño 15. Para activar las ligaduras, debemos ir a Text Editor/Font/Font Ligatures y Edit in setting.json; cambiamos la propiedad “editor.fontLigatures” a true Utilizo la extensión de Material Icon Theme para mejorar los íconos del explorador de archivos según los formatos o tecnologías utilizadas. También, utilizo la extensión de Tokyo Night con el tema Storm para personalizar el color tanto del fondo como de la fuente.
