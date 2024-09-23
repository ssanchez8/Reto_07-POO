# Reto_07-POO

Para este ejercicio se modificó el programa del restaurante del reto 4. Se involucró una nueva clase OrderIterator, encargada de definir un iterador para recorrer cada item perteneciente a la orden registrada por el usuario.
Teniendo en cuenta esto, se definió la clase OrderIterator al inicio del código y se implementaron dentro de ella los métodos __iter__() y __next__(), encargados de retornar la instancia del iterador y retornar cada uno de los alimentos de la orden. El iterador recorre cada item que solicite el cliente accediendo a cada uno de sus atributos (nombre, precio, cantidad, gramaje, etc). A continuación se observa la nueva clase definida.

``` python
class OrderIterator:
    def __init__(self, items):
        self._items = items
        self._index = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self._index < len(self._items):
            item = self._items[self._index]
            self._index += 1
            return item
        else:
            raise StopIteration
```

Merece la pena mencionar que el resto de las clases no sufrieron modificaciones y se mantuvieron con el código del reto 4, además del código encargado de la interfaz que solicita la orden al cliente. 

El otro cambio que sufrió el programa correspondió a la ejecución del mismo. En prmer lugar se modificó el orden de ejecución que se tenía, para que el método print_bill() ejecute la cuenta con el descuento aplicado. Esto se realizó con el fin de agregar la ejecución del iterador con la ayuda de un for. Es decir, el iterador se encarga de recorrer cada uno de los ítems solicitados, y se imprimen como "detalles del pedido", mostrando los artículos con su precio y cantidad. Luego de esto, se solicita al cliente que registre si posee un cupón de descuento, para finalmente ejecutar el método ecargado de imprimir la cuenta con el descuento aplicado a la orden total.

``` python
#Se cambia el orden de la ejecución, para poder iterar en los items de la orden, y luego aplicar el descuento

# Se itera sobre los items de la orden, para mostrar los detalles del pedido
print("\nDetalles de la orden:")
for item in order:
    print(f"{item.name}: Precio - {item.price}, Cantidad - {item.quantity}")
    

selection = input("¿Posee un cupón de descuento? (s/n): ")
if selection == "s":
    discount = int(input("Ingrese el valor porcentual descuento: "))
    order.calculate_discount(discount)


# Imprimir la cuenta
order.print_bill()
````

