# Reporte con procedimiento almacenado al día actual y al día anterior:

Se necesita que se generen dos tipos de reportes: 
* Uno del día actual en donde el área de ventas no ha procesado toda la información pero se requiere saber como van las ventas.
* Otro reporte del día anterior en donde el área de ventas a terminado de procesar toda la información. </br></br>
También se requiere que los reportes se suban a un servidor FTP y finalmente enviar un correo especificando si el reporte se subió al servidor FTP satisfactoriamente
o se produjo algún error.

--------------------------------------------------------------
1. Creamos un nuevo paquete SSIS.
2. Usaremos la base de datos de NORTHWND la cual adjunto a este proyecto. "Script-Northwnd.sql"
3. Crearemos los siguientes SPs que también adjunto a este proyecto. "ReporteDiaActual_y_Anterior.sql"

4. En nuestro proyecto SSIS, crearemos dos variables ReporteActual y ReporteDiaAnterior, cada una la definiremos de tipo String y le agregaremos en el campo valor la ejecución del SP terminado por un punto y coma:

<p align="center">
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob//main/Assets/Imagen1.png"  height=150>
</p>

5. Creamos un Data Flow Task, el cual llamaremos Generar Reportes. Ingresamos y en el Data Flow creamos dos nuevos origenes de datos OLE DB Source (Origen Dia Actual y Origen Dia Anterior)para cpnectar con la base de datos NORTHWND y ejecutar directamente los SPs con las variables que creamos:

<p align="center">
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob//main/Assets/Imagen2.png"  height=450>
</p>

Repetimos el procedimiento para Origen Dia Anterior.

6. Ahora vamos a establecer los destinos de Excel, para ello en un repositorio vamos a crear dos archivos de excel. Uno para Reporte Dia Actual y otro para Reporte Dia Anterior. Importante en cada archivo colocar los encabezados de la base de datos.

<p align="center">
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob//main/Assets/Imagen3.png"  height=250>
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob//main/Assets/Imagen4.png"  height=250>
</p>

Procederemos a ejecutar el proyecto para cargar los archivos de Excel.

7. De acuerdo con lo que nos solicitan al inicio del requerimiento, vamos a agregar al control flow un FTP Task para subir los reportes a un servidor FTP.

<p align ="center">
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob//main/Assets/Imagen5.png">
</p>

Configuramos los parametros del servidor, para este ejemplo use una cuenta gratuita de "DriveHQ". Una ves probada la conexión, vamos a agregar en File Transfer el archivo que queremos transferir al servidor FTP. En este caso agregamos el LocalPath (El archivo Excel que creamos para Reporte Dia Actual y Reporte Dia Anterior).
También agregamos el RemotePath (/My Documents) la ubicación dónde queremos alojar el archivo en el servidor FTP.

<p align ="center">
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob//main/Assets/Imagen6.png">
</p>

Repetimos el mismo proceso para el FTP Reporte Dia Anterior. 
Nota: En la opción de OverwriteFileAtDest colocar True.

Podemos ejecutar el proyecto para validar que efectivamente se cargaron los archivos al servidor FTP.

<p align ="center">
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob//main/Assets/Imagen7.png">
</p>

