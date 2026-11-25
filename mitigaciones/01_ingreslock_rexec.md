# Mitigación 1 y 2 · Ingreslock (1524/tcp) y rexec (512/tcp)

Ambos servicios se lanzaban desde el superservidor `inetd`/`xinetd`.

```bash
# Estado inicial
sudo netstat -tlnp | grep -E ':1524|:512'
ls /etc/xinetd.d/
grep -nE '^(ingreslock|exec)' /etc/inetd.conf

# Respaldo y deshabilitación (comentar las líneas)
sudo cp /etc/inetd.conf /etc/inetd.conf.bak
sudo sed -i -E 's/^(ingreslock|exec)([[:space:]])/#\1\2/' /etc/inetd.conf
grep -nE '^#(ingreslock|exec)' /etc/inetd.conf

# Aplicar
sudo /etc/init.d/xinetd restart
```

## Verificación desde Kali
```bash
sudo nmap -p 1524,512 <APP>
# 1524/tcp closed ingreslock
# 512/tcp  closed exec
```

**Riesgo residual:** deshabilitar Ingreslock no descarta que el sistema ya estuviera comprometido. Lo correcto es reconstruirlo desde una imagen confiable. rlogin y rsh (513–514) siguen expuestos.
