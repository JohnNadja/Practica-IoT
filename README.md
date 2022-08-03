# Práctica de IoT los servicios de Azure
![IoT](/images/IoT.png)

## Índice
### [Introducción](#introducción)
### [Prerrequisitos](#prerrequisitos-para-la-práctica)
### [Práctica con IoT Hub](#práctica-iot-hub) 


### Introducción

Internet of things (IoT) o Internet de las cosas es la conexión de todo aquel dispositivo inteligente que pueden ser los electrodomésticos como las neveras, licuadoras, cafeteras, televisores, etc. En [Azure](https://azure.microsoft.com/es-mx/) se ofrecen servicios de control, administración y monitoreo de datos con los objetos inteligentes. Para más información sobre como funciona IoT en Azure, se pue revisar el siguiente [enlace]https://azure.microsoft.com/es-mx/solutions/iot/).


#### IoT Hub ![hubIcon](/images/icon-IoT-Hub.svg)
Es un servicio de control total de todo objeto inteligente con Azure. Se caracteríza principalmente por ser un servicio tipo [IaaS](https://azure.microsoft.com/es-mx/resources/cloud-computing-dictionary/what-is-iaas/) ya que solo ofrece la infraestructura para la conexión entre dispositivos, además de realizar cualquier acción con los objetos inteligentes. Por su estructura deservicio, no contempla con interfaz gráfica como IoT Central.


#### IoT Central ![centralIcon](/images/icon-IoT-Central.svg)
Es similar este servicio con *Azure IoT Hub* proque de igual manera realiza la conexión de IoT a Azure. Sin embargo, es más simple de usar ya que muestra un Panel (o *Dashboard*) de administración sobre los dispositivos conectados y sólo se requiera utilizar para monitorear dichos dispositivos. Es un servicio tipo [PaaS](https://azure.microsoft.com/es-mx/resources/cloud-computing-dictionary/what-is-paas/) porque Azure realiza la mayor parte de configuraciones para poder cobectar y acceder a los objetos inteligentes. 


#### Azure Sphere ![sphereIcon](/images/icon-Azure-Sphere.svg)

Es un servicio que provee seguridad en Azure para los dispositivos inteligentes de hardware y software. Está disponible tanto para *IoT Hub* como *IoT Central*.  
Es un servicio tipo [PaaS](https://azure.microsoft.com/es-mx/resources/cloud-computing-dictionary/what-is-paas/)

#### IoT Edge ![edgeIcon](/images/icon-IoT-Edge.svg)

Es una conexión a dispositivos, es decir, el puente que realiza el acceso con Azure a través de *IoT Hub* e *IoT Central*.

----

### Prerrequisitos para la práctica
 - Tener una cuenta de Azure para realizar la práctica en su [*Portal*](https://portal.azure.com/#home) (si aún no se cuenta con alguna, se puede hacer el registro en el siguiente [*enlace*](https://azure.microsoft.com/es-mx/free/)). 
 - Contar con una suscripción activa de Azure para poder realizar la práctica (en el enlace anterior se muestra como se puede hacer).
 - Tener una [cuenta de almacenamiento de Azure con CLI](https://github.com/JohnNadja/Practica-Cuenta-de-Almacenamiento#1). Sólo seguir hasta el paso 1.
 - Contar con algún editor de texto de nuestra preferencia. Durante la práctica se usa [Visual Studio Code](https://code.visualstudio.com/). 
 - Tener instalado [Node.js](https://nodejs.org/en/download/) de acuerdo con el Sistema Operativo de la computadora.
    - Para Windows, se debe [colocar la variable de entorno](https://bertofern.wordpress.com/2019/01/08/solucion-node-js-npm-no-reconocido-como-comando-interno-o-externo/) para su correcta ejecución.

- Contrar con la instalación de [Git](https://git-scm.com/downloads) de acuerdo con el Sistema Operativo de la computadora.

----



### Práctica IoT Hub

En esta práctica se utilizaremos el servicio de Azure [IoT Hub](https://azure.microsoft.com/es-mx/services/iot-hub/) para conectar dispositivos y controlar sus funciones disponibles.

#### Requisitos
 - Ingresar al sitio [siguiente](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted) (cuando se solciite) porque este es un simulador (provisionado por Azure en GitHub) de una *Raspberry Pi* para poder realizar la práctica.

#### Instrucciones

1. Buscar en el [Portal de Azure](https://portal.azure.com/#home) y, dentro se buscará el servicio ***Centro de IoT***
    - Parámetros en **Aspectos básicos**:
        |Campo|Descripción|
        |--|--|
        |Suscripción|Seleccionar la suscripción activa o adquirida|
        |Grupo de recursos| Ubicar el recurso en el grupo de recursos deseado (si no se cuenta con alguno, se puede crear ahí mismo).|
        |Nombre de IoT Hub| El nombre desado del recurso nuevo  de IoT. Ej. *iotforge*.|
        |Región|Región donde se localizará el recurso|

    - Parámetros en **Redes**:
        |Campo|Descipción|
        |-|-|
        |Configuración de conectividad| Para esta ocasión será ***Acceso público***|

    Se pulsa **Revisar y Crear** y después **Crear** para finalizar con la edición del nuevo recurso. Esperar hasta que se complete el proceso.

    ![NewHub](/images/NewHub.gif)

2. Una vez dentro del recurso (buscando dentro del grupo de recursos o accediendo direcatemente al recruso), en el panel izquierdo, se encontrará la **Administración de dispositivos** y se seleccionará la opción de ***Dispositivos***. Esto es para "*crear*" un nuevo dispositivo.
    - Se selecciona **Agregar dispositivo**:
        |Campo|Descipción|
        |-|-|
        |Id de dispositivo|Nombre del nuevo dispositivo. Ej: *TempSens*|
    
    - Se **Guarda** y espera a que se cree el dispositivo.

    ![NewDevice](/images/NewDevice.gif)

3. (Seleccionamos *Actualizar* si no aparece aún el dispositivo creado recientemente). Una vez dentro del nuevo dispositivo, se copiará la ***Cadena de conexión principal*** (es una clave para poder tener permiso de enviar datos a Azure).
    - Dentro del sitio de simulación de Rasberry Pi, se ingresará dicha *Cadena de conexión principal* sin los corchetes:
    ```
    const connectionString = '[Your IoT hub device connection string]'
    ```
    Y se ejecuta.

    ![Cadena](/images/Cadena.gif)
    
    - Si envía señales (se enciende el LED), significa que se realizó correctamente y el proceso está seindo ejecutado de forma adecuada.

4. Para verificar que se muestren los datos enviados en IoT Hub (ya que no se cuenta con un entorno gráfico nativo en el servicio), se usará una Aplicación de **Node.js** proprocionada en Azure. Se puede consultar en el siguiente [enlace](https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization). Esta aplicación es un entrono de ejecución de Javascript. Para fines prácticos, sólo nos concierne ejecutar dentro de un servidor la aplicación y así visualizar una pagina web.
    - Se clonará el repositorio (de este paso) en la ubicación local deseada. Es importante saber dónde es su ubicación para poder ejecutar el entorno de forma correcta.
        - Ejemplo de clonación rápida:
        1. Abrir la terminal de linea de comandos (o *CMD*).
        2. Reconocer dónde será la ubicación del repositorio clonado.
        3. Colocar la dirección (Ejemplo: Escritorio) usando el comando;
            ```cmd
            cd Colocar/aquí/Ubicacion/deseada
            ```
            Ejemplo:
            ```cmd
            cd Desktop
            ```
        4. Usar el comando:
            ```git 
            git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
            ```
        5. Esperar a que se realice la clonación de forma correcta.

        ![Cloning](/images/Cloning.gif)
    
    - Posteriormente se abrirá la carpeta donde se ubique el repositorio clonado con ayuda de otra terminal usando **cd**.
    ![2ndterminal](/images/2ndterminal.png)


5. Una vez teniendo la **Cuenta de Almacenamiento** (revisar los *PRERREQUISITOS* si aún no se cuenta con alguna) en el Portal de Azure, Se iniciará su CLI (es un ícono de terminal con un **>** por al centro). Se usará el modo Bash y se ejecuta el siguente comando:

    ``` Bash
    az iot hub connection-string show --hub-name [nombre del recurso Hub] --policy-name
    ```
    Ejemplo:
    ``` Bash
    az iot hub connection-string show --hub-name iotforge --policy-name service
    ```
    
    - Se mostrará un "*conecctionString*". Éste se copia  (y guardar bien) todo l valor que se encuentre dentro de las comillas para que así se obtenga el permiso de recibir los datos que el dispositivo está enviando. 

    ![String](/images/String.gif)


6. Se requiere ahora un *Consumer Group* para poder obtener los datos. Se ejecuta el comando ahí mismo:
    ```CLI
    az iot hub consumer-group create --hub-name [nombre del recurso IoT Hub] --name [NombreDelConsumerGroup]
    ```
    Es importante guardar el nombre del Consumer Group hasta que se vuelva a mencionar.
    ![consumerGroup](/images/consumerGroup.gif)

7. Dentro de una terminal local, se ejecutará el comando siguiente en la ubicación donde se colocó el repositorio clonado:
    ``` bash
    npm install
    ```
    ![npmInstall](/images/npmInstall.gif)

8. Dentro de la terminal, donde se localiza el repositorio, se configuran las variables de entorno (pulsar tecla Enter/Return por cada variable):
    - Primera variable: 
        ``` bash
        set IotHubConnectionString=[colocar sin corchetes la connectionString del paso 5]
        ```
    - Segunda variable: 
        ```bash
        set EventHubConsumerGroup=[NombreDelConsumerGroup]
        ```

    ![variables1](/images/variables1.gif)

9. Se ejecuta el comando:
    ```BASH
    npm start
    ```
    Deberá parecer todo correcto para poder proceder.
    ![npmStart](/images/npmStart.gif)

10. Una vez ejecutándose de fora correcta, se puede revisar en el navegador colocando la dirección `localhost:3000`
    ![navegador](/images/navegador.png)


11. Ahora bien, una vez verificado que se puede realizar de forma local, se puede implementar en la nube con ayuda de [App Servie](https://azure.microsoft.com/es-mx/services/app-service/) para realizar un despliegue en una página web.
    - En la terminal (CLI) de Azure, se colocará el siguiente comando para poder crear dicha página:
        ```BASH
        az appservice plan create --name NombreAppservice --resource-group NombreGrupoRecursosAppService --sku FREE
        ```
    Si todo resulta correcto, aparecerá en alguna línea de respuesta: **`"privisioningState": "Succeded"`**
    
    - Continuando, se tiene que recordar el NombreAppService que se le haya asignado para lo siguiente. Se ejecuta el comando:
        ```BASH
        az webapp create -n myiotwebapp1 -g NombreGrupoRecursosAppService -p NombreAppservice --runtime "node|14LTS" --deployment-local-git
        ```
    
    - Se modificará el App Service (entrando al recurso ya sea buscando los servicios creados recientemente o con la barra de búsqueda) en el portal de Azure. En el recurso, se busca el apartado de **Configuración de TLS/SSL** (en el panel izquierdo) y se asegurará que únicamente se encuentre habilitada la función de **Sólo HTTPS**
    ![HTTPS](/images/HTTPS.png)
        - Otra manera es usando el comando en el CLI de Azure:
            ``` bash
            az webapp update -n myiotwebapp1 -g NombreGrupoRecursosAppService --https-only true
            ```

        - Progresando en la configuración a tráves del CLI, se ejecuta el sigueinte comando:
            ``` bash
            az webapp config set -n myiotwebapp1 -g NombreGrupoRecursosAppService --web-sockets-enabled true
            ```
    
    - Una vez completado correctamente la ejecución de comandos, se revisa en el recurso de App service el apartado **Centro de Implementación**. Ahí se seleccionará ***Crendenciales GIT o FTPS locales*** 
        - En ámbito de usuario, colocar un nombre de usuario único y contraseña para poder acceder al usar FTP. Estos datos se deben recordar para despúes deslpegar la página web.
        ![FTP](/images/FTP.gif)

        - En el mismo apartado, se íra a Configuración y se buscará la sección **URI de Git Clone** donde se copiará para poder enviar la página y posteriormente, en la terminar local (asegurándose estar dentro de la carpeta del repositorio clonado) se ejecutará el siguiente comando:
            ```git
            git remote add webapp URIGitClone
            ```
            Donde *URIGitClone* será la dirección que se copió en un instante. 
            ![URI](/images/URI.gif)

        - Y por último se despliega la página en Azure con el comando:
            ```git 
            git push webapp master:master
            ```
            En unos pocos segundo aparecerá una ventana emergente que solicitará el usuario y contraseña que se crearon previamente. 
            ![push](/images/push.gif)

    - Sin embargo, se requerirán de nuevo las variables de entorno que se obtuvieron anteriormente. En el recurso de App Service (dentro del Portal de Azure), se irá al apartado **Configuración** y, en ***Configuracíón de la aplicación***, se colocará una *Nueva configuración de la aplicación* que en realidad son las variables de entorno.
        - Primera variable:
            |Parámetro|Valor|
            |-|-|
            |Nombre|IotHubConnectionString|
            |Valor|colocar la ConnectionString que se obtuvo en el paso 5|
        
        - Segunda variable:
            |Parámetro|Valor|
            |-|-|
            |Nombre|EventHubConsumerGroup|
            |Valor|colocar el nombre del Consumer Group que se creó durante el paso 6|

        - Se guardan los cambios y esperar a que se actualice el servicio.
        ![variablesAppService](/images/variablesAppService.gif)

12. Por último, se deberá ir al apartado de **Introducción** de App Service para después buscar la ***URL*** y revisar la página web creada monitoreando los datos.  
![URL](/images/URL.gif)
![monitoreos](/images/monitoreos.png)
----
# **⚠Importante⚠** 

### Recordar que, si no se requiere más del servicio, se puede eliminar pulsando el botón **Detener** después de haber seleccionado la *instancia de proceso* que, se encuentra en **Proceso** del panel izquierdo.

O bien, eliminar el grupo de recursos dentro del [Portal de Azure](https://portal.azure.com/) si no se requiere todo el contenido de dicho grupo.


## Hasta aquí la finalización de la práctica.
