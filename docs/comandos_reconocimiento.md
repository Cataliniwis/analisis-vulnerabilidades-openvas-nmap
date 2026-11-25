# Comandos de reconocimiento (Nmap / NSE)

> `<APP>` = servidor de ventas de laboratorio · `<STOCK>` = servidor de inventario de laboratorio

| Objetivo | Comando |
|---|---|
| Barrido completo de puertos TCP y versiones | `sudo nmap -sV -p- <APP> -oN app-ventas-nmap.txt` |
| Telnet (23/tcp) | `sudo nmap -sV --reason -p 23 <APP>` y luego `telnet <APP>` |
| FTP anónimo (21/tcp) | `sudo nmap -sV -p 21 --script ftp-anon,ftp-syst <APP>` y luego `ftp <APP>` (usuario `anonymous`) |
| Servicios r* heredados | `sudo nmap -sV --reason -p 512,513,514 <APP>` |
| Cabeceras y métodos HTTP | `sudo nmap -sV -p 80 --script http-headers,http-methods <APP>` |
| SMBv1 y firma SMB | `sudo nmap -p 139,445 --script smb-protocols,smb-security-mode <APP>` |
| Exportaciones NFS | `sudo nmap -p 2049 --script nfs-showmount,nfs-ls <APP>` |
| Barrido del servidor de inventario | `sudo nmap -sV -p- <STOCK> -oN stock-lab-nmap.txt` |
| Algoritmos y autenticación SSH | `sudo nmap -p 22 --script ssh2-enum-algos,ssh-auth-methods <STOCK>` |

## Configuración de Greenbone/OpenVAS

| Parámetro | Valor |
|---|---|
| Perfil | Full and fast |
| Lista de puertos | All TCP and Nmap top 100 UDP |
| NVT simultáneos por host | 4 |
| Filtro de resultados | QoD ≥ 70 % |
| Alcance | Una tarea por activo, solo direcciones privadas del laboratorio |
