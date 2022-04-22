# HTTP (HyperText Transfer Protocol)
- Es un protocolo de capa de aplicación para transmitir documentos hipermedia
- Protocolo sin estado
- Diseñado para la comunicación entre navegadores y servidores
- Sigue el modelo clásico de cliente-servidor
- Se envía a través de TCP, o a través de una conexión TCP encriptada TLS

## Componentes de sistemas basados en HTTP
En un sistema las solicitudes (requests) las envía un agente de usuario, para ser
manejadas por un servidor y enviar una respuesta (response).
Existen numerosas entidades entre el cliente y servidor (proxies, cache ...). Así como,
más computadoras, enrutadores, módems y más, que debido al diseño en capas de la Web,
quedan ocultas en las capas de red y tranporte.
### Cliente: Agente de usuario
Es cualquier herramienta que actua en nombre del usuario, quien es siempre la entidad
que inicia una solicitud.
Comunmente un navegador, quien traduce instrucciones en una pagina web a solicitudes HTTP
e interpreta respuestas HTTP para presentar al usuario una respuesta clara.
### Servidor web
Encargado de servir el documento solicitado por el cliente. Quien puede ser una única
maquina, una colección de servidores (para compartir la carga) o un software complejo que
interroga a otras computadoras, para solicitar recursos y generar total o parcialmente el
documento solicitado
### Proxies
Existen numerosas entidades (computadoras, maquinas) que transmiten mensajes HTTP entre
el cliente y servidor, que quedan ocultas debido al diseño en capas de la web. Pero,
aquellos que operan en la capa de aplicación se denominan proxies.
#### Tipos
- Proxies transparentes: Reenvían las solicitudes sin alterarlas
- Proxies no transparentes: Cambian la solicitud de alguna manera y la reenvían
#### Funciones
- Almacenanmiento en caché
- filtrado
- Equilibrio de carga
- Autenticación
- Registro

## Aspectos básicos de HTTP
### HTTP es simple
Es legible por humanos, lo que facilita las pruebas para los desarroladores y reduce
la complejidad para los recien llegados.
### HTTP es extensible
Los encabezados hacen que este protocolo sea fácil de ampliar y experimentar
### HTTP es sin estado, pero no sin sesión
Sin estado, ya que no existe vinculo entre dos solicitudes que se realizan de manera
sucesiva. Mientras que, las cookies de HTTP permiten el uso de sesiones con estado y
así compartir un mismo contexto o el mismo estado entre solicitudes.
### HTTP y conexiones
Una conexión se controla en la capa de transporte, por lo tanto, fuera del alcance
de HTTP. Por lo que HTTP requiere de un protocolo en la capa de transporte que sea
confiable (TCP).
El comportamiento predeterminado de HTTP/1.0 es abrir una conexión TCP para cada par
de request/reponse HTTP, lo cual no es eficiente.
HTTP/1.1 introdujo la canalización y conexiones persistentes, donde la conexión TCP
subyacente se puede controlar parcialmente mediante la "Connection" encabezado.
HTTP/2 fue una paso más allá al multiplexar mensajes a través de una sola conexión.
