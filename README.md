# ecc-nube

El plugin ECC que uso con Claude Code, empaquetado en un solo archivo para que las
sesiones de Claude Code en la nube lo puedan bajar al arrancar.

ECC es [affaan-m/ECC](https://github.com/affaan-m/ECC) (licencia MIT), recortado y
adaptado a mi forma de trabajar: el ciclo plan, test, implementar, revisar y
verificar, con una cascada que reparte el trabajo entre Haiku, Sonnet y Opus según
lo difícil que sea cada parte. Trae 38 agentes, 22 comandos, 79 skills y sus hooks.

## Qué hay aquí

- `ecc-plugin.tar.gz`: la carpeta `plugin/` del repo donde mantengo ECC, tal como
  quedó en un commit.
- `version.txt`: la versión del plugin, el commit del que sale y el sha256 del
  archivo.

Este repo es público por una razón práctica: una sesión en la nube solo puede
leer el repo en el que trabaja y archivos de repos públicos. El repo de trabajo
de ECC sigue privado.

## Cómo se usa

El script de arranque del entorno en la nube baja el archivo desde un commit fijo
de este repo:

```
https://raw.githubusercontent.com/B3njjaman/ecc-nube/<commit>/ecc-plugin.tar.gz
```

Antes de instalarlo revisa que el sha256 sea el que tiene anotado. Si no coincide,
no instala nada. Si coincide, lo deja en `~/.claude/skills/ecc/`, donde Claude Code
lo carga como el plugin `ecc@skills-dir`. Como la URL apunta a un commit y no a
`main`, un cambio en este repo no llega a las sesiones hasta que actualizo el
script.

Si quieres probarlo en tu máquina, descomprime el archivo en una carpeta dentro de
`~/.claude/skills/` y abre Claude Code. O, para una sola sesión:

```bash
mkdir ecc && tar -xzf ecc-plugin.tar.gz -C ecc
claude --plugin-dir ecc/plugin
```

## Cómo se actualiza

El paquete se arma con `git archive` sobre un commit, así que entra solo lo
commiteado y el mismo commit da el mismo archivo byte a byte. Antes de armarlo, el
script revisa que no haya archivos con nombre de credencial ni palabras de una
lista que guardo fuera de los repos. Cada versión nueva entra por un PR.

## Licencia

MIT, la misma de ECC. El aviso original está en `LICENSE`.
