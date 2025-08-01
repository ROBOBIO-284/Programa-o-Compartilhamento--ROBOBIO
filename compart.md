#Programação
##Aqui explicaremos as importações da nossa programação.
###Importações:

```python
import motor, motor_pair
from motor_pair import PAIR_1, move_tank_for_time
from hub import port
```

motor_pair.pair(motor_pair.PAIR_1, port.E, port.F)

async def mover_cm (CM, drc, vel, acel):

    ace_des = 5000 

    global PAIR_1 

    graus = int ((CM/19.60)*360)

    if drc == 't': 
        graus = -graus

    if acel == 's': 
        ace_des = 1800
    else:
        ace_des = 3000

    await motor_pair.move_tank_for_degrees(PAIR_1, graus, vel*10, vel*10, stop=motor.HOLD, acceleration=ace_des, deceleration=ace_des)

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