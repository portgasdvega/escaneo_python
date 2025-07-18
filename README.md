¡Perfecto, Emiliano!
Vamos a dejar tu proyecto documentado de forma profesional, clara y útil, sin adornos innecesarios.

---

## 📄 `README.md` para tu script de escaneo

Aquí tienes una versión sólida que puedes usar directamente en tu repositorio de GitHub:

---

#  Escáner de Puertos Automatizado con Python y Nmap

Este script automatiza un escaneo rápido de puertos TCP utilizando `nmap`, con opción para guardar los resultados en un archivo `.txt`. Es ideal para tareas de reconocimiento básicas en redes o prácticas de hacking ético.

---

## ¿Qué hace este script?

- Limpia la consola al iniciar
- Solicita al usuario una IP o dominio para escanear
- Ejecuta `nmap -sS -Pn` sobre el destino
- Pregunta si deseas guardar el resultado en un archivo
- Si aceptas:
  - Guarda la fecha y hora del escaneo
  - Guarda el resultado del escaneo en el archivo especificado

---

## Requisitos

- Python 3.x
- `nmap` instalado en el sistema
- Permisos `sudo` si el escaneo requiere privilegios elevados
- Sistema operativo basado en Linux (por el uso de `shell=True` con comandos como `clear` y `tee`)

---

## Ejemplo de uso

```bash
$ python3 scanner.py
Ingrese la IP o Dominio: 8.8.8.8
Desea almacenar el resultado en un archivo .txt(y/n)?: y
Como lo quieres nombrar: google.txt
````

Archivo `google.txt` generado:

```
2025-07-18 15:05:24.232825
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-07-18 15:05 CST
Nmap scan report for dns.google (8.8.8.8)
Host is up (0.028s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT    STATE SERVICE
53/tcp  open  domain
443/tcp open  https
```

---

## Estructura del código

```python
import subprocess as sp
from datetime import datetime

sp.run("clear",shell=True)
time = datetime.now()
ip=str(input("Ingrese la IP o Dominio: "))
almac=input("Desea almacenar el resultado en un archivo .txt(y/n)?: ")


while True:
    if almac.lower()=="y":
        txt = input("Como lo quieres nombrar: ")
        sp.run(f"echo {time} >> {txt}", shell=True)
        sp.run(f"sudo nmap -sS -Pn {ip} | tee -a {txt}", shell=True)
        break
    elif almac.lower()=="n":
        print("Ok")
        break
    else:
        print("Error")
```

---

## Notas técnicas

* Se utiliza `shell=True` en todas las llamadas a `subprocess.run()` para mantener el estilo de ejecución tipo terminal.
* El escaneo TCP SYN (`-sS`) requiere privilegios de administrador.
* `-Pn` omite el ping previo, útil para hosts que bloquean ICMP.
* `tee` permite visualizar y guardar al mismo tiempo.

---

## Autor

**Emiliano Martínez Vega**
Script desarrollado como parte de ejercicios de automatización en Python para ciberseguridad.
