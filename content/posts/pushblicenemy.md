+++
title = 'El enemigo público de los programadores de apps júnior: las notificaciones push'
date = 2024-11-28T11:53:37+01:00
draft = false
+++

Como programadores nos encontramos con muchos retos, cada cual más ilógico y extraño que el anterior, pero el auténtico enemigo de cualquier desarrollador de apps son las notificaciones push, que no te engañen. Puedes tardar años en implementar esa pantalla absurda si quieres, que no pasará nada. Pero envías un push a producción y todos te recordarán.

Me explico.

Yo, siendo programador junior, tenía como objetivo en el momento desarrollar un sistema para enviar notificaciones push a las aplicaciones que desarrollábamos. Así que me puse manos a la obra: investigué SDKs, cómo funcionan los pushes a nivel interno y cuál era la mejor manera de programar un servidor para tal objetivo.

Cuando tuve todo lo necesario me puse a ello, generé una aplicación de pruebas y unos certificados específicos y me puse manos a la obra. Todo perfecto, los pushes se enviaban, y sólo donde toca. Además con iconos y metadatos que la app puede usar para saber qué cargar. Genial, ¿no?

Pues vamos a empezar a hacer rollout a todas las aplicaciones, por qué no.

Las primeras aplicaciones empiezan a salir con el sistema que desarrollé integrado en ellas, y empezamos a hacer pruebas controladas. Lo típico, enviar un push por ubicación e ID de dispositivo. El sistema funciona niquelado. Empezamos a añadir más filtros: tiempo, apertura de la app, visita de secciones... todo perfecto.

"Pero, entonces, Kyngo, ¿por qué estás escribiendo este artículo? Parece que a ti te fue todo bien", te preguntarás.

No fue así, créeme. Aún no ha empezado la diversión.

Empezamos a usar el sistema de forma global, cientos de miles de usuarios usan nuestras apps a diario, todo funcionaba rodado. Pero, de repente, nos encontramos con una notificación en una de las apps más populares...

"test"

Al cabo de treinta segundos...

"test 2"

"test abierto por última vez en ..."

"test this one will work"

Todos me miran con los ojos como platos. Yo les miro, pregunto con risa nerviosa que qué sucede, y me enseñan un móvil. Mis ojos se abren de golpe y suelto un grito de "WHAT?".

Uno de los programadores se quita los cascos y se da cuenta de la escena. Pregunto qué ha hecho, y le enseñan los pushes. ¿Su respuesta?

"Ah, no, esto he sido yo. Estoy probando que la API funciona bien."

En producción.

Estaba probando que el sistema funciona bien en producción. Un programador senior con casi 20 años de experiencia en sus espaldas. Tócate los cojones.

Pero, Kyngo, esto va sobre pushes y programadores junior, ¿por qué nos cuentas esto?, te volverás a preguntar.

Por dos motivos, básicamente. El primero, demostrar que ser senior puede no importar una mierda, y el segundo, es demostraros que los pushes pueden convertirse de formas muy random en tu enemigo. Ahora lo entenderás.

Al cabo de dos años de esto, y un programador menos en el róster, nos tocó implementar un sistema de confirmación a través de notificaciones push. Consistía en que entrabas en un sitio, se escaneaba el QR en pantalla por el personal del recinto, y cuando se procesaba, te llegaba un push dándote la bienvenida.

Empecé a implementarlo y hacer pruebas en un entorno controlado, todo parecía funcionar de lujo.

Parecía.

Subimos el sistema a producción tras hacer pruebas, y nos vamos a casa a pasar la noche. A la mañana siguiente llegamos a la oficina y vemos al CEO echando humo. El sistema de pushes no funcionó bien. Pero no como os imagináis.

Resulta que cuando entraba el primero, le llegaba una notificación: "Bienvenid@ al sitio , fulanit@!". Hasta ahí todo bien. Cuando llegaba el segundo, recibía su notificación pertinente.

Pero el primer tío que entró también. Y se iban acumulando. Bienvenido, fulanito. Bienvenido, menganito. Bienvenida, fulanita. Y así toda la noche.

El CEO echando humo, porque habíamos enviado a un solo dispositivo más de setencientos pushes dando la bienvenida a todo cristo, al segundo le llegaron seicientas noventa y nueve, y así sucesivamente hasta el último.

¿Qué pasó? Que la función Lambda que enviaba los pushes se quedaba colgado por un problema interno de AWS que hacía que se tardase más en obtener respuestas, haciendo que se finalizase la ejecución de la función... antes de hacer limpieza.

Treinta segundos son más que suficientes para enviar un push a más de mil dispositivos en un entorno ideal, pero si AWS se queda colgado enviando un solo push ese tiempo... pasa lo que pasa.

¿La moraleja? No uséis Lambda si no sabéis bien lo que hacéis. :)

Con esto aprendimos todos cómo funciona Lambda por detrás, pero vimos que nos faltaba mucho por aprender de desarrollo y pruebas de calidad.

Y capaz que el sistema que implementé siga siendo usado. Espero que, al menos, hayan arreglado los fallos de novicio que cometí al hacerlo. Que seguro que habría más.

¡Salud, y que vuestro código sea resiliente!
