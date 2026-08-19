Para esta práctica se utilizó un archivo de ventas exportado desde un sistema legacy. El archivo contenía información de clientes y operaciones de venta en una misma tabla, además de nombres de columnas poco descriptivos, valores nulos, registros duplicados y diferentes tipos de datos.
El objetivo del proceso de transformación fue preparar los datos para su posterior utilización en Power BI, mejorando su calidad, consistencia y estructura antes de realizar el análisis.Las transformaciones se realizaron utilizando Power Query, dentro de Power BI Desktop.

Las transformaciones se realizaron siguiendo un orden determinado para evitar problemas durante el proceso.
1-Carga de datos:Primero se importó el archivo Ventas_export_legacy.xlsx desde Power BI Desktop utilizando el conector de Excel.
En lugar de cargar directamente los datos al modelo, se seleccionó la opción Transformar datos para ingresar al Editor de Power Query y realizar previamente las tareas de limpieza y preparación.
2-Eliminar as filas completamente vacías: Como primer paso de limpieza se identificaron y eliminaron las filas que no contenían ningún dato.
Esta transformación fue necesaria porque las filas completamente vacías no aportan información al análisis y podrían generar registros innecesarios en el modelo.
3-Eliminacion de registros duplicados: Posteriormente se identificaron los registros duplicados y se eliminaron las filas completamente repetidas.
La eliminación se realizó considerando el conjunto de columnas del registro, de manera que no se eliminaran operaciones diferentes que pudieran compartir algunos datos.
Esto permite evitar que una misma operación sea contabilizada más de una vez y afecte indicadores como la cantidad de ventas, facturación total o ticket promedio.
4-Renombrado de columnas: Los nombres técnicos originales fueron reemplazados por nombres descriptivos en español.
Por ejemplo:
COD_OP se reemplaza por	id_operacion
COD_CLI	se reemplaza por id_cliente
NOM_CLI	se reemplaza por nombre_cliente
F_VTA	se reemplaza por fecha_venta
COD_PROD se reemplaza por	id_producto

El objetivo fue mejorar la legibilidad de la información y facilitar su utilización posteriormente en el modelo y en las visualizaciones de Power BI.

4-Corrección de tipos de datos: Después de limpiar y renombrar las columnas se asignaron los tipos de datos correspondientes a cada campo.
Las fechas, como fecha_venta y fecha_alta_cliente, fueron configuradas como Date, ya que se utilizarán para realizar análisis temporales.
Los campos monetarios, como precio_unitario y total_venta, fueron configurados como número decimal, porque representan valores económicos y pueden contener decimales.
La cantidad fue configurada como número entero, debido a que representa unidades vendidas.
Los identificadores, como id_cliente e id_operacion, fueron tratados como texto, ya que funcionan como códigos identificadores y no como valores sobre los cuales se realizarán operaciones matemáticas.
Los campos descriptivos, como nombres, correos electrónicos, ciudades, provincias, categorías y canales, fueron configurados como texto.

Cómo resolviste los valores nulos y duplicados encontrados.

Durante la revisión de los datos se encontraron valores nulos en diferentes columnas.
No se decidió reemplazar todos los valores nulos automáticamente por cero, ya que un valor vacío no necesariamente significa que el valor sea cero.
Por ejemplo, un teléfono o correo electrónico vacío significa que no se dispone de ese dato, mientras que un descuento vacío podría representar la ausencia de un descuento.
Por este motivo, los valores nulos se trataron según el significado de cada campo. En aquellos casos en los que no existía información suficiente para asignar un valor válido, se mantuvo el valor nulo en lugar de introducir información que pudiera distorsionar el análisis.
En el caso de los datos numéricos utilizados para los indicadores, se tuvo especial cuidado de no convertir valores desconocidos en cero automáticamente, ya que esto podría afectar cálculos como promedios y totales.

Los registros duplicados fueron identificados durante la etapa de limpieza y posteriormente eliminados.
La decisión de eliminar duplicados se tomó porque se trataba de registros completamente repetidos y mantenerlos podría generar una doble contabilización de las operaciones.
Esto es especialmente importante en una base de ventas, ya que los duplicados podrían aumentar artificialmente la facturación y la cantidad de operaciones.

Qué criterio usaste para separar los datos del cliente de los de la transacción.
Uno de los principales objetivos de la transformación fue separar la información correspondiente a los clientes de aquella relacionada con las transacciones.

La tabla original contenía ambos tipos de información mezclados.

Tabla Clientes

Se identificaron como datos propios del cliente aquellos que describen a la persona o entidad independientemente de una venta específica:

id_cliente
nombre_cliente
email_cliente
telefono_cliente
ciudad_cliente
provincia_cliente
segmento_cliente
cliente_activo
fecha_alta_cliente

La clave utilizada para identificar de manera única a cada cliente fue id_cliente.

Tabla Transacciones

Se consideraron datos de transacción aquellos que describen una operación de venta concreta:

id_operacion
id_cliente
fecha_venta
id_producto
nombre_producto
categoria_producto
cantidad
precio_unitario
descuento_porcentaje
total_venta
moneda
canal_venta

La clave de la operación es id_operacion, mientras que id_cliente permite relacionar cada venta con el cliente correspondiente.

Esta separación permite evitar la repetición innecesaria de información de los clientes en cada operación y prepara los datos para construir posteriormente un modelo de datos más eficiente en Power BI.

Conclusión:

Luego de aplicar las transformaciones, los datos quedaron preparados para continuar con las siguientes etapas del proyecto en Power BI.
El proceso permitió:
-eliminar filas completamente vacías;
-eliminar registros duplicados;
-utilizar nombres de columnas descriptivos;
-asignar tipos de datos adecuados;
-gestionar los valores nulos según el significado de cada campo;
-separar la información de clientes de la información de transacciones;
-preparar una estructura más adecuada para el análisis y la construcción posterior de visualizaciones y medidas.

En conclusión, la transformación realizada en Power Query permitió mejorar la calidad, consistencia y organización de los datos, dejando el conjunto preparado para la construcción del modelo analítico y del dashboard en Power BI.
