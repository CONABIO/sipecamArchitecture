# `AWS Auto Scaling groups`

## 1. Uso de instancias con `autoscaling groups`

---
### 1.1 Creación de instancias


1. Entrar a la consola de amazon con el usuario y _password_ asignados.


2. Entrar al servicio de `EC2`:

    ![](https://i.imgur.com/rfQkuEk.png)


3. En el panel izquierdo, seleccionar: `Auto scaling > Autoscaling Groups`.

4. Seleccionamos el grupo `minikube-sipecam-general-autoscaling-group`:

    ![](https://i.imgur.com/nYxVHBd.png)

5. A continuación veremos el siguiente panel, y debemos seleccionar el botón `Edit`:

    ![](https://i.imgur.com/8J1EPjh.png)

    Posteriormente veremos la siguiente ventana:

    ![](https://i.imgur.com/dLNdARe.png)


    > En este ejemplo el `autoscaling-group` tiene una instancia en funcionamiento, y su máxima capacidad es 1. 

    Para crear una iniciar una nueva instancia debemos modificar los parámetros de la siguiente forma:

    ![](https://i.imgur.com/d4pbBaM.png)

    Posteriormente damos _click_ al botón `update`.


6. Para verificar que la instancia se esté levantando correctamiente, podemos ir a la sección `Instance management`. En este opanel podemos ver que la nueva instancia aún no está en servicio pero se está levantando:
    
    ![](https://i.imgur.com/uuZwWlo.png)



    Una vez el estatus de "lifecycle" de la instancia se encuentra en `InService`, damos click a su respectivo `Instance ID`, lo que nos redirecciona al siguiente panel:


    ![](https://i.imgur.com/mBu3Xpi.png)


    Posteriormente copiamos el `Public IPv4 DNS`


7. Para acceder a `jupyterlab` debemos copiar y pegar en un navegador:

    > https://<ec2 dns ipv4 de la instancia>:30001/myurl


    El _password_ requerido es: [consultar al equipo de desarollo]


8. Para acceder a `kubeflow` debemos copiar y pegar en un navegador:

    > http://<ec2 dns ipv4 de la instancia>:31380




---
### 1.2 Escalamiento hacia abajo

A continuación se describen los pasos hacer escalamiento hacia abajo de las instancias que queremos dejar de utilizar.

1. Debemos repetir los pasos del 1 al 4 de la sección "Creación de instancias" [i.e ir a`EC2 > Auto Scaling groups > minikube-sipecam-general-autoscaling-group`]. Una vez estamos en el panel principal nos dirigimos a la sección `Instance management`:

    ![](https://i.imgur.com/dNXO8w2.png)

2. Una vez en el nuevo panel, podemos observar las instancias que tenemos activas. Y en la parte derecha se puede observar el tipo de protección que tienen a la hora de realizar escalamientos. 

    En este caso, la instancia utilizada tiene la protección "Scale in", lo que implica que está protegida de hacer un escalamiento hacia abajo. 


    ![](https://i.imgur.com/ca3ObDb.png)

    Para desactivar esta protección, seleccionamos el recuadro en la parte izquierda del identificador de la instancia ("Instance ID") y luego el botón `Actions`. Luego, seleccionamos la opción `Remove scale-in protection`:
    
    ![](https://i.imgur.com/Jhjxiwm.png)
    
3. Seleccionamos el panel `Details`, y luego el botón `Edit`:

    ![](https://i.imgur.com/D88MjlO.png)

    Una vez se abre el nuevo panel, actualizamos el nuevo número de instancias requeridas en el grupo de _autoscaling_. En este ejemplo estaba una instancia activa, y ahora no queremos ninguna, por lo que se deben ajustar las opciones de la siguientes forma:
    
    ![](https://i.imgur.com/WFYaIof.png)
    
    
    Al seleccionar el botón `Update`, el escalamiento hacia abajo será completado y la instancia seleccionada será terminada. 

