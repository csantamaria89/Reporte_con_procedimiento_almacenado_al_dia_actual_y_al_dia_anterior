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

En nuestro proyecto SSIS, crearemos dos variables ReporteActual y ReporteDiaAnterior, cada una la definiremos de tipo String y le agregaremos en el campo valor la ejecución del SP terminado por un punto y coma:

<p align="center">
<img src="https://github.com/csantamaria89/Reporte_con_procedimiento_almacenado_al_dia_actual_y_al_dia_anterior/blob/main/assets/Imagen1.png"  height=450>
</p>
