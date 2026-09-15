# Anote su tensión

Registro de tensión arterial de **Maximiliano Murillo**, compartido por la familia.

La app es un único archivo, `index.html`, servido como página estática. Los datos
están en Firestore (proyecto `tension-tracker-1267b`).

## Cómo está organizado

Hay **una sola hoja compartida**. No hay hojas por persona ni permisos que repartir:
cualquier familiar autorizado entra con su correo, ve las mismas tomas y puede
anotarlas. Lo que escribe uno aparece en el móvil de los demás en un segundo.

    sheets/{domingo}     una semana por documento (id = domingo en que empieza)
      startDate          "2026-09-13"
      days[7]            cada día: 3 tomas por la mañana y 3 por la tarde
      updatedBy          correo del último familiar que anotó
    config/app
      patient            nombre del paciente
    members/{correo}     familiares autorizados (se dan de alta a mano)

La semana va de domingo a sábado y la hoja de la semana en curso se crea sola:
al abrir la app, al volver a ella y cada media hora.

## Dar de alta a un familiar

1. Consola de Firebase → **Authentication** → *Add user*: correo y contraseña.
2. Consola de Firebase → **Firestore** → colección `members` → *Add document*,
   con el **correo en minúsculas como identificador** del documento. El contenido
   da igual; basta con que el documento exista.
3. Entregar el correo y la contraseña a esa persona.

Para retirar el acceso basta con borrar su documento de `members`.

Conviene dejar el registro público desactivado en **Authentication → Settings →
User actions → Enable create (sign-up)**, para que nadie pueda crearse una cuenta
por su cuenta.

## Reglas de seguridad

Están en `firestore.rules`. Si se cambian, hay que pegarlas en la consola de
Firebase (**Firestore → Rules → Publish**): el archivo del repositorio es solo la
copia de referencia.
