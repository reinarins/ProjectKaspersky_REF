# UiPath_KasperskyPassCheckerREF 

<b>::: IMPORTANTE :::</b> 
<br><br> 
Este es un proyecto creado con el <b>único fin</b> de explorar el <b>Robotic Enterprise Framework</b> de UiPath y de crear un bot siguiendo este marco. Para ello, se han almacenado IDs, datos y correos de empleados FICTICIOS junto a una serie de contraseñas en un archivo Excel, <b>PRÁCTICA NO RECOMENDADA</b> a la hora de cumplir con las directrices en materia de ciberseguridad. 
<hr>

:robot: El <b>objetivo</b> de este bot es comprobar la seguridad de diferentes contraseñas almacenadas en un archivo Excel. Para ello, accede a la web 'Kaspersky Password Checker', introduce una contraseña y solicita nuevas para aquellas contraseñas marcadas como inseguras (icono amarillo) o muy inseguras (icono rojo). Una vez obtenidas estas nuevas contraseñas, las almacena en un Excel nuevo.
<br><br>
Después, accede al artículo 'La calidad de tus contraseñas' de la web 'Seguridad en Internet', y recoge la información de la sección 'Características de una contraseña segura' para guardarla en un archivo de texto. Por último, adjunta ambos archivos en un correo electrónico y los envía a la persona de interés.
<br><br>
Este bot contempla también dos posibles excepciones de negocio:
1. Archivo Excel no encontrado: si el archivo Excel que guarda todos los datos necesarios para el inicio del proceso (donde se almacenan los IDs, los datos y las contraseñas) ha sido cambiado de ubicación o se ha visto modificado su nombre, el bot envía un correo electrónico para notificar del error.
2. Datos incorrectos en el archivo Excel: si en la columna 'IDs' del archivo hay algún caracter no numérico, el bot identifica que no se han guardado los datos correctamente y envía un correo electrónico para notificar del error.

<hr>
Especial hincapié en que este es un bot creado como proyecto final para mi primer curso de RPA en Generation Spain, por lo que insisto en que <b>almacenar datos sensibles en archivos Excel es una práctica que NO DEBE SEGUIRSE</b>.
<br><br>
¡Gracias! :blush:

<hr>

### Documentation is included in the Documentation folder ###


### REFrameWork Template ###
**Robotic Enterprise Framework**

* Built on top of *Transactional Business Process* template
* Uses *State Machine* layout for the phases of automation project
* Offers high level logging, exception handling and recovery
* Keeps external settings in *Config.xlsx* file and Orchestrator assets
* Pulls credentials from Orchestrator assets and *Windows Credential Manager*
* Gets transaction data from Orchestrator queue and updates back status
* Takes screenshots in case of system exceptions


### How It Works ###

1. **INITIALIZE PROCESS**
 + ./Framework/*InitiAllSettings* - Load configuration data from Config.xlsx file and from assets
 + ./Framework/*GetAppCredential* - Retrieve credentials from Orchestrator assets or local Windows Credential Manager
 + ./Framework/*InitiAllApplications* - Open and login to applications used throughout the process

2. **GET TRANSACTION DATA**
 + ./Framework/*GetTransactionData* - Fetches transactions from an Orchestrator queue defined by Config("OrchestratorQueueName") or any other configured data source

3. **PROCESS TRANSACTION**
 + *Process* - Process trasaction and invoke other workflows related to the process being automated 
 + ./Framework/*SetTransactionStatus* - Updates the status of the processed transaction (Orchestrator transactions by default): Success, Business Rule Exception or System Exception

4. **END PROCESS**
 + ./Framework/*CloseAllApplications* - Logs out and closes applications used throughout the process


### For New Project ###

1. Check the Config.xlsx file and add/customize any required fields and values
2. Implement InitiAllApplications.xaml and CloseAllApplicatoins.xaml workflows, linking them in the Config.xlsx fields
3. Implement GetTransactionData.xaml and SetTransactionStatus.xaml according to the transaction type being used (Orchestrator queues by default)
4. Implement Process.xaml workflow and invoke other workflows related to the process being automated
