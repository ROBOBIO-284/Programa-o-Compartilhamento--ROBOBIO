# ***Programação base - Robobio***

---

## Nesse arquivo, mostraremos uma programação base em Python Spike Prime para as equipes que desejam iniciar com essa linguagem

---

### Sumário
- Importações
- Par global
- mover_cm
- mover_sec

---

### Importações:
#### As importações são componentes essenciais do nosso código, pois é por meio delas que trazemos bibliotecas externas para complementar nossa programação. Abaixo está um exemplo das bibliotecas que utilizamos:

```python
import motor, motor_pair
from motor_pair import PAIR_1, move_tank_for_time
from hub import port
```
---

### Par Global:
#### Também é importante declarar um par de motores de locomoção logo no início do código, fora das funções. Dessa forma, eles se tornam componentes “globais” e podem ser utilizados em diferentes partes do programa. No exemplo abaixo, utilizamos os motores conectados nas portas “E” e “F”, definidos com a ajuda da biblioteca PORT:

```python
motor_pair.pair(motor_pair.PAIR_1, port.E, port.F)
```

---

### Mover Centímetros:
#### Começando agora com a parte prática, temos a função mais simples e inicial, o "Mover Centímetros".


#### Abaixo, temos a definição de uma função utilizando `async def`, seguida pelo nome da função (definido pelo programador) e pelos parâmetros, que também são escolhidos de acordo com a necessidade do operador.

```python
async def mover_cm (CM, drc, vel, acel):
```


#### Agora, vamos para a parte da aceleração e desaceleração padrões de acordo com a nossa necessidade, essa variável será definida mais a frente por nós. 
#### Também 
```python
    ace_des = 5000 

    global PAIR_1 
```
```python
    graus = int ((CM/19.60)*360)
```
```python
    if drc == 't': 
        graus = -graus

    if acel == 's': 
        ace_des = 1800
    else:
        ace_des = 3000
```
```python
    await motor_pair.move_tank_for_degrees(PAIR_1, graus, vel*10, vel*10, stop=motor.HOLD, acceleration=ace_des, deceleration=ace_des)
```

```python
async def mover_sec (SEC, drc, vel, acel):

    ace_des = 5000 

    global PAIR_1 

    if drc == 't': 
        vel = -vel

    if acel == 's': 
        ace_des = 1800
    else:
        ace_des = 3000

    await move_tank_for_time(PAIR_1, vel*10, vel*10, SEC*1000, stop=motor.HOLD, acceleration=ace_des, deceleration=ace_des)
```