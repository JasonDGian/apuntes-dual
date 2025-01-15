# 📌 Crear un Job

# 📌 Uso de variables en Jobs.
En los scripts que escribimos para las tareas de Jenkins podemos hacer uso de variables y variables de entorno de la terminal que el servicio emplea.

#### 🧮 Ejemplo de uso.   
En la sección ejecutar escribimos nuestro script, declarando una variable personalizada que a su vez invoca la variable `DATE` con el switch `%r`.

```bash
AHORA=$(date + "%r)
echo "La hora actual es: $AHORA" > /tmp/ahora
```   
   
**Ejemplo en tarea**.
   
![image](https://github.com/user-attachments/assets/f1ece043-bd30-4be5-ad6b-803c5a6bec91)
    
**Salida de la consola**.
    
![image](https://github.com/user-attachments/assets/a6b7a69f-4233-4471-96af-4fd88a50b3a2)
