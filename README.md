# Try-Except

try: # intenta lo que esta abajo en el codigo, si algo sale mal de ahi, pasa al except(no sale del programa)
    x = float(input("Ingrese un numero: "))
    y = 10
    print(x / 10)
except:
    print("Algo salio mal.") 


# Otro ejemplo con else

while True:
    try:
        a = float(input("Ingrese un numero: "))
        b = float(input("Ingrese otro numero: "))
        print(a + b)
    except: # todos los bloques except siempre van arriba del else
        print("Ha ocurrido un error. Tiene que ingresar 2 numeros.")
    else:
        print("La suma se ha realizado correctamente.")
        break # para que no ejecute constantemente con el while 
    finally: # Finally = haya ocurrido o no un error, lo ejecuta igual
        print("Fin del bucle.") # esto se ejecuta siempre 
        break # otro break sino sigue pidiendo que ingreses numeros


try:
    n = int(input("Ingrese un numero: ")) # si no poniamos el int, iba a saltar el error
    a = 5 / n 
except Exception as error: # guardamos la excepcion como una variable
    print("Ha ocurrido un error", type(error).__name__) # name para que me tire el error especifico y no todo completo
                                                        # name tambien para que acorte el mensaje


try:
    n = int(input("Ingrese un numero: ")) 
    a = 5 / n 
except TypeError: # ejemplo, si queres dividir un entero y una cadena, si al n lo pongo entre ""
    print("No se puede dividir el numero dentro de una cadena.")
except ValueError: # cuando no puede ser procesado correctamente, ejemplo, cuando queres convertir una cadena a un entero o si queres acceder a un elemento de una lista que no esta, porque no tiene posicion,[0, 1, 2], si queremos acceder al [4] da error porque no existe el elemento 4
    print("Debes introducir una cadena que sea numero.") # salta error si pongo palabras
except ZeroDivisionError:
    print("No se puede dividir por cero. Ingrese otro numero.") # salta si intento dividir por cero
except Exception as error: # todo lo que no capture, me salta con name, que error es y le puedo agregar otro tipo de error que no estaba previsto
    print("Ha ocurrido un error, no previsto.", type(error).__name__)


def dividir(a, b):

    try:
        division = a / b
    except ZeroDivisionError:
        print("No se puede dividir por cero.")
        # return None, siempre retorna algo y como no hay nada, siempre es None
    except TypeError:
        print("Uno de los datos no es un numero.")
    except Exception as error:
        print(type(error).__name__)
    else:
        return division # el return es cuando todo sale bien

# esta manera es más limpia
resultado = dividir(a=0, b=0)
if resultado: # usamos if para que no devuelva None de la linea 55, except ZeroDivisionError
    print(resultado)

# esta manera, mejor explicado
if resultado is not None: # al usar if se comprueba que el resultado es diferente al None por defecto, quiere decir, que la division se realizó correctamente y no fue hecha por 0
    #print(resultado)
    print(resultado)

def interactuar_usuario():

    while True:
        try:
            numero_1 = int(input("Ingrese un numero: "))
            numero_2 = int(input("Ingrese otro numero para dividir: "))
        except ValueError:
            print("No es un numero.")    
            continue # para que vuelva 
        else: # es el bloque que no tiene errores, siempre captura el bucle y vuelve a preguntar
            resultado = dividir(numero_1, numero_2)
        if resultado: # gracias al if no salta None
            print(f"El resultado es: {resultado}")

interactuar_usuario()


# Primero TP
# Registro de usuario con nombre y contraseña
# Utilizar una funcion para almacenar datos y otra funcion para mostrar informacion
# Utilizar un diccionario para almacenar tal informacion con el usuario-contraseña
# Utilzar otra funcion para el log in de usuarios

import json 
from pathlib import Path

def obtener_ruta(): # para que no me envie el archivo a cualquier lado, con una funcion la importamos correctamente

    BASE_DIR = Path(__file__).resolve().parent
    return BASE_DIR

def ingresar_datos() -> dict:

    nombre = input("Ingrese su nombre: ").capitalize()
    edad = int(input("Ingrese su edad: "))
    dni = input("Ingrese su numero de identificacion: ")
    activo = input("Ingrese si esta activo (SI/N0): ")

    diccionario =  {"Nombre": {nombre}, "Edad": {edad},"DNI": {dni}, "Activo": {activo}}
    return diccionario
    
def guardar_datos(diccionario, ruta, nombre_del_archivo): # yo quiero que aca me llegue un formulario, sino tira error en la linea 27

    with open(f"{ruta}/{nombre_del_archivo}", "w") as archivo:
        json.dump(diccionario, archivo, indent=4)
        print("Registro guardado")
    

def main(): # llama a todas las funciones
    
    nombre_del_archivo = "datos.json"
    ruta = obtener_ruta()
    diccionario = ingresar_datos() # a ingresar datos tengo que guardarlo en una variable
    guardar_datos(diccionario, ruta, nombre_del_archivo) # luego que los datos fueron ingresados en el diccionario, los guardo


main() # es lo primero que ejecute python



    

    

