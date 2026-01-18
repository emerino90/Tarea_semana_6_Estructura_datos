#Implementar un método dentro de la lista enlazada que permita invertir los datos almacenados en una lista enlazada, es decir que el primer elemento pase a ser el último y el último pase a ser el primero, que el segundo sea el penúltimo y el penúltimo pase a ser el segundo y así segundo y así sucesivamente.

class Nodo:
    def __init__(self, dato):
        self.dato = dato
        self.siguiente = None # Enlace al siguiente nodo

class ListaEnlazada:
    def __init__(self):
        self.cabeza = None # Primer nodo de la lista

    def agregar(self, dato):
        # Método auxiliar para añadir nodos
        nuevo_nodo = Nodo(dato)
        if not self.cabeza:
            self.cabeza = nuevo_nodo
            return
        ultimo = self.cabeza
        while ultimo.siguiente:
            ultimo = ultimo.siguiente
        ultimo.siguiente = nuevo_nodo

    def imprimir(self):
        # Método auxiliar para mostrar la lista
        actual = self.cabeza
        elementos = []
        while actual:
            elementos.append(str(actual.dato))
            actual = actual.siguiente
        print(" -> ".join(elementos))

    def invertir_lista(self):
        """
        Invierte la lista enlazada usando un enfoque iterativo (O(n)).
        """
        prev_node = None  # Puntero al nodo anterior (inicialmente None)
        current_node = self.cabeza # Puntero al nodo actual (empieza en la cabeza)
        
        # Itera mientras haya un nodo actual
        while current_node:
            # 1. Guarda el siguiente nodo antes de modificar el puntero
            next_node = current_node.siguiente 
            
            # 2. Invierte el puntero 'siguiente' del nodo actual
            current_node.siguiente = prev_node 
            
            # 3. Mueve los punteros hacia adelante
            prev_node = current_node # 'prev_node' ahora es el nodo que acabamos de procesar
            current_node = next_node # 'current_node' se mueve al siguiente original

        # Cuando el bucle termina, 'prev_node' es el último nodo original,
        # que ahora es la nueva cabeza de la lista invertida.
        self.cabeza = prev_node

# --- Ejemplo de Uso ---
lista = ListaEnlazada()
lista.agregar(1)
lista.agregar(2)
lista.agregar(3)
lista.agregar(4)
lista.agregar(5)

print("Lista original:")
lista.imprimir() # Salida: 1 -> 2 -> 3 -> 4 -> 5

lista.invertir_lista()

print("\nLista invertida:")
lista.imprimir() # Salida: 5 -> 4 -> 3 -> 2 -> 1

# EJERCICIO 2  
#Implementar el método de búsqueda en la clase lista, el cual debe retornar el número de cual debe retornar el número de veces que se encuentra el dato dentro veces que se encuentra el dato dentro de la lista. de la lista. En caso de no encontrarse, el método d En caso de no encontrarse, el método debe mostrar un mensaje indicando que el dato mostrar un mensaje indicando que el dato no fue enc no fue encontrado. El parámetro de entrada del ontrado. El parámetro de entrada del método es el valor que método es el valor que se desea buscar.
class MiLista:
    def __init__(self):
        self.elementos = [] # Inicializa la lista vacía

    def agregar(self, dato):
        self.elementos.append(dato)

    def buscar_ocurrencias(self, valor_a_buscar):
        """
        Busca un valor en la lista y retorna el número de veces que aparece.
        Muestra un mensaje si no se encuentra.
        """
        contador = 0
        for elemento in self.elementos:
            if elemento == valor_a_buscar:
                contador += 1 # Incrementa el contador si el elemento coincide

        if contador == 0:
            print(f"El dato '{valor_a_buscar}' no fue encontrado en la lista.")
            return 0 # Retorna 0 o podrías retornar None o -1
        else:
            return contador

# --- Ejemplo de Uso ---
mi_lista = MiLista()
mi_lista.agregar(10)
mi_lista.agregar(20)
mi_lista.agregar(10)
mi_lista.agregar(30)
mi_lista.agregar(10)
mi_lista.agregar(40)

# Buscar un dato que sí está
veces_encontrado = mi_lista.buscar_ocurrencias(10)
print(f"El número 10 se encontró {veces_encontrado} veces.") # Salida: El número 10 se encontró 3 veces.

# Buscar un dato que no está
veces_encontrado_2 = mi_lista.buscar_ocurrencias(50) # Salida: El dato '50' no fue encontrado en la lista.
print(f"El número 50 se encontró {veces_encontrado_2} veces.") # Salida: El número 50 se encontró 0 veces.

# EJERCICIO 3 
#Crear una lista enlazada con 50 números enteros, del 1 al 999 generados aleatoriamente. Una
#vez creada la lista, vez creada la lista, se deben eliminar los nodos qu se deben eliminar los nodos que estén fuera de un r e estén fuera de un rango de valores leídos ango de valores leídos
#desde el teclado.
import random

# 1. Definir la clase Nodo
class Nodo:
    def __init__(self, dato):
        self.dato = dato  # El valor del nodo (un número entero)
        self.siguiente = None # Puntero al siguiente nodo

# 2. Definir la clase ListaEnlazada
class ListaEnlazada:
    def __init__(self):
        self.cabeza = None # El primer nodo de la lista

    # Método para añadir un nodo al final
    def agregar(self, dato):
        nuevo_nodo = Nodo(dato)
        if self.cabeza is None:
            self.cabeza = nuevo_nodo
        else:
            actual = self.cabeza
            while actual.siguiente: # Recorre hasta el último nodo
                actual = actual.siguiente
            actual.siguiente = nuevo_nodo

    # Método para imprimir la lista
    def imprimir_lista(self):
        actual = self.cabeza
        elementos = []
        while actual:
            elementos.append(str(actual.dato))
            actual = actual.siguiente
        print(" -> ".join(elementos))

    # Método para eliminar nodos fuera de un rango [min_val, max_val]
    def eliminar_fuera_rango(self, min_val, max_val):
        actual = self.cabeza
        anterior = None
        
        # Recorrer la lista y eliminar nodos que no cumplan la condición
        while actual:
            if actual.dato < min_val or actual.dato > max_val:
                # Si el nodo actual está fuera de rango, lo eliminamos
                if anterior: # Si no es la cabeza
                    anterior.siguiente = actual.siguiente
                else: # Si es la cabeza
                    self.cabeza = actual.siguiente
                actual = actual.siguiente # Avanzar sin actualizar 'anterior'
            else:
                # Si el nodo está dentro del rango, avanzamos
                anterior = actual
                actual = actual.siguiente

# --- Parte principal del programa ---

# 1. Crear la lista enlazada y llenarla con 50 números aleatorios (1-999)
lista = ListaEnlazada()
for _ in range(50):
    numero_aleatorio = random.randint(1, 999)
    lista.agregar(numero_aleatorio)

print("Lista enlazada original (50 números aleatorios):")
lista.imprimir_lista()
print("-" * 30)

# 2. Leer el rango desde el teclado
try:
    limite_inferior = int(input("Introduce el valor mínimo del rango (ej: 100): "))
    limite_superior = int(input("Introduce el valor máximo del rango (ej: 500): "))
    
    # 3. Eliminar nodos fuera del rango especificado
    lista.eliminar_fuera_rango(limite_inferior, limite_superior)
    
    print(f"\nLista enlazada después de eliminar nodos fuera del rango [{limite_inferior}, {limite_superior}]:")
    lista.imprimir_lista()

except ValueError:
    print("Error: Por favor, introduce números enteros válidos para los límites.")

#ejercicio 4
#Crear una lista enlazada con 50 números enteros, del 1 al 999 generados aleatoriamente. Una
#vez creada la lista, vez creada la lista, se deben eliminar los nodos qu se deben eliminar los nodos que estén fuera de un r e estén fuera de un rango de valores leídos ango de valores leídos
#desde el teclado.
import random

class Nodo:
    def __init__(self, dato):
        self.dato = dato
        self.siguiente = None

class ListaEnlazada:
    def __init__(self):
        self.cabeza = None

    def insertar(self, dato):
        nuevo_nodo = Nodo(dato)
        if not self.cabeza:
            self.cabeza = nuevo_nodo
        else:
            actual = self.cabeza
            while actual.siguiente:
                actual = actual.siguiente
            actual.siguiente = nuevo_nodo

    def mostrar(self):
        actual = self.cabeza
        elementos = []
        while actual:
            elementos.append(str(actual.dato))
            actual = actual.siguiente
        print(" -> ".join(elementos) if elementos else "Lista vacía")

    def filtrar_rango(self, minimo, maximo):
        # Manejar la eliminación en la cabeza de la lista
        while self.cabeza and (self.cabeza.dato < minimo or self.cabeza.dato > maximo):
            self.cabeza = self.cabeza.siguiente
        
        # Manejar la eliminación en el resto de la lista
        actual = self.cabeza
        while actual and actual.siguiente:
            if actual.siguiente.dato < minimo or actual.siguiente.dato > maximo:
                actual.siguiente = actual.siguiente.siguiente
            else:
                actual = actual.siguiente

# 1. Crear la lista y generar 50 números aleatorios
lista = ListaEnlazada()
for _ in range(50):
    lista.insertar(random.randint(1, 999))

print("Lista original:")
lista.mostrar()

# 2. Leer rango desde el teclado
try:
    inferior = int(input("\nIngrese el límite inferior del rango: "))
    superior = int(input("Ingrese el límite superior del rango: "))

    # 3. Eliminar nodos fuera del rango
    lista.filtrar_rango(inferior, superior)

    print(f"\nLista filtrada (solo valores entre {inferior} y {superior}):")
    lista.mostrar()
except ValueError:
    print("Error: Por favor ingrese números enteros válidos.")

#Crear un programa que maneje dos Crear un programa que maneje dos listas enlazadas d listas enlazadas de elementos que almacenen datos d e elementos que almacenen datos de
#tipo enteros. La primera se deben almacenar sólo los números primos, y se agregan por el
#final. La segunda deben contener sólo números Armstrong, se rong, se agregan por el agregan por el inicio de la lista. inicio de la lista.
#Al final, mostrar:
#a. El número de datos El número de datos insertados en cada lista. insertados en cada lista.
#b. Mostrar un mensaje indicando la lista que Mostrar un mensaje indicando la lista que contiene contiene más elementos. más elementos.
#c. Mostrar todos los datos insertados en las listas.
# 1. Definición de Clases y Funciones Auxiliares

class Nodo:
    """Representa un nodo de la lista enlazada."""
    def __init__(self, dato):
        self.dato = dato
        self.siguiente = None

class ListaEnlazada:
    """Implementa una lista enlazada simple."""
    def __init__(self):
        self.cabeza = None
        self.tamaño = 0

    def agregar_al_final(self, dato):
        """Agrega un nodo al final de la lista."""
        nuevo_nodo = Nodo(dato)
        if self.cabeza is None:
            self.cabeza = nuevo_nodo
        else:
            actual = self.cabeza
            while actual.siguiente:
                actual = actual.siguiente
            actual.siguiente = nuevo_nodo
        self.tamaño += 1

    def agregar_al_inicio(self, dato):
        """Agrega un nodo al principio de la lista."""
        nuevo_nodo = Nodo(dato)
        nuevo_nodo.siguiente = self.cabeza
        self.cabeza = nuevo_nodo
        self.tamaño += 1

    def mostrar_lista(self):
        """Muestra todos los datos de la lista."""
        elementos = []
        actual = self.cabeza
        while actual:
            elementos.append(actual.dato)
            actual = actual.siguiente
        return elementos

def es_primo(numero):
    """Verifica si un número es primo."""
    if numero <= 1:
        return False
    for i in range(2, int(numero**0.5) + 1):
        if numero % i == 0:
            return False
    return True

def es_armstrong(numero):
    """Verifica si un número es Armstrong."""
    num_str = str(numero)
    n = len(num_str)
    suma = 0
    for digito in num_str:
        suma += int(digito) ** n
    return suma == numero

# 2. Programa Principal

def main():
    # Inicialización de las listas
    lista_primos = ListaEnlazada()
    lista_armstrong = ListaEnlazada()

    # Datos de ejemplo (puedes modificarlos o leerlos de un input)
    datos_entrada = [153, 17, 370, 2, 9, 371, 4, 1634, 10]

    # Procesamiento de los datos
    for num in datos_entrada:
        # Para la lista de primos (agregar al final)
        if es_primo(num):
            lista_primos.agregar_al_final(num)

        # Para la lista de Armstrong (agregar al inicio)
        if es_armstrong(num):
            lista_armstrong.agregar_al_inicio(num)

    # a. Mostrar el número de datos insertados
    print(f"a. Número de datos en la lista de primos: {lista_primos.tamaño}")
    print(f"a. Número de datos en la lista de Armstrong: {lista_armstrong.tamaño}")

    # b. Mostrar la lista con más elementos
    if lista_primos.tamaño > lista_armstrong.tamaño:
        print("b. La lista de primos contiene más elementos.")
    elif lista_armstrong.tamaño > lista_primos.tamaño:
        print("b. La lista de Armstrong contiene más elementos.")
    else:
        print("b. Ambas listas tienen la misma cantidad de elementos.")

    # c. Mostrar todos los datos insertados
    print("\nc. Datos en la lista de primos:")
    print(lista_primos.mostrar_lista())
    print("\nc. Datos en la lista de Armstrong:")
    print(lista_arm)
    
