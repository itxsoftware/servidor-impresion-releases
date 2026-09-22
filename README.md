# Servidor de impresión ITX

Instaladores del Servidor de impresión de ITX Software. Este repo solo publica los instaladores: no tiene código.

## Descargar

**[Última versión → Releases](https://github.com/itxsoftware/servidor-impresion-releases/releases/latest)**

En **Assets**, bajar `Setup-ServidorImpresion-<version>.exe`. No hace falta cuenta de GitHub.

No bajes los links *Source code (zip)* ni *Source code (tar.gz)*. GitHub los agrega solo a todos los releases y adentro no hay nada útil.

Desde la terminal, con [GitHub CLI](https://cli.github.com/):

```powershell
gh release download -R itxsoftware/servidor-impresion-releases --pattern "Setup-*.exe"
```

### Verificar la descarga (opcional)

Cada release trae un `.sha256` junto al instalador. Para comprobar que el archivo bajó entero:

```powershell
Get-FileHash .\Setup-ServidorImpresion-<version>.exe -Algorithm SHA256
```

El hash tiene que ser el mismo que figura en `Setup-ServidorImpresion-<version>.exe.sha256`.

## Instalar

1. Ejecutar `Setup-ServidorImpresion-<version>.exe` en la PC del local.
2. Si Windows muestra *"Windows protegió su PC"*, tocar **Más información → Ejecutar de todas formas**. Aparece porque el instalador no está firmado.
3. Elegir para quién se instala:
   - **Solo para mí** (recomendado): no pide permisos de administrador, tampoco en las actualizaciones automáticas.
   - **Para todos los usuarios**: pide permiso de administrador al instalar y en cada actualización automática.
4. Al terminar se abre el servidor. Completar empresa, sucursal, impresora por defecto y base de datos, y tocar **Guardar**.

El servidor arranca solo cada vez que se inicia sesión en Windows y queda en la bandeja del sistema, junto al reloj.

## Actualizar

**Las actualizaciones son automáticas.** El servidor busca una versión nueva un minuto después de arrancar y después cada 6 horas. Si la encuentra, la baja y avisa con un globo en la bandeja. La instalación se hace **en el próximo arranque** para no cortar una impresión: el próximo inicio de sesión de Windows, o cerrar con *Salir* y volver a abrir.

Para instalarla en el momento, usar **Actualizar ahora** en el menú de la bandeja.

**Las versiones `v14.09.2026` y anteriores no se actualizan solas.** Hay que instalarles a mano una versión nueva una sola vez, bajándola del link de arriba. Desde ahí se actualizan solas.

Instalar una versión nueva encima de la anterior también actualiza, y se conserva la configuración.

## Desinstalar

Desde **Configuración → Aplicaciones**, buscar *Servidor de impresión ITX*. Al desinstalar no se borra la configuración (`C:\servImp\empSuc.txt`): si se vuelve a instalar, arranca con los mismos datos.

## Si algo falla

Los registros de la actualización automática están en `%LocalAppData%\ITX Software\Servidor de impresion\updates\`:

- `update.log`: una línea por cada chequeo, descarga o instalación.
- `setup.log`: la salida del instalador. Si `update.log` dice "Lanzado ..." pero la versión no cambió, el motivo está acá; por ejemplo, se canceló el permiso de administrador.
