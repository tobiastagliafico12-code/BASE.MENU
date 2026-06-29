# 🚀 BASE DE MENU INTERACTIVO 

¡Bienvenido! Esta es una base de menú interactiva, moderna y personalizable de **10 opciones**, diseñada para que puedas integrarla fácilmente como la interfaz principal de tus propias herramientas y scripts. 

Le da un toque visual increíble a tus herramientas de consola gracias a su efecto estilo Matrix y feedback sonoro.

---

## ✨ Características

* 🔟 **10 Opciones configurables:** Espacio de sobra para organizar todas tus herramientas.
* 🟢 **Animaciones:** Efectos + animación de carga
* 🔊 **Soporte de Sonido**
* 🎨 **Interfaz Limpia:** Navegación intuitiva y estética cuidada para la consola.
* 🧩 **Modular:** Código organizado para que solo tengas que preocuparte por programar tus funciones.

---

<p align="center">
  <img src=Screenshot_20260629-180655.jpg width="400" alt="Vista Previa BASE MENU"/>
</p>

## Requisitos:
```bash
pkg update && pkg install figlet git -y
```

# PASOS DE INSTALACION:
1. ```bash
   nano menu.sh
   ```
  2. Pegar el script
  3. ctrl + X
  4. ```bash
     chmod +x menu.sh
     ```
  5. ```bash
     ./menu.sh
     ```



## ⚡SCRIPT:
```bash
#!/data/data/com.termux/files/usr/bin/bash

# Colores
GREEN='\033[0;32m'
BRIGHT_GREEN='\033[1;32m'
BLUE='\033[0;34m'
RED='\033[0;31m'
NC='\033[0m'

# Config
VERSION="2.9"
DEV="tobix"
TELEGRAM="tobix_ventas0"
USER_TEXT="tu user"

beep_ok() { echo -e '\a'; sleep 0.05; }
beep_err() { for i in {1..2}; do echo -e '\a'; sleep 0.2; done; }
triple_beep() { for i in {1..3}; do echo -e '\a'; sleep 0.1; done }

loading_bar() {
    echo -ne "${GREEN}[*] INICIANDO SISTEMA ["
    for i in {1..20}; do echo -ne "${BRIGHT_GREEN}█${NC}"; sleep 0.05; beep_ok; done
    echo -e "${GREEN}] 100%${NC}"
    sleep 0.5
    clear
}

glitch_banner() {
    clear
    echo -e "${GREEN}<<${NC}"
    for i in {1..3}; do 
        figlet -f slant "B4S3" | while IFS= read -r line; do
            echo -e "${RED}${line}${NC}"
        done
        sleep 0.08
        clear
        echo -e "${GREEN}<<${NC}"
        figlet -f slant "BASE" | while IFS= read -r line; do
            echo -e "${BRIGHT_GREEN}${line}${NC}"
        done
        sleep 0.08
    done
    echo -e "${GREEN}>>${NC}\n"
}

static_banner() {
    echo -e "${GREEN}<<${NC}"
    figlet -f slant "BASE"
    echo -e "${GREEN}>>${NC}\n"
}

# 1. SCAN AL INICIO
scan_system() {
    echo -e "${GREEN}[*] ESCANEANDO SISTEMA...${NC}"
    for item in Firewall Proxy ROOT DNS IPTABLES; do 
        echo -e "${BRIGHT_GREEN}[OK] ${item}: BYPASS${NC}"
        sleep 0.1
        beep_ok
    done
    echo -e "${BRIGHT_GREEN}[!] ACCESO TOTAL CONCEDIDO\n${NC}"
    sleep 0.3
}

matrix_effect() { 
    clear
    for i in {1..15}; do 
        echo -e "${GREEN}$(head /dev/urandom | tr -dc '01' | head -c 60)${NC}"
        sleep 0.06
    done
    triple_beep
}

# 2. FUNCION 2 COLUMNAS FIXED - Sin el ║ de más a la derecha
box_doble() { 
    printf "${GREEN}║${NC} [${1}] ${2}%-14s ${GREEN}║${NC} [${3}] ${4}%-14s\n" ""
}

# BORDE ANIMADO DOBLE CENTRADO ANCHO 60
animated_box_top() {
    TOTAL=60
    TITLE=" OPCIONES "
    LEFT=$(( (TOTAL - ${#TITLE}) / 2 ))
    RIGHT=$(( TOTAL - LEFT - ${#TITLE} ))

    echo -ne "${GREEN}╔"
    for i in $(seq 1 $LEFT); do echo -ne "═"; sleep 0.01; done
    echo -ne "${TITLE}"
    for i in $(seq 1 $RIGHT); do echo -ne "═"; sleep 0.01; done
    echo -e "${GREEN}╗${NC}"
}

menu() {
clear
static_banner

echo -e "${BLUE}VERSION: $VERSION | DEV: $DEV${NC}"
echo -e "${BLUE}USUARIO: $USER_TEXT | TG: $TELEGRAM${NC}\n"

animated_box_top
echo -e "${GREEN}║${NC}"
box_doble "1" "${BRIGHT_GREEN}OPCION${NC}" "6" "${BRIGHT_GREEN}OPCION${NC}"
box_doble "2" "${BRIGHT_GREEN}OPCION${NC}" "7" "${BRIGHT_GREEN}OPCION${NC}"
box_doble "3" "${BRIGHT_GREEN}OPCION${NC}" "8" "${BRIGHT_GREEN}OPCION${NC}"
box_doble "4" "${BRIGHT_GREEN}OPCION${NC}" "9" "${BRIGHT_GREEN}OPCION${NC}"
box_doble "5" "${BRIGHT_GREEN}OPCION${NC}" "10" "${BRIGHT_GREEN}OPCION${NC}"
echo -e "${GREEN}║${NC}"
echo -e "${GREEN}╠═[0] ${RED}SALIR${NC}" # <- Sin el ╣ de la derecha para dejarlo abierto
echo "" # <- Linea vacia para simular que esta roto

echo -ne "${GREEN}> ${NC}"
read -n1 -s opcion
echo ""

case $opcion in
    1|2|3|4|5|6|7|8|9|10) beep_ok; clear; echo -e "${BRIGHT_GREEN}[+] Ejecutando OPCION $opcion...${NC}"; sleep 1.5 ;;
    0) beep_err; echo -e "${RED}[!] Saliendo...${NC}"; sleep 0.5; clear; exit 0 ;;
    *) beep_err; echo -e "${RED}[!] ACCESO DENEGADO${NC}"; sleep 0.5 ;;
esac
}

# SECUENCIA DE INICIO: 1. FIREWALL/ROOT ETC
glitch_banner
matrix_effect
loading_bar
scan_system # <- Aparece antes del menu

while true; do menu; done
```
