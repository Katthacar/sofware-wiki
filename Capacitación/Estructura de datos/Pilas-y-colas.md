
# ¿Qué es una pila o Stack?
Son estructura de datos lineales que funcionan bajo la filosofía LIFO(Last In - First Out)

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d1/Pila.svg/1200px-Pila.svg.png" width="400">


Usos de las pilas:

* Gestionar los fragments en Android
* Gestionar el llamado a funciones
* Evaluar expresiones algebraicas en notación postfija

**Notación postfija:**  1 5 2 * +

<img src="https://i.ibb.co/1JnMQTw/Screen-Shot-2019-01-04-at-11-38-16-AM.png" width="400">
<img src="https://i.ibb.co/Fw8W34z/Screen-Shot-2019-01-04-at-11-38-41-AM.png" width="400">

## Operaciones

* Apilar(PUSH)
* Desapilar(POP)
* Está vacía
* Está llena

## Implementación de la clase Pila en Python

    class Pila(object):
        def __init__(self):
            self.items = []

        def apilar(self, element):
            self.items.append(element)
    
        def desapilar(self):
            self.items.pop()
    
        def isEmpty(self):
            if len(self.items) > 0:
                return True
            else:
                return False

        def getLast(self):
            size = len(self.items)
            if (size > 0):
                return self.items[size - 1]
            else:
                return None
----
# ¿Qué es una cola o Queue?
Son estructura de datos lineales que funcionan bajo la filosofía FIFO(First In - First Out)

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/bb/Cola.svg/1200px-Cola.svg.png" width="400">


Usos de las colas:

* Gestionar la cola de atención en un banco
* Gestionar la venta de tickets masivos


## Operaciones

* Encolar(PUSH)
* Decolar(POP)
* Está vacía
* Está llena

## Implementación de la clase Pila en Python

    class Cola(object):
        def __init__(self):
            self.items = []

        def encolar(self, element):
            self.items.append(element)

        def decolar(self):
            self.items.pop(0)
    
        def getLast(self):
            size = len(self.items)
            if (size > 0):
                return self.items[size - 1]
            else:
                return None

        def getFirst(self):
            size = len(self.items)
            if (size > 0):
                return self.items[0]
            else:
                return None
