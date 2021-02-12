# Análisis matemático de AM
---
Ahora toca analizar un poco mas en detalle que es lo que ocurre matemáticamente. Esto nos permitirá entender mejor como se genera una señal de AM, junto con algunos otros conceptos.

La portadora no modulada podría expresarse de la siguiente manera:

$$
E_c(t)=E_c\sin(2\pi f_c t)
$$

Recordando lo que habíamos dicho hasta ahora, la amplitud de la portadora es la que se veía afectada por la señal moduladora, por lo que una primera aproximación a la ecuación de la onda de AM podría ser:

$$
E(t)=E_c+E_m\sin(2 \pi f_m t)
$$

Y hasta aquí, estaríamos solamente sumando y restando los valores instantáneos de la moduladora a la amplitud pico de la portadora. Nos falta aun agregar la variación temporal de la portadora. Si esta amplitud variable, la multiplicamos por la variación temporal de la portadora, obtendremos lo que estamos buscando:

$$
E_{AM}(t) = [E_c+E_m \sin(2 \pi f_m t)]\sin(2 \pi f_c t)
$$

Y esa es la ecuación de una señal de AM. Pero es un tanto incómoda para usar, así que vamos a trabajarla un poco. Recordando al índice de modulación, podemos reescribir la ecuación como:

$$
E_{AM}(t) = [E_c+m E_c\sin(2\pi f_mt)]\sin(2\pi f_ct)
$$

Ahora si distribuimos, nos va a quedar algo espantoso, pero ya lo vamos a arreglar:

$$
E_{AM}(t) = E_c\sin(2\pi f_ct)+m E_c\sin(2\pi f_mt)\sin(2\pi f_ct)
$$

Nos interesa poder simplificar de alguna manera el segundo término. Afortunadamente, existe una identidad trigonométrica que nos va a permitir hacerlo:

$$
\sin(\alpha)\sin(\beta)=\cfrac{1}{2}[\cos(\alpha - \beta)-\cos(\alpha + \beta)]
$$

Entonces reemplazando los argumentos de los senos por alfa y beta, nos va a quedar:

$$
E_{AM}(t) = E_c\sin(2\pi f_ct)+ \cfrac{mE_c}{2}\cos[2\pi(f_c-f_m)t]-\cfrac{mE_c}{2}\cos[2\pi (f_c+f_m)t]
$$

Lo interesante de esta forma de la ecuación de AM, es que nos permite ver muy fácil algunas particularidades de este tipo de modulación. Por ejemplo, notarán que hay tres términos bien definidos a los que llamaremos:

1. Portadora no modulada:

$$
E_c\sin(2\pi f_ct)
$$

2. Frecuencia lateral inferior (FLI o LSF en inglés):

$$
+\cfrac{mE_c}{2}\cos[2\pi(f_c-f_m)t]
$$

3. Frecuencia lateral superior (FLS o USF en inglés):

$$
-\cfrac{mE_c}{2}\cos[2\pi (f_c+f_m)t]
$$

Los términos 2 y 3 nos dan información nueva. Nos dicen que como resultado de mezclar la moduladora y portadora, no tenemos una frecuencia única, sino tres, la de la portadora, la de una frecuencia que está una frecuencia moduladora por debajo de la portadora (lo indica la resta que está dentro del coseno) y una frecuencia que está una frecuencia moduladora por arriba de la portadora (lo que indica la suma dentro del coseno).

También es interesante observar las amplitudes. En el caso de la portadora, se mantiene igual, pero las frecuencias laterales tienen una amplitud definida que es la mitad de la amplitud de la moduladora original (recuerden que m Ec = Em).

A partir de esta ecuación ahora podemos analizar y entender muchas cosas mas de la AM.