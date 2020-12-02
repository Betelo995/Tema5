# Modelos Probabilísticos IE0405
# Laboratorio 5
## Isaac Rojas Hernández
### B76693
### Jueves 3 de Diciembre del 2020
### Profesor Fabián Abarca

En el presente laboratorio se debía modificar el código pre-establecido para que cumpliera con los requisitos solicitados. En este caso, el requisito indicaba que el servicio que se tenía previamente no debía superar el 10\% del tiempo, completamente vacío o sin atender a ningún cliente. 
En este caso se reutiliza la fórmula anterior, sin embargo se toma en cuenta que ahora para que el servidor no esté vacío debe hacerse para 1 o más clientes de forma que se vería la siguiente ecuación: 
<img src="https://render.githubusercontent.com/render/math?math=P( \text{1 o más clientes en el sistema} ) = \sum_{i=1}^{\infty} (1 - \rho) \rho^i  = 1 - \sum_{i=0}^{1} (1 - \rho) \rho^i = \rho^2">

La solución obtenida de wolfram alpha nos da como resultado para este caso que <img src="https://render.githubusercontent.com/render/math?math=P_{i \geq i} = \rho ^{2}">. Ahora como se desea que el servicio no esté vacío más del 10\% del tiempo, significa que la probabilidad obtenida anteriormente debe ser mayor al 90\%, teniendo entonces que: 
<img src="https://render.githubusercontent.com/render/math?math=P(\text{1 o mas clientes en el sistema}) = \rho^{2} \geq 0.9 ">


Cambiando <img src="https://render.githubusercontent.com/render/math?math=\rho"> por su equivalente se tiene que: 

<img src="https://render.githubusercontent.com/render/math?math=\rho^{2} \geq 0.9">
<img src="https://render.githubusercontent.com/render/math?math=\left ( \frac{\lambda}{\nu} \right )^{2} \geq 0.9">
<img src="https://render.githubusercontent.com/render/math?math=\nu^{2}\leq \frac{2^{2}}{0.9} \Rightarrow \nu \leq 2.11 ">

Ahora si bien la parte matemática se ve de esta forma en el código provisto era necesario cambiar primero el valor de <img src="https://render.githubusercontent.com/render/math?math=\nu">, para que estuviera acorde a lo averiguado anteriormente por lo tanto en el código se cambió: 
```Python
# Parámetro de servicio (servicios/segundos)
nu = 2.11/60 #Escogiendo 2.11 al ser el mayor valor permitido. 

```
Luego se debía también cambiar el criterio de aprobación de la especificación dada, para que ahora calzara con que <img src="https://render.githubusercontent.com/render/math?math=P(\text{1 o más personas en el servicio}) \geq 0.90">.

```Python 
fraccion = frecuencia / len(t)
if fraccion >= 0.9:  #se modifica para que verifique que la fracción es mayor a 0.9, que cumpliría el criterio estupilado por el enunciado
    print('\t Sí cumple con la especificación.')
else:
    print('\t No cumple con la especificación.') 
print('Simulación es equivalente a {:0.2f} horas.'.format(len(t)/3600))
```


