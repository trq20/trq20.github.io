<script type="text/javascript" charset="utf-8" 
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML,
https://vincenttam.github.io/javascripts/MathJaxLocal.js"></script>

# Potencia
---

## Contexto
---
La potencia eficaz de la portadora la podemos calcular como:

$$
P_c = \Big (\frac{E_c}{\sqrt{2}} \Big)^2 \frac{1}{R}=\frac{E_c^2}{2R}
$$

La potencia en una de las bandas laterales la podemos expresar como:

$$
P_{BL} = \Big(\frac{mE_c /2}{\sqrt{2}}\Big) ^2 \frac{1}{R}= \frac{m^2E_c^2}{8R}=\frac{m^2}{4} P_c
$$

Mientras que la potencia de ambas bandas laterales será el doble:

$$
P_{2BL} = \frac{m^2}{2} P_c
$$

Finalmente, la potencia total de la señal de AM será:

$$
P_t = P_c + P_{2BL} = P_c \Big( 1 + \frac{m^2}{2}\Big)
$$

## Resolver
---
### Problema 1
Para una onda de AM con $E_c=10 \space V$, una resistencia de carga de 50 Ω e índice de modulación 1, determinar:  
- Las potencias de la portadora y las bandas laterales.
- La potencia total de las bandas laterales.
- La potencia total de la onda modulada.
- Repetir los ítems anteriores con un índice de modulación 0,5.

### Problema 2
Para un índice de modulación 0,2 y una portadora con potencia de 1000 W, determinar:
- Potencia total de la banda lateral.
- Potencia de banda lateral superior e inferior.
- Potencia total transmitida.

### Problema 3
En una onda de AM de 500 W de potencia total con una modulación del 32%, determinar:
- La potencia de la portadora.
- La potencia de ambas bandas laterales.
- El índice de modulación necesario para que la potencia de ambas bandas laterales sea de al menos 50 W.

Lo que resuelvan, lo van a escribir en un `README.md` escribiendo las ecuaciones en un lenguaje que se llama `LaTeX`. 

## Orientación
---
- Pueden encontrar una referencia al lenguaje `LaTeX` en esta [página](https://en.wikibooks.org/wiki/LaTeX/Mathematics).
- Como GitHub no renderiza bien las ecuaciones en `Markdown`, vamos a tener que usar una herramienta adicional para que se vean bien en el repositorio. En vez de escribir las fórmulas entre `$$ $$`, van a escribir esto en su lugar:

```html
<img src="https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1">
```

Y reemplazan lo que viene después de `math=` por la fórmula que quieran.

## Como entregar
---
Dentro de la carpeta `pset1/potencia` abrir la terminal y escribir `git init`. Luego, crear un archivo dentro de la carpeta que se llame `README.md`. El archivo debe tener este contenido:

```markdown
# Potencia

Alumno: Nombre y apellido
Curso: Curso
Materia: Telecomunicaciones II

## Resoluciones
[Todas las cuentas que hayan hecho]
```

Pueden agregar cualquier comentario u observación adicional que crean que pueda ser útil dentro de este archivo.

En la terminal ahora corran los comandos:

```
git add .
git commit -m "Initial commit"
git checkout -b teleco2/2021/am/potencia
```

Por ultimo, hacer un push de la rama que recién crearon al repositorio en GitHub con:

```
git push https://github.com/trq20/USERNAME.git teleco2/2021/am/potencia
```

Recuerden cambiar `USERNAME` por su nombre de usuario en GitHub. Pueden verificar si la entrega se hizo visitando el repositorio en `https://github.com/trq20/USERNAME/tree/teleco2/2021/am/potencia`. Si al entrar al link no encuentran nada, vuelvan a verificar los pasos de esta sección.