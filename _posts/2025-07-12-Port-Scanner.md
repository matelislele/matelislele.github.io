## Terrible Port Scanner

## About
Padariau port scanneri pythone. 

Čia mano paprastas portų skeneris, parašytas su Python. Jis tikrina, ar tam tikri prievadai (nuo 50 iki 84) yra atviri pasirinktame IP adrese.

Programa paleidžiama per terminalą, įvedus IP adresą kaip argumentą. Ji tada bando prisijungti prie kiekvieno porto ir parodo, kurie veikia (yra atviri).

- Tikrina TCP Portus nuo 50 iki 84.
- Parodo IP adresą ir laiką, kada pradėtas skanavimas
- Jei įvedi blogą adresą – išmeta klaidą
- Jei paspaudi `Ctrl+C` – gražiai užsidaro

## Kaip paleisti

```bash
python3 port_scanner.py <IP_adresas>
```

## Reflection
Manau man sekesi gerai, zinau kad jis gaidys, bet svarbu kad veikia.

Sunkumas - 4/10

Panaudojimas - 6/10

Kokybe - 3/10



```python
import sys
import socket
from datetime import datetime

#define the target
if len(sys.argv) == 2: #argv yra argumentu skaicius. pvz py port_scanner.py (1 argumentas) <ip> (2 argumentas)
    target = socket.gethostbyname(sys.argv[1]) #Translate hostname to IPv4
else:
    print("Invalid amount of arguments.")
    print("Syntax: python3 port_scanner.py <ip>")

#Add a pretty banner
print("-" * 50)
print("Scanning target: " + target)
print("Time started: " + str(datetime.now()))
print("-" * 50)

try:
    for port in range(50, 85):
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        socket.setdefaulttimeout(1)
        result = s.connect_ex((target, port))
        if result == 0:
            print(f"Port {port} is open")
        s.close()
except KeyboardInterrupt:
    print("\nExiting program.")
    sys.exit()

except socket.gaierror:
    print("Hostname could not be resolved.")
    sys.exit()

except socket.error:
    print("Couldn't connect to server.")
    sys.exit()
```
