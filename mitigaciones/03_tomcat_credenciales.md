# Mitigación 4 · Tomcat con credenciales por defecto (8180/tcp)

```bash
# Respaldo
sudo cp /etc/tomcat5.5/tomcat-users.xml /etc/tomcat5.5/tomcat-users.xml.bak

# Reemplazar las contraseñas de las 3 cuentas por valores robustos
sudo nano /etc/tomcat5.5/tomcat-users.xml
#   <user username="..." password="<NUEVA_CONTRASEÑA_ROBUSTA>" roles="..."/>

# Validar la sintaxis XML antes de reiniciar
xmllint --noout /etc/tomcat5.5/tomcat-users.xml && echo "XML válido"

sudo /etc/init.d/tomcat5.5 restart
sudo netstat -tlnp | grep 8180
```

## Verificación desde Kali
```bash
curl -s -o /dev/null -w "%{http_code}\n" -u tomcat:tomcat http://<APP>:8180/manager/html
# 401
```

**Riesgo residual:** la consola sigue expuesta, Tomcat sigue desactualizado y el conector AJP (*Ghostcat*) sigue crítico. Solo verifiqué una ruta de acceso.
