# Mitigación 3 · dRuby/DRb (8787/tcp)

El servicio corría como **root** y se iniciaba automáticamente desde `/etc/rc.local`.

```bash
# Identificar el proceso
sudo netstat -tlnp | grep 8787

# Deshabilitar el inicio automático
sudo cp /etc/rc.local /etc/rc.local.bak
sudo sed -i 's|^\(.*druby_timeserver.rb.*\)$|# \1|' /etc/rc.local

# Detener el proceso en ejecución
sudo kill <PID>
sudo netstat -tlnp | grep 8787   # sin resultados
```

## Verificación desde Kali
```bash
sudo nmap -p 8787 <APP>   # 8787/tcp closed
```

**Riesgo residual:** el código del servicio y la versión obsoleta de Ruby siguen instalados.
