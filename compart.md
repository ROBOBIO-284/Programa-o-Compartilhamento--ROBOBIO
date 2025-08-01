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

### Variáveis
- CM = centímetros
- drc = direção
- vel = velocidade
- acel = aceleração

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


#### Agora passamos para a configuração dos valores padrão de aceleração e desaceleração, ajustados conforme a nossa necessidade. Essa variável será definida mais adiante por nós.
#### Também realizamos a importação da variável `global PAIR_1`, que já havia sido declarada anteriormente como o par principal de motores — conectados nas portas "E" e "F".

```python
    ace_des = 5000 

    global PAIR_1 
```


#### Aqui temos uma parte essencial do nosso código: a conversão de distância (em centímetros) para graus de rotação do motor. Como as funções pré-definidas do Python para o Spike Prime não permitem o uso direto de centímetros, utilizamos a fórmula: `(centímetros / circunferência da roda) * 360`. Isso nos permite trabalhar com medidas em centímetros no nosso programa, convertendo automaticamente para graus, que é a unidade aceita pelo controle dos motores.

```python
    graus = int ((CM/19.60)*360)
```


#### Esse trecho do nosso código está dividido em duas partes principais:

#### 1. Direção do movimento:
- Verificamos se a direção está definida como "trás". Nesse caso, a velocidade será negativa, indicando que o robô deve se mover para trás.

#### 2. Configuração da aceleração: Verificamos se a opção de aceleração está ativada.

- Se estiver, utilizamos o valor 1800, que é um padrão adotado por nós com base no comportamento do Python para o Spike Prime.

- Caso contrário, utilizamos o valor 3000, representando uma aceleração mais suave ou ausente.

```python
    if drc == 't': 
        graus = -graus

    if acel == 's': 
        ace_des = 1800
    else:
        ace_des = 3000
```


#### Agora entramos na parte prática do nosso código. É aqui que colocamos em ação todas as definições feitas anteriormente, utilizando a função motor_pair.`move_tank_for_degrees()`.
#### Nessa função, passamos os seguintes parâmetros:
- Par de motores: utilizamos a variável global que define os motores principais.

- Graus: o valor calculado a partir da conversão dos centímetros para graus.

- Velocidade: multiplicamos nossa velocidade por 10, já que o Python para Spike Prime usa uma escala de 0 a 1000.

- Parada: usamos o modo HOLD, que mantém os motores travados após o movimento.

- Aceleração e desaceleração: passamos a variável ace_des, que já foi configurada anteriormente conforme nossa lógica.

```python
    await motor_pair.move_tank_for_degrees(PAIR_1, graus, vel*10, vel*10, stop=motor.HOLD, acceleration=ace_des, deceleration=ace_des)
```

