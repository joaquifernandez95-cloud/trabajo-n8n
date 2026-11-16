1. Introducción 
El presente proyecto consiste en desarrollar un sistema automatizado de atención al cliente 
para un centro de estética, utilizando la plataforma n8n y herramientas de inteligencia 
artificial. 
El objetivo es optimizar la gestión de consultas de clientes, automatizar las respuestas 
sobre tratamientos y precios, y almacenar cada interacción para facilitar el seguimiento por 
parte del establecimiento. 
El sistema permite recibir mensajes, consultar información almacenada en Google Sheets, 
procesar los datos mediante un agente de inteligencia artificial y devolver una respuesta 
automática al cliente. 
Además, cada consulta queda registrada en una planilla de Google Sheets, permitiendo que 
el centro de estética disponga de un historial organizado de las interacciones. 
2. Objetivos del proyecto 
Objetivo general 
Desarrollar un workflow de automatización que permita mejorar la atención al cliente de un 
centro de estética mediante la integración de diferentes fuentes de información y 
herramientas de inteligencia artificial. 
Objetivos específicos 
● Recibir consultas de clientes mediante un Webhook. 
● Consultar información de tratamientos, precios y duración desde Google Sheets. 
● Interpretar los mensajes utilizando un agente de inteligencia artificial. 
● Generar respuestas automáticas y personalizadas. 
● Registrar las consultas y respuestas en una base de datos. 
● Devolver el resultado al sistema que originó la consulta. 
3. Herramientas utilizadas 
Herramienta 
n8n Cloud 
Webhook 
Google Sheets 
OpenAI 
AI Agent 
Aggregate 
Respond to 
Webhook 
Postman 
Función dentro del proyecto 
Plataforma de automatización 
Recibe los mensajes de los clientes 
Almacena tratamientos, precios y consultas 
Proporciona el modelo de inteligencia artificial 
Interpreta consultas y genera respuestas 
Agrupa los registros obtenidos de Sheets 
Devuelve la respuesta al cliente 
Simula el envío de mensajes para realizar 
pruebas 
4. Fuentes de información 
El sistema utiliza dos fuentes principales: 
Fuente 1: Webhook 
Es la entrada de información del sistema. Recibe los datos enviados por un cliente, 
incluyendo: 
● Nombre. 
● Número de teléfono. 
● Mensaje o consulta. 
Fuente 2: Google Sheets 
Funciona como fuente de información interna del centro de estética. 
La primera pestaña contiene el catálogo de tratamientos, sus precios y duración. 
La segunda pestaña almacena las consultas recibidas, junto con los datos del cliente y las 
respuestas generadas por el sistema. 
5. Arquitectura del workflow 
El flujo de trabajo se desarrolla mediante la siguiente secuencia: 
1. Webhook 
Recepción de datos del cliente 
2. Google Sheets 
Consulta del catálogo de tratamientos 
3. Aggregate 
Agrupación de los datos obtenidos 
4. AI Agent + OpenAI 
Interpretación y generación de respuesta 
5. Google Sheets 
Registro de la consulta y su respuesta 
6. Respond to Webhook 
Entrega de la respuesta al cliente 
6. Descripción del funcionamiento 
Etapa 1 – Recepción de información 
El cliente envía un mensaje al sistema. El Webhook recibe los datos y los entrega al 
workflow. 
Etapa 2 – Consulta de información 
Google Sheets obtiene los tratamientos disponibles, sus precios y duración. De esta 
manera, el agente utiliza información previamente cargada y no necesita inventar los datos. 
Etapa 3 – Procesamiento de datos 
El nodo Aggregate reúne los registros de Google Sheets en una única lista para facilitar su 
utilización por parte del agente. 
Etapa 4 – Inteligencia artificial 
El AI Agent utiliza OpenAI para interpretar el mensaje recibido y elaborar una respuesta. 
Se configura un conjunto de instrucciones que establece límites claros: no inventar precios, 
no ofrecer tratamientos inexistentes y no confirmar turnos sin verificar su disponibilidad. 
Etapa 5 – Almacenamiento 
El sistema agrega una nueva fila en la pestaña Consultas de Google Sheets, registrando la 
fecha, el nombre, el teléfono, el mensaje y la respuesta generada. 
Etapa 6 – Entrega del resultado 
Finalmente, Respond to Webhook devuelve la respuesta generada por el agente al sistema 
que realizó la consulta. 
7. Ejemplo práctico de funcionamiento 
Para comprobar el funcionamiento del sistema se realizó una prueba utilizando Postman 
como simulador de mensajes. 
Se envió la siguiente consulta: 
None 
{ 
"nombre": "Carolina", 
"telefono": "1165432100", 
"mensaje": "Hola, quisiera saber cuánto cuesta la 
radiofrecuencia y cuánto dura." 
} 
El sistema recibió los datos, consultó Google Sheets y envió la información al agente de 
inteligencia artificial. 
El agente elaboró una respuesta utilizando los datos del catálogo. 
Posteriormente, Google Sheets registró automáticamente la consulta y la respuesta 
generada. 
Finalmente, el sistema devolvió la respuesta mediante Respond to Webhook. 
Resultado de la prueba: se verificó la ejecución correcta de los nodos y el registro de la 
información en Google Sheets. 
8. Seguridad y limitaciones 
Se establecieron instrucciones para reducir errores en las respuestas del agente: 
● No inventar precios ni tratamientos. 
● Utilizar la información proporcionada por Google Sheets. 
● No confirmar turnos sin verificar previamente la disponibilidad. 
● Solicitar información adicional cuando sea necesario. 
● Mantener un lenguaje profesional y cordial. 
La solución utiliza servicios en la nube, por lo que requiere conexión a Internet y depende 
de la disponibilidad de los servicios externos. 
También es importante considerar que los datos personales de los clientes deben 
protegerse mediante permisos de acceso adecuados, credenciales seguras y políticas de 
privacidad. El hecho de utilizar nombres y teléfonos no significa que esos datos carezcan de 
protección. 
Actualmente, el sistema registra solicitudes de turnos, pero no administra una agenda real ni 
confirma reservas. 
9. Posibilidades de mejora y escalabilidad 
El proyecto puede ampliarse incorporando nuevas funcionalidades: 
1. Google Calendar: consultar disponibilidad y registrar reservas confirmadas. 
2. Gmail: enviar automáticamente las respuestas o confirmaciones por correo 
electrónico. 
3. WhatsApp Business: permitir que los clientes interactúen directamente desde 
WhatsApp. 
4. Gestión de cancelaciones: permitir cancelar o modificar solicitudes. 
5. Escalabilidad: si aumenta considerablemente el volumen de mensajes, incorporar 
procesamiento en paralelo, colas de ejecución, almacenamiento más robusto y 
mecanismos de control de errores. 
Estas mejoras permitirían transformar el asistente en un sistema integral de gestión de 
atención al cliente. 
10. Conclusión 
El desarrollo de este proyecto permitió implementar una solución de automatización que 
integra diferentes fuentes de información, procesamiento mediante inteligencia artificial y 
almacenamiento de resultados. 
La utilización de n8n permitió conectar servicios externos y diseñar un flujo de trabajo 
automatizado sin necesidad de desarrollar una aplicación desde cero. 
El sistema cumple con el objetivo planteado: recibir información desde distintas fuentes, 
procesarla mediante herramientas vistas durante el curso y entregar un resultado 
estructurado y utilizable. 
Además, demuestra cómo la inteligencia artificial puede incorporarse a un negocio real para 
optimizar tareas administrativas, mejorar la atención al cliente y reducir el trabajo manual. 
En un negocio de atención al público que depende de WhatsApp e Instagram las 24 horas, 
la infraestructura en la nube garantiza disponibilidad continua sin depender de una 
computadora encendida en el local ni de la conexión a internet de la recepción. Por eso mi 
decisión en este proyecto va a ser correr el modelo en la nube.  
En cuanto al caso de roi justificado: 
Tiempo invertido en chats: Una conversación promedio (saludo, pasar precios, 
explicar el tratamiento, buscar hueco en agenda y confirmar) lleva unos 6 minutos 
de ida y vuelta. Con 120 consultas diarias, se necesitan 12 horas hombre por día, lo 
que obliga a tener al menos dos personas dedicadas casi exclusivamente al chat. 
Costo salarial directo: En Argentina, el costo laboral total de una recepcionista de 
jornada completa ronda entre $1.100.000 y $1.400.000 ARS mensuales. Si 
necesitás dos personas para cubrir turnos y volumen de mensajes, el gasto fijo 
supera los $2.400.000 ARS al mes. 
Pérdida de pacientes fuera de horario: El 45% de las consultas en estética y 
salud entran entre las 19:00 y las 00:00 (cuando la gente sale de trabajar) o los fines 
de semana. Si el mensaje se responde al día siguiente, el paciente ya escribió a 
otras tres clínicas y reservó en la que le contestó primero.  
Y por ultimo dejo pegado el system prompt que utilice en el nodo de agent ai:  
Sos un asistente virtual de un centro de estética. 
Tu función es atender consultas de clientes sobre tratamientos, precios, duración y 
solicitudes de turnos. 
INSTRUCCIONES: 
1. Respondé siempre de manera cordial, clara y profesional. 
2. Utilizá exclusivamente la información proporcionada por Google Sheets para 
informar precios, tratamientos y duración. 
3. Nunca inventes precios, tratamientos ni horarios disponibles. 
4. Si un cliente quiere reservar un turno, solicitá o confirmá el día y horario 
deseados. 
5. No confirmes reservas reales. Aclarale al cliente que su solicitud será 
revisada por el centro de estética. 
6. Si falta información, hacé una pregunta para obtenerla. 
7. No inventes información que no figure en los datos disponibles. 
8. Respondé siempre en español. 
Tu objetivo es brindar una buena atención y recopilar correctamente las solicitudes 
de los clientes.
