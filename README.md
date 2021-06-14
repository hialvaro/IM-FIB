# Resum IM

Resum amb el contingut més important de cara a l'exàmen final. Elaborat 1 dia abans d'aquest.

## Continguts
# Table of contents

- [Wireless Communication](#wireless-communication)
  - [Introducción](#introducción)
- [Transmisión a distancia mediante radio](#transmisión-a-distancia-mediante-radio)
  - [Las Señales](#las-señales)
  - [Atenuación](#atenuación)
  - [Atenuación](#atenuación)
    - [Reflexión](#reflexión)
    - [Difracción](#difracción)
    - [Zona de Fresnel](#zona-de-fresnel)
    - [Scattering](#scattering)
    - [Multipath Fading](#multipath-fading)
  - [Ruido](#ruido)
  - [Modulación multinivel](#modulación-multinivel)
  - [Códigos de corrección de errores](#códigos-de-corrección-de-errores)
  - [Capacidad del canal](#capacidad-del-canal)
- [OFDM y MIMO](#ofdm-y-mimo)
    - [Delay spread](#delay-spread)
  - [Modulación Multiportadora](#modulación-multiportadora)
  - [OFDM (Overlapping Channels)](#ofdm-overlapping-channels)
    - [802.11a @54Mbps (3/4 64QAM)](#80211a-54mbps-34-64qam)
  - [Diversidad](#diversidad)
  - [MIMO](#mimo)
- [Bluetooth Low Energy (BLE)](#bluetooth-low-energy-ble)
  - [GAP](#gap)
  - [GATT](#gatt)
- [Sensores IMU](#sensores-imu)
  - [Sensores inerciales](#sensores-inerciales)
  - [Sensores MEMS](#sensores-mems)
    - [Accelerometro](#accelerometro)
  - [Magnetómetro (Sensor de campo magnético)](#magnetmetro-sensor-de-campo-magntico)
  - [Giroscopio](#giroscopio)
  - [Conclusión](#conclusión)
- [Rotaciones: Orientación Relativa y Absoluta](#rotaciones-orientación-relativa-y-absoluta)
  - [Rotaciones 3D](#rotaciones-3d)
  - [Rotaciones relativas](#rotaciones-relativas)
  - [Rotaciones absolutas](#rotaciones-absolutas)
- [Redes Celulares (4G / LTE, 2G y 3G)](#redes-celulares-4g--lte-2g-y-3g)
  - [Acceso múltiple](#acceso-mltiple)
    - [TDMA Acceso Múltiple por Divisón de Tiempo](#tdma-acceso-mltiple-por-división-de-tiempo)
    - [FDMA División de Frecuencia](#fdma-división-de-frecuencia)
    - [CDMA Code Division Multipe Access](#cdma-code-division-multipe-access)
    - [4G (LTE)](#4g-lte)
- [Mobile Packet Core](#mobile-packet-core)

- [Wireless Communication](#wireless-communication)
  - [Introducción](#introducción)
- [Transmisión a distancia mediante radio](#transmisión-a-distancia-mediante-radio)
  - [Las Señales](#las-señales)
  - [Atenuación](#atenuación)
  - [Atenuación](#atenuación)
  - [Ruido](#ruido)
  - [Modulación multinivel](#modulación-multinivel)
  - [Códigos de corrección de errores](#cdigos-de-corrección-de-errores)
  - [Capacidad del canal](#capacidad-del-canal)
- [OFDM y MIMO](#ofdm-y-mimo)
  - [Modulación Multiportadora](#modulación-multiportadora)
  - [OFDM (Overlapping Channels)](#ofdm-overlapping-channels)
  - [MIMO](#mimo)

## Wireless Communication

### Introducción
Las redes wireless (celulares, wifi, ble) se basan en la transmisión por rádio.

![](https://i.imgur.com/Q1hmsNk.png)

A la izquierda del sistema hay un dispositivo que quiere transmitir `1001` que puede corresponder a cualquier tipo de datos. Hay bits de info y de codificación usados para luchar contra los errores en la Tx.

Los códigos se usan para evitar que información incorrecta sea transmitida a las aplicaciones superiores. Los códigos de corrección se usan para evitar errores en la Tx. Se usan para corregir los errores o para detectarlos y pedir una retransmisión de la información.

Los bits se expresan en forma de onda. Estos son uns símbolos con una frecuencia portadora añadida. Estas portadoras son fundamentales porque si la información no fuera modulada a una cierta frecuencia no podria ser transmitida.

Esta información debe ser amplificada, por eso hay un amplificador de potencia (cuadrado con triangulo dentro). La salida del amplificador se envía a una antena (cono naranja). Esta antena transmite ondas electromagnéticas que serán captadas en la antena receptora (cono naranja derecho). La señal de entrada tiene un nivel de potencia adecuado para la electronica pero si queremos que la señal sea recibida correctamente en el receptor incluso con atenuación debemos amplificarla.

La señal recibida es _extremadamente débil_ y es tan débil que se puede comparar con el ruido térmico. Normalmente ese ruido no se debe tener en cuenta en el emisor. Pero en el receptor la señal es comparable al ruido e interferencias. Al recibir la señal se mezcla. En el receptor tenemos un amplificador de bajo ruido que amplifica y filtra la señal. No solo se amplifica la señal recibida, tambien se amplifica el ruido y al final tenemos una señal con ruido mezclado. La señal de salida tiene una potencia suficientemente fuerte para trabajarla pero tiene mucho ruido. 

La caja del final del cirucuito es la que debe interpretar la señal en bits; puede haber errores debido al ruido e interferencias. Los sitemas de detección y corrección de errores solucionan esto.

## Transmisión a distancia mediante radio

Si tenemos un circuito electronico dónde pasa corriente constante, que son cárgas electricas en movimiento, genera un campo eléctrio y un campo magnético en el circuito (electromagnético). Si la corriente es variable en el tiempo, esto provoca que el campo electromagnetico dela vecindad del circuito tambien sea variable.

Si poenmos un circuito receptor muy próximo del transmisor, el tx tambien induce una corriente vairable en el receptor (circuitos extremadamente próximos). La corriente en el primer (receptor) circuito se ve alterada por la existencia del segundo circuito (tx). Hay una interacción. Detectando estas variaciones se pueden comunicar los circuitos (Near Field Communication).

Lo normal es que las antenas esten muy lejos. En este caso la comunicación se produce por ondas electromagnéticas. El segundo cirucito está en un campo lejano (Far Field). La corriente variable en el 1r circuito provoca un campo electromagnético variable que se porpaga a través de ondas electromagnéticas que provocan un campo electromagnético variable en el segundo circuito dónde provoca una corriente eléctrica varibale también a distancia.

Las ondas electromagnéticas son dificiles de visualizar, suceden en el espacio y en el tiempo.

![](https://i.imgur.com/ZZeGzNi.png)

Azul: campo eléctrico \ Rojo: Campo electromagnético

![https://i.imgur.com/ZdM1grV.png](https://i.imgur.com/ZdM1grV.png)

La diferencia entre picos positivos y negativos es la longitud de onda. La diferencia entre picos en tiempo es el Periodo (s). La inversa del Periodo es Frecuencia (Hz).

Muchas veces la frecuencia se expresa en rad/s, una multiplicación por 2pi. F -> Hz // Omega -> rad/s. La conversión es `F*2pi` o `Omega/2pi`.

Además tambien tenemos la velocidad de propagación de la onda. Des del momento que se produce la perturbación en la antena Tx cuanto tarda en llegar la señal. La velocidad en el vacio es `c` (velocidad luz). _300.000km/s == 3*10⁸ m/s_. Factor de conversión entre _longitud de onda_ y _velocidad de Tx_ es `Velocidad Tx / Freq`.

Las señales que enviamos por las antenas de radio son pulsos:

![](https://i.imgur.com/D9kJXmp.png)

Las antenas la cantidad de energia de onda que transmiten es dependiente de la frecuencia. Debemos tener un pulso multiplicado por una señal oscilatoria de tipo seno y coseno y su frecuencia la llamamos **frecuencia portadora**. Los 1 y 0 se transmiten como símbolos a través de una multiplicación de la señal portadora. Los símbolos, por ejemplo en WiFi, no son de 4GHz esa es la señal portadora:

![](https://i.imgur.com/paWzDVz.png)

### Las Señales

![](https://i.imgur.com/dp8oUhd.png)

La señal verde es un pulso rectangular, multiplicado por una señal oscilando a una cierta frecuencia (**la portadora**).

Arriba hay una señal oscilatoria con la fórmula dónde `alpha` es la amplitud, `ω` es la frecuencia y `ϕ` es la fase. La frecuencia en este caso expresada en `rad/s`.

La **fase** nos dice cómo empieza la señal. Por ejemplo:

![](https://i.imgur.com/i7Wpp7l.png)

- Si la señal es `cos` y la fase es `0` tenemos el caso **1**.
- Si la señal es `cos` y la fase es `π radianes` es el caso **2**.
- Si la señal es `cos` y la fase es `π/2` es el caso **3**.

El coseno es la proyección sobre el eje X. Debemos imaginar una flecha que empieza a girar apuntando hacia el valor de entrada `x`.

En este caso la flecha empieza apuntando hacia el eje `x` positivo. El coseno en el **tiempo 0** vale 1. A medida que va avanzando su valor va disminuyendo hasta llegar a `0`.

En el segundo caso, empezamos con un valor negativo de `-1`. Este caso la flecha empezaria apuntando hacia el eje `x` negativo.

En el tercer caso, empezamos con un valor de `0` y immediatamente después empieza a ser negativo. Este caso la flecha empieza apuntando hacia las `y` positivas. Esto es `π/2 rad`. En este caso puede haber la duda de si la flecha apunta hacia arriba o hacia abajo, pero cuando empieza a girar, su valor se va haciendo negativo por lo que está hacia arriba.

![](https://i.imgur.com/vPIShdf.png)

### Atenuación

La señal cuando viaja tambien tiene un cambio en la fase a causa del tiempo de viaje. La fase es sumar dentro del argumento del coseno.

La amplitud es una multiplicación y la fase se le debe sumar `phi`.

La señal inicial puede ser expresada como un número complejo:

`s(t) = cos(ω\*t) + i sin(ω\*t) = e^(iωt)` dónde `w` és `omega`.

Y la señal en el receptor también:

`s(t) = a*cos(w\*t+ϕ) + i a*sin(ω\*t+ϕ) = e^i(ωt+ϕ)` dónde `w` és `omega` y `a` es `alpha`.

![](https://i.imgur.com/fji7kmv.png)

Usando esta notación podemos reprencentar la atenuación y cambio de fase multiplicando la señal por un número complejo: Cambio de amplitud (multiplicar un alpha por la atenuación) y introducir un desfase (e^(i*phi)):

**h = a * e^(i*ϕ)** dónde `h` es el Channel Effect.

**r(t) = s(t)*h = e^(iωt) * a * e^(i * ϕ) = a * e^i(ωt+ϕ)**

![](https://i.imgur.com/rkXoomW.png)

Ejemplo: Si nuestro portatil se encuentra a 3 metros del access point, el tiempo de trayecto es `t=d/v = 3 / 3x10^8 = 10*10⁻⁹ = 10ms`. 

Entonces si la frecuencia en WiFi es `ω = 2π * 2.4 G rad/s` esto significa que si ahora multiplicamos por la fase `ϕ = - 2π * 2.4 * 10 = -150 rad`.

Si este resultado lo dividimos entre `2π` obtenemos las vueltas que ha dado: `23.87`, si hacemos `ϕ = 0.87*2π = -0.69 rad = ϕ`. Por lo que el desfase (ϕ) es `0.69 rad`.

### Atenuación

Diferencia entre la potencia transmitida vs la potencia recibida.

Logaritmos en base 10 contan ceros.

- log(10, 1000) = 3
- log(10, 10) = 1
- log(10, 5) = log(10, (10/2)) = log(10, 10) - log(10, 2) = 1 - 0.3010 = 0.6989

Cuando tenemos un número y queremos expresarlo en dB debemos calcular `x dB = 10·log(10, x)`. Los dB son usados para expresar números muy grandes o pequeños:

- 100000 = 10·log(10, 100000)= 10·5 = 50dB
- 0.00001 = 10·log(10, 0.00001) = -5·10 = -50dB

Los logaritmos los usamos para evaluar atenuaciones. `Ptx/Prx` como no tiene unidades podemos expresarlo en dB: `10·log(Ptx/Prx)`.

En muchos casos podemos usar dBm, es el dB respecto 1mW:

- `10·log(P/1 mW)` (dBm)

Eg:

- P = 100mW = 10·log(100/1) = 20dBm
- P = 10nW = 10·log(0.00001mW/1) = -50dBm
- Loss (dB) = `Ptx (dBm) - Prx (dBm)` = 20 - (-50) = 70dB

Factores que influyen en la atenuación de un enlace rádio. Nos fijamos en el caso en el espacio libre (naves espaciales). Hay una fórmula que nos permite predecir la atenuación y ver los factores que influyen en esta:

`Pt = Pt·Gt·Gr(gamma/4·π·d)²`

4πd² = Área de una esfera. La propagacion de las ondas en el espacio tienen forma de esfera.

- Ganancias de las antenas.
- Longitud de onda o frecuencia de la portadora.
- Distancia.

Al crecer y distribuirse con un factor de `d²` (radio al cuadrado) es de esperar que la potencia se atenue en un factor de `d²` con la distancia.

En los sistemas que usamos nosotros no se produce la misma atenuación que en el espacio libre. En la transmisión en tierra es:

![](https://i.imgur.com/F3UVM5l.png)

En tierra la atenuación va a ser (normalmente) mucho más grande que en el espacio libre. El factor de crecimiento (exponente) de la distancia suele ser mayor que 2 en tierra. Normalmente usaremos `a=4`.

Un factor que **afecta la atenuación** es la dirección de las **antenas**. Las antenas se diseñan con direcciones privilegiadas. Normalmente son direccionales. **Fuera de la dirección privilegiada la atenuación es mucho mayor.**

![](https://i.imgur.com/IKjOFE6.png)

La distancia, la frecuencia y la ganancia de las antenas son muy imporantes en el espacio libre. Pero en la tierra hay muchos otros factores que van a afectar:

- Reflexión, Difracción, Efecto Doppler y Scattering o Dispersión.

#### Reflexión
Cuando una onda choca contra un muro o algún obstáculo, una parte de la onda sale reflejada. Debemos tener en cuenta el tamaño relativo de los objetos con los que choca la onda respecto la longitud de onda.

Si el objeto es muy pequeño respecto la longitud de onda para la antena es como si no existiese el objeto.

Si el objeto es muy grande, la onda se comporta como la luz.

#### Difracción

Cuando hablamos de difracción debemos tener en cuenta el tamaño relativo de los objetos o ranuras por dónde pasará la onda con respecto la longitud de onda:

![](https://i.imgur.com/irBohEV.png)

La longitud de onda seria la distancia entre las líneas azules. En (de izquierda arriba a derecha abajo) el primer caso la ranura tiene un tamaño que es de un poco más del doble que la longitud de onda la señal atravesará la ranura prácticamente en línea recta.

Si la ranura es mucho más pequeña (segundo caso) vemos que la señal las ondas se salen del trayecto en línea recta que marcaría la ranura.

El tercer caso la ranura es igual que en el primer caso, pero esta vez la longitud de onda es mayor. Por este motivo el comportamiento es distinto porque la relación relativa entre las dos provoca que la onda se salga del trayecto en línea recta.

Por esto lo importante no es la longitud de onda, sino el tamaño de esta respecto al osbtaculo.

En los dos casos de abajo no son ranuras sino obstáculos. Si tenemos una longitud de onda grande va a tener mayor difracción, en cambio cuanto más pequeña es la longitud de onda más se va a comportar como la luz.

Las ondas también pueden atravesar paredes, ventanas o osbtáculos. Cuando pasa esto la atenuación es muy grande. A mayor frecuencia mayor es la atenuación. Para frecuencias más bajas las ondas de rádio es más probable que la atenuación tenga menos efecto porque ya hemos visto que a causa de la difracción que sufren pueden propagarse **no en línea recta** sino que puede recibirse en posiciones que no estan en línea recta y puede atravesar más facilmente los obstaculos.

La atenuación depende de la distancia con un factor `a=4`, este es un valor médio que puede variar segun los escenarios.

La frecuencia, debido a que cuando aumenta la frecuencia aumenta la atenuación en función a la distancia (Formula de Frizz tenemos el inverso de la frecuencia en el factor que determina la atenuación). Pero también hay frecuencias que hay picos de absorción debido a los gases y partículas que componen el aire (Oxígeno, Agua...).

#### Zona de Fresnel

Si tenemos dos antenas y hay obstáculos entre medio se puede identificar unas zonas (Zonas de Fresnel) dónde si no hay obstáculos la transmisión es relativamente buena. En cambio si la zona se ve ostaculizada la atenuación es mucho más grande. Son zonas que marcan un rádio respecto la línea de transmisión que no es uniforme, es una especie de elipsódie que aumenta cuanto más cerca de las antenas y disminuye cuando se aleja. Al centro el rádio es máximo. Además también nos dice la importancia de los obstáculos según si ocupan o no la zona de fresnel.

![](https://i.imgur.com/fQOnnpi.png)

#### Scattering

Cuando una onda choca con un objeto que tiene muchas aristas y la onda sale reflejada en todas las direcciones.

---

**La atenuación se incrementa en un factor de d² en el espacio libre. Cuando estamos en un entorno urbano, la atenuación en algunos casos puede ser menos o más acusada en relación a la distancia. En general suele ser un factor mayor de 2**. 

---

#### Multipath Fading

En cada punto del espacio la atenuación puede fluctuar. La atenuación multitrayecto aparece debido a que la señal no sigue un único camino en su trayectoria debido a los osbtáculos y distintos fenómenos. La señal recibida es la superposición de distintos frentes de onda:

![](https://i.imgur.com/8HUMT9w.png)

En la imágen vemos que hay una señal que corresponde al camino directo pero también puede corresponder a la señal que choca contra la pared. Así que la señal recibida es la superposición de las dos en este caso. Se recibe la señal con distintas fases superpuestas debido a que llegan en tiempos distintos.

![https://i.imgur.com/UGLT0hR.png](https://i.imgur.com/UGLT0hR.png)

Las ondas pueden tener distintas amplitudes y fases, pero la frecuencia siempre es la misma.

##### Qué sucede cuando sumamos señales con distintas fases?

Si sumamos en fase, la resultante tendra la misma frecuencia y fase y el doble de amplitud.

Si sumamos en contrafase son interferencias destructivas; en caso de estar totalmente en contrafase se cancelan..

![](https://i.imgur.com/0H74EMw.png)

---

En un caso real, podemos tener distintos casos para distintos receptores en lugares espaciales distintos. Por este motivo una antena puede tener mejor recepción que otra según su localización. Hay zonas espaciales dónde puede presentar picos y otros mínimos.

![](https://i.imgur.com/iTvlydG.png)

![](https://i.imgur.com/W6Gc650.png)

En el heatmap se puede apreciar un patrón y estructura. Normalmente, de forma estadística, la diferencia entre un valor máximo y un mínimo suele estar en media longitud de onda. Por ese motivo algunos AP tienen dos antenas separadas media longitud de onda aproximadamente para intentar solucionar un poco el problema.

> La atenuación multitrayecto es impredecible. Los objetos se pueden mover (hojas, etc) y hay muchos factores impredecibles.

A causa de esto la tasa de pérdida de paquetes puede variar mucho de un punto a otro.

![](https://i.imgur.com/G7WJEIy.png)

En esta imagen se ve un experimento dónde han movido un AP por una habitación y se puede ver el Throughput y el packet-loss ratio variando.

El multipath fading está causado por la diferencia de tiempo entre el trayecto principal y los trayectos secundarios de rebotes. Por eso el espacio (escenario) por dónde se propaga puede hacer que haya tiempos de delay sean mayores o menores (indoor vs outdoor).

Eg: 

Escenario dónde la distancia en un rebote es de 3m. La diferencia es: `3 / 3*10⁸` = `10⁻⁸` = 20ns de delay. `d/c`.

Si suponemos que estamos con WiFi (la onda oscila a una frecuencia de 2.4GHz). El período  `T = 1/2.4*10^-9 = 1/2.4 = 0.41ns` es el tiempo que transcurre entre dos ciclos.

El tiempo entre el primer rayo y el segundo rayo es `20ns`, y la distancia entre dos ciclos es `0.41666ns`. Entonces si dividimos `20/0.41` obtenemos la cantidad de ciclos que han habido en esos 20ns. Son `48 ciclos`. Por lo que podemos saber que, al no contener ningún residuo (decimales), la señal estará en fase con la señal principal después del trayecto de 20ns pero con una intensidad más pequeña.

Que una interferencia sea constructiva o destructiva depende de la frecuencia:

![](https://i.imgur.com/WxOxTv4.png)

Diferentes portadoras pueden par lugar a interferencias constructivas o destructivas en el mismo punto del espacio.

La interferencia puede ser destructiva o constructiva dependiendo de la frecuencia de la señal. Para un mismo camino el tiempo es el mismo, pero al tener frecuencias distintas el numero de ciclos es distinto y puede suceder que para una cierta frecuencia el numero de ciclos para la señal directa y la reflejada se sumen de forma destructiva o constructiva.

### Ruido

Pn = N0 * Bw dónde B0 es la densidad de potencia de ruido y Bw es el ancho de banda.

### Modulación multinivel

-

### Códigos de corrección de errores

Si usamos 3 bits y tenemos 8 posibilidades podemos elegir 4 códigos invalidos, de este modo podemos detectar 4 tipos de errores:

![](https://i.imgur.com/9lWg62n.png)

De este modo podemos **detectar** errores pero no corregirlos.

Si usamos 4 bits y por lo tanto ahora tenemos 16 posibilidades, y elegimos solo 4 como correctas:

![](https://i.imgur.com/MdJ6bDI.png)

Ahora el error de 1 solo bit se puede corregir. Si transmitimos `0000` y recibimos `0100` sabemos que hay un error. Pero en este caso no podemos corregir tampoco el error ya que puede ser el caso de `0000` y el error esta en el segundo bit o `0101` y que el error está en el segundo bit. Añadiendo dos bits de redundancia aún no somos capaces de corregir errores.

Hay cógidos que si permiten la corrección de errores. Uno de los más sencillos son los códigos de Hamming. Tenemos `4`bits de transmisión y se añaden 3 bits de redundancia. Existen unas ecuaciones llamadas parity checks:

![](https://i.imgur.com/Ad7BCOv.png)

Podemos elaborar el diagrama de venn, colocar C1, C2, C3 y C4 y encontrar C5, C6 y C7 asegurando que hay un número impar de 1 en cada círculo.

![](https://i.imgur.com/eYSorzZ.png)
`
### Capacidad del canal

Si tenemos un sistema de comunicaciones con un cierto SNR y un cierto ancho de banda, como podemos aumentar la velocidad de Tx sin aumentar la potencia ni el ancho de banda?

- Modulación multinivel - Podemos permitir más bits por el canal; podemos transmitir más información. Contra: Si aumentamos el numero de bits pot símbolo aumentamos la tasa de errores. Aumentamos R/Bw pero necessitamos una mejor SNR.

- Podemos añadir bits de redundancia pero al añadirlos necesitaremos más símbolos para transmitir los mismos bits de información (R; bits sin incluir los bits de código) disminuyendo la R/Bw aunque con el mismo SNR bajamos la tasa de error.

**Relación fundamental de Shannon (Formula capacidad del canal de Shannon):**

Un canal con ruido aditivo blanco gausiano y sin multipath fading la fórmula de shannon nos dice:

![](https://i.imgur.com/ckYjUFM.png)

La Capacidad es la máxima tasa de transmisión de información que podemos tener con una tasa de error relativamente baja.

![https://i.imgur.com/S903hwm.png](https://i.imgur.com/S903hwm.png)

![](https://i.imgur.com/hsZn9rK.png)

![](https://i.imgur.com/tMX6Aw2.png)

La fórmula de Shannon nos dice que en la zona marcada (prohibida) no podemos establecer un sistema de comunicaciones. El sistema de comunicaciones debe quedar por la zona marcada debajo de la curva.

Cuando tenemos un sistema de Tx y calculamos la Eb/No y la eficiencia espectral y lo marcamos en el gráfico (punto verde) este nos debe caer bajo la zona de la curva para que el sistema de transmisión pueda funcionar correctamente en teoria. Es un límite teórico.

Suponemos que estamos transmitiendo en Wifi a R = 20Mbps. El ancho de banda de WiFi es Bw = 20MHz. Con estos datos la Eficiencia Espectral sería de 1:

![https://i.imgur.com/S903hwm.png](https://i.imgur.com/S903hwm.png)

(2¹ - 1) / 1 <= Eb/No

Como muy poco Eb/No debe valer 1. Si lo marcamos en el gráfico x,y = (1, 1).

#### Pregunta típica de exámen
Suponemos que Eb/No vale 10 en el comedor de nuestra casa; x,y = (10, 1). Nuestra eficiencia espectral con Wifi a 20Mbps sigue siendo 1. Si me alejo del AP y me voy a una habitación que se encuentra al otro extremo de mi piso que pasará con el Eb (Energia/bit recibida)? Se mantiene, aumenta o disminuye?

**R:** Disminuye. Recordemos que Eb es la potencia recibida (energia por bit) dividida entre la R (tasa de bits de información por segundo). Por lo tanto si me alejo la potencia recibida disminuye (ya que la potencia depende mucho de la distancia, recordemos la atenuación). La R no se modifica y por lo tanto la Eb disminuye. Como No es una constante, si me alejo del AP nos acercamos a la zona dónde el sistema puede funcionar incorrectamente. Si en vez de alejarme hubiera disminuido la potencia de transmisión (Ptx) el efecto es el mismo.

![](https://i.imgur.com/cfdRVTF.png`)

![](https://i.imgur.com/HeQ8Dfp.png)

Tradeoff fundamental. Los sistemas que utilizan una potencia baja la distancia a la que puedes transmitir los bits es tambien baja. Los sistemas de baja potencia tienen alcances cortos. La distancia y la potencia de transmisión están inversamente relacionadas.

 - Si modificamos el Ancho de banda nos movemos en vertical.
 - Si modificamos la R nos movemos en diagonal.
 - Si modificamos la distancia o la potencia de transmision nos movemos en horizontal.
 
No podemos tener:

- Una R muy grande 
- Una distancia muy grande
- Una Ptx pequeña
- Bw pequeño

Aunque este seria el sistema ideal, pues transmites mucha informacion a gran distancia, con poca potencia y poco ancho de banda, no puede existir.

Podemos tener:

- Baja potencia (Bluetooth, NFC...)
	+ Vt es baja
	+ Distancia es baja

- Alta velocidad (WiFi)
	+ Distancia corta
	+ Potencia alta
	
- Gran alcance (Celulares)
	+ Vt baja
	+ Potencia alta
	
## OFDM y MIMO

Permitió que los sistemas inalambricos dieran un salto en capacidad, rompiendo los límites de la curva de Shannon.

Todos los sistemas actuales usan estas técnicas en redes de todos los tipos.

PROBLEMA: Si en un sistema utilizamos más ancho de banda disminuimos la eficiencia espectral (la bajamos). Si doblamos el ancho de banda debemos doblar la R para mantener la misma eficiencia espectral. `Efic Espectral = Bw/R`. Si queremos usar R más grandes sin variar la eficiencia espectral debemos usar más ancho de banda.

4G ha aumentado el ancho de banda respecto 2G o 3G. En .11n podemos usar canales de 40MHz en vez de 20MHz.

Aumentar el ancho de banda significa buscar rangos dónde el ancho de banda este disponible (normalmente en altas frecuencias), pero vamos a tener menos rango.

#### Delay spread

Es la diferencia entre el camino que tiene el tiempod e camino mínimo y el que tiene un tiempo de camino máximo con una amplitud todavía significativa. 

En una habitación la diferencia del retardo son unos pocos metros. Si por ejemplo la diferencia es de 3m, si calculamos el tiempo `t=d/c` tenemos que son `10ns`.

Pero si vamos a un escenario outdoor las diferencias de distancia aumentaran y con ellas los tiepos de __delay spread_ siendo del orden de `ms`.

Si estamos en un ancho de banda pequeño (2MHz) y tengo un tiempo de símbolo (inverso del Bw) de `500ns`. Si tenemos una distancia entre los caminos de 30m y por lo tanto un delay spread de `100ns`. Van llegando los rayos y el último llega en `100ns`. Durante los primeros `100ns` van llegando símbolos (distintos) y se van interfiriendo (tiempos i fases distintos) (constructivos y destructivos) y hacen fluctuar la amplitud. Al cabo de 100ns ya no llegan estos símbolos antiguos (con retraso) y se estabiliza la amplitud. Al cabo de un rato vuelve a haber fluctuaciones porque acaban unos símbolos y van llegando otros nuevos símbolos.

Lo importante es que durante un periodo central (`400ns`) la amplitud es constante. 

Una vez acaba la transmision de este símbolo el último rayo que venia con `100ns` de retraso aún le quedan `100ns` para acabar, por lo que se va a interferir con el próximo símbolo ya que esta llegando cuando el siguiente símbolo esta llegando por primera vez.

![](https://i.imgur.com/S0VIxMo.png)

Los `100ns` primeros (el tiempo del camino más largo) de todos estos símbolos van a ser inservibles. Pero aún tendré `400ns` en este caso para detectar el símbolo.

Si usamos un Bw mayor tenemos un tiempo de símbolo de `50ns` (menor). Si el delay spread es de `100ns` este mismo símbolo esta volando por otros trayectos más lentos y va a llegar en el futuro. Por lo que el símbolo va a llegar de lleno cuando esté transmitiendo el símbolo siguiente. Habrá una interferencia entre símbolos muy grande. En casos de delays muy grandes puede interferir con símbolos muy futuros.

Solución?

### Modulación Multiportadora

Idea: En vez de transmitir muchos bits/s muy cortos, agrupamos los símbolos en tiempos mayores. Dividimos, por ejemplo, el canal de 20MHz en 20 canales de 2MHz y por cada canal transmitimos un símbolo con un un Ts de `500ns`. Como cada símbolo viaja a distinta frecuencia no se interfieren entre ellos y los podemos extraer. No hay el problema del delay spread.

### OFDM (Overlapping Channels)

Consiste en coger las señales y transmitirlas lo más empaquetadas posibles (empaquetamiento óptimo). Se hace la modulación multiportadora óptima. Transmitimos muchos símbolos en portadoras distintas de forma que cada símbolo tiene un ancho de banda más pequeño (más duración) pero como se transmiten simultaneamente el trhoughput equivale a haber transmitido muchos símbolos más cortos con una sola frecuencia portadora.

.11a usa OFDM. Si no fuera por OFDM al tener bits muy estrechos tendria problemas con el delay spread.

#### 802.11a @54Mbps (3/4 64QAM)

El canal de 20MHz se parte en 64 subportadoras; cada subportadora tendria un Bw teórico de 20/64. De estas 64 subportadoras se utilizan 48 para enviar datos.

Algunas se usan para enviar tonos constantes para hacer estimaciones de la atenuación.

Si utilizamos un coding rate de 3/4 significa que enviamos 3 bits de información por cada 4 bits transmitidos. 

Si utilizamos 64QAM transmitimos 6 bits (2⁶ = 64)de información o no por cada símbolo.

El tiempo de símbolo de cada subportadora es de 4us; un poco por encima del tiempo teórico que esperariamos (el inverso del Bw).

R = 48 subportadoras * 1 símbolo de subportadora / 4usecs * 6 bits/subportadora  * 3/4 bit info/bits totales = 54Mbps.

Tenemos 48 subportadoras cada una lleva 1/4usec símbolos por segundo, cada símbolo de cada subportadora lleva 6 bits de los cuales hay 3 bits de información por cada 4 bits transmitidos.

### Diversidad

Es la técnica principal usada en los sistemas wireless para solucionar el problema de los canales inalámbricos variables (multipath fading).

Esta técnica consiste en usar transmisiones redundantes de modo que la probabilidad de que una gran atenuación en alguno de los canales no va a causar una comunicación erronea.

Una forma de tener diversidad es usar un sistema de transmisión que para una portadora tiene una interferencia destructiva, si cambiamos la frecuencia portadora es muy posible que para esta nueva no sea destructiva.

OFDM se puede utilizar como técnica de diversidad empleando esta propiedad para luchar contra la atenuación.

Otra forma de conseguir diversidad es usar varias antenas en la transmisión y/o en la recepción. Al transmitir desde distintos lugares provoca que no haya tanta posibilidad de que en todas coincida una interferencia destructiva.

Al coger el canal de 20MHz en OFDM y partirlo en 64 subcanales lo que haremos es transmitir los bits por los canales dónde la interferencia es constructiva y evitar los canales dónde las interferencias son destructivas. Como podemos saber como son las interferencias? De los 64 subcanales solo usamos 48, estos otros canales se envian señales de amplitud conocida para detectar las atenuaciones e interferencias y centrar la transmisión en los mejores canales. De esta forma puedes tener diversidad al usar frecuencias portadoras distintas.

A causa de esto la tasa de transmisión no es constante.

### MIMO

Usar múltiples antenas en el transmisor y el receptor. Se utiliza para tener una mejor ganancia de diversidad. Como hay mucha más divercidad es mucho más probable que no haya atenuación.

También se puede tener una ganancia de multiplexación y, al igual que com OFDM, romper con los límites de Shannon. Utiliza la atenuación multitrayecto en su favor para tener más símbolos por segundo.

![](https://i.imgur.com/5bMfGoN.png)

Usando esto de aquí, podemos transmitir símbolos a la vez y en la misma banda de frecuencia y recuperar estos símbolos por separado aumentando la capacidad del canal. Usando MIMO podemos transmitir al doble de la velocidad. Si tenemos `n` antenas en el receptor o `n` antenas en el transmisor (1xN // Nx1) estamos multiplicando por un factor de `n` la relación SNR. 

Si usamos mimo mejoramos nuestra SNR en un factor `n²` (NxN).

Solo a costa de tener una electronica más complicada y sin aumentar el ancho de banda o la potencia aumentamos la capacidad del canal, por lo que compensa tener más antenas.

MIMO se puede usar para ganar diversidad (menor sensibilidad al multipath fading) o para la multiplexación (mejor SNR y una eficiencia espectral mayor). Pero hay un tradeoff entre las dos.


## Bluetooth Low Energy (BLE)

Bluetooth SIG es quien desarrolla la tecnologia bluetooth. En 2010 se introdujo la version 4.0 que es la que veremos.

El nivel físico de bluetooth consiste en transmision en la banda ISM. Hay 40 canales de 2MHz (3 canales para advertising y 37 para transmision de paquetes de datos).

R = 125Kbps, 1Mbps son las velocidadas de transmisión, aunque el throughput es menor.

La potencia máxima es 10mW o 100mW en BT5

La distancia máxima teorica es de 100m aunque en realidad es mucho menos.

Un beacon puede funcionar muchos meses con una pequeña batería.

En Bluetooth se usa un stack distinto al de TCP/IP.

![](https://i.imgur.com/TShkwLY.png)

### GAP

En bluetooth hay dos fases. La primera estamos en advertising, descubrimos los dispositivos bluetooth. Esta primera fase se gobierna por GAP (Generic Access Profile). El GAP define como se controla el descubrimiento y la conexión entre dos dispositivos.

En GAP hay dos roles: periféricos (dispositivos con pocos recursos) y centrales (un smartphone).

Durante la fase de descubrimiento hay un intercambio de paquetes pequeños de 31bytes y tambien otros tipos de paquetes relativos a los escaneos (Scan Response) del mismo tamaño. Estos paquetes se envian en 3 canales específicos; los dispositivos envian estos paquetes por esos canales en un cierto intervalo (advertising interval). El escáner escucha en estos canales durante un tiempo (scan window) durante un cierto tiempo (scan interval).

Los paquetes de advertiser pueden ser de 4 tipos:

- **ADV_IND** Advertising Indications, indica que esta preparado para conectarse con cualquier dispositvo central.
- **ADV_DIRECT_IND** El periferico pide una conexión con un dispositivo central específico.
- **ADV_NONCONN_IND** Dispositivos NO conectables, solo mandan algun tipo de informacion a los dispositivos que escuchan.
- **ADV_SCAN_IND** Es similar al anterior, pero tiene la opción de mandar información adicional. Los dispositivos envian un scan pero estan dispuestos a mandar más info si se los requiere.

Los paquetes de esta fase tienen un tamaño máximo de 31 bytes y el payload lleva 1 o más "AD structures": length, type y data.

Los dispositivos bluetooth en la fase de advertising pueden indicar varias cosas: Su nombre, el servicio que dan (a través de UUIDs estandarizados...).

### GATT

Es el que gobierna la transferencia de datos bidireccional de dos dispositivos que ya han pasado por la fase GAP. Hace uso de un protocolo genérico llamado ATT (Attribute Protocol) el cual se usa para guardar información (atributos) en una pequeña base de datos simple en el dispositivo servidor usando IDs de 16bits para cada entrada de la tabla.

El formato estandar de estos atributos son:

- Id único del atributo (16b)
- Identificador del tipo de atributo (UUID)
- Valor
- Permisos del atributo (Read/Write/Security)

Los dispositivos tienen una función predeterminada. Se definen perfiles que son una colección de servicios predefinidos por Bluetooth SIG. GAP y GATT son perfiles genéricos soportdos en todos los dispositivos BLE. Puede haver, por ejemplo, un dispositivo como perfil _Heart Rate_ que combina el _Heart Rate Service_ y  el _Device Information Service_. Este perfil se compone de 2 servicios.

Un dispositivo puede contener distintos perfiles. Existen muchos perfiles distintos (Presion sanguínea, Cycling Speed, Heart Rate...)

Los servicios definen una serie de datos asociados al servicio, estos datos se llaman caracteristicas. Un servicio suele tener distintas caracteristicas (una o más). Los servicios se caracterizan por una UUID (16b cuando son estandares) o 128b cuando son creados por el usuario.

En GATT se establecen dos roles: el servidor y el cliente. El server recibe comandos y peticiones GATT y devuelve respuestas hacia el cliente.

## Sensores IMU

Con la creación del primer iPhone se añadieron varios sensores para distintos casos. Actualmente los sensores son altamente usados por todos los fabricantes y sistemas operativos.

### Sensores inerciales

Los sensores inerciales tienen que ver con la posición y movimiento de un dispositivo. Cuando un sensor manda información siempre lo hace en referencia al sistema de coordenadas concreto. El vertical del móvil Android (abajo arriba) es el eje `y`, en horizontal (derecha izquierda) es el eje `x` y saliendo de la pantalla del móvil es el eje `z`.

Los movimientos respecto al eje son: pitch (`x`), roll (`y`) y Yaw (`z`). Para el símbolo se usa siempre la regla de la mano derecha (pulgar apunta eje, dedos nos dan el positivo).

En Realidad Aumentada nos orientamos respecto al eje global de la tierra (sistema de coordenadas de la tierra). Es importante saber si apunto al norte, este, etc. Lo que apunta hacia el norte magnético es el eje `y`, hacia el este el `x` y en la vertical de la tierra el `z`.

### Sensores MEMS

Combinan componentes electrónicos y mecánicos. Permiten crear sensores muy pequeños, consumos muy bajos y costes muy baratos.

![](https://i.imgur.com/aDU3mbi.png)

Por ejemplo un acelerometro; tenemos un material con una cierta masa fijada en unos ejes ciertamente elásticos que permiten movimiento. Una parte del dispositivo se desplaza y al moverse las placas se mueven respecto las otras se puede medir el desplazamiento y calcular la fuerza.

#### Accelerometro

Mide la fuerza que actua en el smartphone y la masa inercial. Se puede construir con un muelle microscópico y una bolita microscópica por cada eje. Entonces el acelerometro traduce este movimiento a una fuerza que puede ser medida. La lectura del acelerometro en un dispositivo en reposo encima de una mesa con la pantalla hacia arriba seria `x,y,z = 0,0,-9.8` ya que el eje z esta sufriendo la fuerza de la gravedad hacia abajo.

La principal complicación del uso del acelerometro es que mide la aceleración de la gravedad (vertical) y la aceleración lineal del dispositivo y se molestan entre ellas. Ambas son indistingibles, el acelerometro siempre suma las dos. El problema del acelerómetro es cómo separar las dos señales.

Para separarlas podemos filtrar las señales con un filtro paso-alto. La gravedad es una señal paso-bajo, ya que fluctua de forma más lenta. ESto no es suficiente si lo queremos hacer realmente bien, así que deberemos incluir las mediciones de otros sensores para complementarlo.

El acelerometro no nos dice ni la posición ni la velocidad. Pero Pero la velocidad es la integral de la posición y la velocidad es la integral de la posición. Por eso, podemos saber cual es la posición de un móbil si sabemos su posicion incial y su velocidad inicial. Usando el acelerómetro podemos saber la posición de una persona. Esto es teórico, pero al no poder eliminar la gravedad completamente, tenemos un sesgo que nos produce un error. Al hacer integrales el error se acomula creciendo de forma parabólica hasta ser significante.

### Magnetómetro (Sensor de campo magnético)

Es una pequeña brújula que nos indica la dirección del campo magnético de la tierra. El campo magnético no apunta hacia el norte; por ejemplo en Barcelona apunta hacia el norte y hacia la vertical hacia abajo.

El campo en la tierra fluctua constantemente, se debe hacer la media.

Si acercamos el magnetómetro hacia algun elemento metálico grande o magnetizado se distorsionado.

### Giroscopio

Mide la velocidad angurlar de giro del dispositivo en cada uno de los ejes de coordenadas. Mide rotaciones, pero no mide desplazamientos. Te da la velocidad de rotación respecto cada uno de los ejes.

Los giróscopos son muy buenos calculando la velocidad angular de rotación, pero normalmente tienen un drift. Eso significa que aúnque este en reposo indican una rotación inexistente muy lenta entorno a un eje.

### Conclusión

Los acelerometros pueden medir la aceleración lineal, pero con el error de la gravedad. Al tener el móvil en la mano y al ser inestable se va a sumar la inestabilidad con la gravedad, por lo que los movimientos precisos son muy complicados para el acelerómetro.

El giróscopo mide rotaciones y no desplazamientos. Mide las rotaciones a corto plazo muy bien. Pero a largo plazo añade un drift.

Si fusiono el Acelerometro y el Giroscopo puedo mejorar los dos. Para eliminar el drift del acelerometro (imprecision de la mano) puedo usar el giroscopio ya que lo va a detectar muy bien. Para eliminar el drift del giroscópio puedo usar el acelerómetro ya que la gravedad en media siempre va a apuntar al mismo sitio (el giroscopio dice que giro, pero el acelerometro dice que no.)

Acelerometro de 6 ejes: Acelerómetro+Giróscopo fusionados para un mejor funcionamiento.

Hay subrutinas en el sistema operativo que procesan todas estar lecturas RAW que hacen todos estos procesamientos para dar lecturas correctas.

Los sensores raw devuelven vectores de 3 valores uno para cada componente.

Los sensores sintéticos son los que ya nos devuelven la información procesada. 

- El sensor de gravedad nos devuelve un vector 3D indicando la magnitud y dirección de la gravedad. 
- El acelerometro nos devuelve un vector 3D representando la aceleración de cada eje excluyendo la gravedad. 
- El sensor de rotación representa la orientación del disositivo con una combinación de un ángulo y un eje en el que el dispositvo ha sido rotado entorno al eje. 
- Sensor de movimiento significativo indica cuando hay un movimiento suficientemente importante. 
- También hay un sensor de podómetro.
- Cámaras
- Luminosidad
- Proximidad

## Rotaciones: Orientación Relativa y Absoluta

### Rotaciones 3D

No son commutativas, si cambiamos el orden del giro no es lo mismo.

1. La rotación se define como un eje de giro y un angulo de rotación respecto ese eje (Teorema de Euler).
2. Uso de quaterniones para representar la rotación. Una generalización de la cuestion de los números complejos.

**Teorema de Euler**: En un espacio 3D cualquier desplazamiento de un cuerpo rígido tal que un punto del cuerpo rígido se mantiene fijo es equivalente a una sola rotación alrededor de un eje que gira a través del punto fijo. Se puede representar como una rotación alrededor de un cierto eje `v` y un ángulo respecto ese eje. Una rotación 3D siempre deja 2 puntos fijos.

**Quaterniones**: `q=x+ix+jy+kz` es una generalización de los números complejos a 4D. Los números complejos tiene dos partes: real e imaginaria y los cuaterniones tienen representación en 4D: parte real (w) y 3 partes imaginarias (i, j, k). 

### Rotaciones relativas

La rotación relativa es aquella relativa al própio dispositivo sin tener en cuenta el mundo exterior. Esto se usa cuando se quiere ignorar la posición del dispositivo relativa a la tierra ya que no se necesita. Cuando esta quieto hay una pequeña rotación a cámara lenta debida a la composición de los própios sensores.

Se necesita una corrección del drift ya que si no cuando el móvi esta quieto se puede creer que está rotando ligeramente entorno a un eje aleatorio.

El giróscopo es muy bueno para indicar rotaciones relativas a corto plazo. En Android el sensor TYPE_GYROSCOPE te retorna la velocidad angular instantanea en los tres ejes en rad/sec. Podemos convertir estas medidas en cuaterniones rotación instantánea para un tiempo corto con una fórmula estudiada en clase.

### Rotaciones absolutas

Usamos la matriz de rotación. La idea básica es encontrar el este,norte y perpendicular a la tierra (gravedad) en coordenadas del dispositivo. Si los tenemos y los ponemos como vectores columna de la matriz de giro y esta matriz nos cambia de coordenadas de la tierra a coordenadas del dispositivo.

La brújula no apunta al norte, apunta en parte hacia el norte y en parte en vertical (en el caso de Barcelona, varia según el campo magnético de la tierra). El acelerómetro nos dice el vertical respecto la tierra si no hay movimientos rápidos y hemos filtrado. Entonces a partir de estas dos lecturas podemos calcular el este haciendo el producto vectorial de estos dos vectores para obtener la perpendicular (`g` (magnet )*`v` (aceler)).

## Redes Celulares (4G / LTE, 2G y 3G)

**Redes multihop**

Son redes creadas a partir de comunicar nodos a través de antenas cercanas que se comunican entre ellas.

![](https://i.imgur.com/4xNPICj.png`)

Son ventajosas pero tienen problemas de throughput y no pueden ser muy grandes. Se usan con pocos nodos.

**Redes infraestructura**

El dispositivo se comunica con una estaicón base que se comunica con otras estaciones base (antena) a través de cable. Solo hay comunicación inalámbrica en el primer y último salto.

Son las más usadas. 2G, 3G, 4G etc. se basan en este tipo de infraestructuras.

Las estaciones base deben tener cobetura en un espacio llamado célula. Cuando un nodo pasa de una célula a la otra se llama **handover**. Las células reales tienen formas complicadas, no son exagonales. Para aumentar la capacidad del canal se usan antenas direccionales que crean sectores. Por ejemplo sectores de 120 grados con 3 antenas. Las antenas urbanas tienen coberturas de cientos de metros.

El tamaño de las células es un parámetro importante. Si tienes celulas grandes es mejor porque es más barata, pero la capacidad agregada es más pequeña.

En zonas densamente pobladas donde hay mas usuarios por m² las celulas son más pequeñas pero hay más handoffs, más torres y una red backbone más grande, por lo que son mas caras.

Estas células se deben conectar a una red fija (backbone) que mantiene el operador que son commutadores, routers, etc. que permiten la operación de la red. Además hay routers con conexión a internet.

### Acceso múltiple

#### TDMA Acceso Múltiple por Divisón de Tiempo

**Síncrono**
Se establece una trama con canales que se repite de forma periódica y los canales se asignan a distintos usuarios.

**Estadístico**
Se establece un mecanismo por el cual los usuarios pueden acceder sin un órden prefijado (Protocolos de acceso al medio). 

Los usuarios transmiten en tiempos distintos con la misma frecuencia portadora. Por eso es por división de tiempo.

#### FDMA División de Frecuencia

Los usuarios transmiten simultáneamente con frecuencias portadoras distintas (2G, 2.5G, 4G...)

--

Cada una tiene sus pros y sus contras. 

En TDMA los usuarios opcupan el canal en tiempos distintos pero las frecuencias se solapan, usan todo el ancho de banda. Los símbolos tienen una duración de 1/Bw, pero al repartir el canal la velocidad de transmisión se reduce en `n` usuarios.

En FDMA todos transmiten a la vez, pero con símbolos de mayor longitud Bw = 1/NT, pero le ancho de banda se debe repartir en `n` subbandas cada una de tamaño `1/n`.

La velocidad y ancho de banda son equivalentes en ambos sistemas.

#### CDMA Code Division Multipe Access

Se envían símbolos a la vez y con la misma frecuencia. Para separar los símbolos usaremos códigos Ortogonales. 

Para esto se usan productos escalares aprovechando las propiedades que estos tienen. Si los dos vectores escalares son ortogonales entre si, su producto escalar es 0.

Si tenemos 3 códigos de N=4 deberemos comprobar que los 3 son ortogonales. Para N=4 el máximo de códigos ortogonales que podemos encontrar es `N`, por lo tanto esto es un limitante en cuanto al número de usuarios simultáneos. Para encontrar el 4o vector ortogonal aprovechamos las propiedades de los productos escalares y aplicar:

![](https://i.imgur.com/9z1U2mD.png)

Este truco se usa en CDMA para el acceso múltiple. Las estaciones usan cada una un código, cuando una estación quiere enviar un bit lo multiplica por el código.

Si las transmisiones se hacen de forma síncrona y todas tienen el mismo nivel de potencia recibida, podemos combinar los códigos de todos los dispositivos en uno solo y luego la estacion base podrá recuperar esos bits transmitidos por cualquiera de los usuarios.

![](https://i.imgur.com/Shk7blq.png)

Las propiedades son un híbrido entre FDMA y TDMA en cuanto a tiempo y uso de la frecuencia. Para un mismo ancho de banda la capacidad es igual que en los casos anteriores, pero tecnologicamente tiene ventajas e inconvenientes.

---

El cambio de versión entre 2G/2.5G --> 3G --> 4G --> 5G se necesita un cambio de chipset ya que no hay compatibilidad hacia atrás. Cuando distintos usuarios están en una mísma celula se hace multiplexación de canales entre los usuarios. Hay canales individuales para cada usuario `Tráfico: info usuario` y `Control`. También hay canales comunes `Control Común`, `Paging: señalización de una nueva llamada`, `Random Access Channel: user request use of channel` y `Broadcast Control: información para todos los usuarios: BS id, etc.`.

#### 4G (LTE)

Aumenta la capacidad de cada célula y mayor capacidad de transmisión para cada usuario. También hay mejoras en la latencia que se ve reducida.

Las bandas de frecuencia son más grandes y más flexibles: de 1.4MHz a 20MHz.

El acceso es distinto en el Downlink (OFDMA) y en el Uplink (UL). También se mejora la eficiencia espectral con el uso de MIMO y scheduling. En LTE como más cerca de la antena mejor es la velocidad de transmisión y se reduce con la distancia.

> OFDMA: Basado en OFDM pero con varios usuarios. Los tiempos de símbolo largos limitan las interferencias entre símbolos debidas al multipath (recordar OFDM). Como tenemos un número de subportadoras grande podemos jugar con esto para mejorar la calidad del servicio. La atenuación es distinta según la posición del usuario pero se puede asignar la mejor subportadora para cada usuario.
> 
> **Problemas**
> 
> La fluctuación en amplitud es muy grande (PAPR alto). Por esto requerimos que los amplificadores de potencia tengan un mayor consumo.
> 
> En el uplink las subportadoras son generadas por los dispositivos de los usuarios por lo que puede haber pequeños drifts que pueden crear interferencias enter subcanales. Por eso en el uplink se sua SC-FDMA, se utiliza una única subportadora que transmite símbolos más pequeños. Esto provoca interferencias entre símbolos pero que se soluciona con algunas técnicas alternativas no estudiadas.

Cada usuario sufrirá una atenuación multitrayecto distinta, por eso se pueden elegir subportadoras según las condiciones del usuario. En LTE se usa un algoritmo de scheduling para asignar estas frecuencias distintas a través de Resource blocks (consisten en 12 subportadoras consecutivas separadas 15KHz en cada uno de los cuales se transmiten 7 símbolos OFDM) asignados a los usuarios y que se van cambiando según las necesidades.

## Mobile Packet Core

**Roaming** Capacidad de la red de saber que un usuario se está moviendo. Para esto el usuario debe tener una funcionalidad de discovery para que sepa en qué celula se encuentra. El nodo debe ser capaz de registrarse con la red para indicar su situación. En 4G es una base de datos llamado HSS (Home Scaner Server). Una vez el usuario está registrado la red debe ser capaz de localizarlo para enviarle los paquetes.

En 4G se simplifica el packet core y se elimina la parte de commutación de circuitos y solo se usa la commutación de paquetes.

![](https://i.imgur.com/of0WEd1.png)

- `SGW - Serving Gateway` se encargan de gestionar la mobilidad de los usuarios según van cambiando de nodo y establecen un tunel con el PGW para que se puedan dirigir al usuario que quieren. 
- `PGW - Packet Data Network Gateway` es el router que nos da acceso a internet o a la red de voz además de filtrado de paquetes y gestión de recursos por usuario.
- `MME - Mobility Management Entity` se encarga de la señalización y control de funciones para permitir el tracking, paging, roaming y handovers.
- `HSS - Home Suscriber Server` se encarga de las funciones del HLR y el AuC (Home Location Register) y (Authentication Center).
