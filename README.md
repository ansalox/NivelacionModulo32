TALLER NIVELACIÓN
MÓDULO 3

Propuesta para el grupo CM3 Colsubsidio
Carlos Fabián Zuluaga Alzate

RESUMEN
Propuesta de ejercicio relacionado a los temas vistos hasta la fecha 11/02/2022 que
abarca fundamentos de Angular, Node.js/express y mongodb.

EJERCICIO
En el centro de la ciudad hay una pequeña empresa que se orienta al lavado de
vehículos, y los propietarios quieren iniciar la labor de sistematización para hacer los
procesos más ágiles en el lavado (y obviamente para analizar la información financiera).
Lo que quiere específicamente el cliente es sencillo. Le solicita a nuestros
desarrolladores la creación de una página web que tenga lo siguiente:
1. Una página(componente) de bienvenida.
2. Un botón en la página de bienvenida que lo lleve a otro componente que tenga un
formulario básico donde se puedan introducir los siguientes datos (datos como los
tipos deben ir en minúsculas y sin caracteres especiales como las tildes):
a. Nombre del trabajador que iniciará el lavado.
b. Identificación del trabajador que realizará el lavado.
c. Nombre del propietario del vehículo.
d. Identificación del propietario.
e. Fecha del servicio.
f. Tipo de vehículo (si es Motocicleta, Automóvil o Camión).
g. Tipo de lavado (sencillo o Brillado)
h. valor del lavado (dependerá del tipo de vehículo y tipo de lavado: sí es un
lavado sencillo el valor base será de 10000 COP, si es brillado el valor base
será de 20000 COP; Ya teniendo el valor base le sumamos un valor adicional
según el tipo de vehículo: si es motocicleta se le agregarán 5000 COP, si es
Automóvil serán 30000 COP más, y si es camión se le adicionará 60000 COP.
3. Un botón que pueda enviar a través de una petición HTTP los datos del formulario
hacia un servidor en Node.js que use express para atender esa solicitud.
4. Luego de que el trabajador haya enviado los datos, debe poder visualizar un
mensaje en la página informando sobre si el registro del lavado fue guardado
correctamente o si ocurrió algún error durante el registro de ese lavado.

1

Adicionalmente el cliente requiere que esos registros queden guardados, por lo tanto
deberá integrar en el servidor de express una persistencia mediante la base de datos de
mongodb. Los datos se deben almacenar en una colección llamada ColombianCarWash y
la estructura/módelo de los documentos que se deben almacenar en la colección debe ser
la siguiente:
{
workerId: number,
workerName: string,
clientId: number,
clientName: string,
vehicleType: string,
washType: string,
washPrice: number
}
Por ahora, como es un desarrollo inicial, no es necesario que realicen un componente
para mostrar un análisis en la página web de ciertas consultas que el cliente nos ha
pedido, pero si deben realizarlas mediante comandos a mongoShell.
Las consultas del cliente son las siguientes (dejaré dos ejemplos):
● (ejemplo) Cuántos servicios de lavado sencillo hay en total.
○ db.ColombianCarWash.countDocuments({washType:"sencillo"})
● Cuántos servicios de lavado brillado hay en total.
● Cual es el valor total de ingresos solo de los vehículos de tipo motocicletas.
● (ejemplo) Cual es el valor total de ingresos solo de los vehículos de tipo camion.
○ db.ColombianCarWash.aggregate([{$match:{"vehicleType":"motocicleta"}},{
$group:{_id: { vehicleType: "$vehicleType" },totalAmountByMotocicleta: {
$sum: "$washPrice" }, count: { $sum: 1 }}}])

● Mostrar la cantidad de lavados que ha hecho el propietario con identificación
“XXXXXXXXXX” (Acá puedes poner cualquier identificación que hayas generado
en la base de datos, por ejemplo si el propietario con documento 12340123401234
ha ido a realizar 10 lavados la ejecución de la consulta debe mostrar un 10, sin
importar el tipo de lavado).
● Consultar los ingresos totales entre un rango de fechas, para este caso del último
mes. (pueden probar simulando servicios de lavado que tengan fecha de enero, y
realizar otros de febrero; la consulta debe retornar la suma de los washPrice de
los registros de febrero únicamente).

2

CONVENCIONES
● El ejercicio debe ser realizado utilizando Angular para la página web (frontend) y
Node.js con express para el servidor (backend).
● Las peticiones HTTP que se usen en angular para enviar los datos del formulario a
la API/Servidor de Node.js/Express deben gestionarse a través de servicios no se
deben hacer directamente en el *.ts del componente.
● Tanto el front como el backend deben ser subidos a un repositorio en github
(ambas carpetas en el mismo repositorio y separadas; una carpeta que diga front y
otra que diga back)
● La base de datos de mongodb debe estar alojada en un cluster de mongodb Atlas
(servicio de cloud para bases de datos de mongodb), allí encontrarán un servicio
de uso gratuito para que puedan practicar:
https://www.mongodb.com/es/cloud/atlas/register
● Las consultas pedidas por el cliente deben ir en un archivo de texto y este debe
también subirse al mismo repositorio. por lo tanto tendrán una carpeta “back”
otra “front” y un txt con las consultas en ese repositorio de github.

Cualquier duda y/o tutoría respecto al taller, pueden ubicarme por el canal oficial de
discord mediante el siguiente link de invitación: https://discord.gg/n8wB9Z7n, o al correo
bictia.proyectos@bit.institute.
