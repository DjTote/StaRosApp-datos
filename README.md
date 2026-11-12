# StaRosApp · datos

Programa de actividades y organizaciones (peñas, asociaciones…) de las fiestas de
Santa Rosa de Lima de Venta de Baños, en el formato que usa la app **StaRosApp**.
StaRosApp es una app personal y **no oficial**, sin relación con el Ayuntamiento.

> **Estado: en preparación.** La versión de la app publicada en Google Play todavía no
> lee estos ficheros. Los datos actuales son de prueba.

Este repositorio es **público**: cualquiera puede ver su contenido y su historial.

## Direcciones

Publicadas con GitHub Pages:

- `https://djtote.github.io/StaRosApp-datos/events.json`
- `https://djtote.github.io/StaRosApp-datos/organizations.json`

Tras guardar un cambio, GitHub tarda unos minutos en publicarlo y las copias en caché
pueden tardar hasta 10 minutos más. Los móviles lo reciben la siguiente vez que se abre
la app.

## `events.json`: actividades

```json
{
  "events": [
    {
      "id": "1",
      "day": "Viernes",
      "date": "14/08/2026",
      "time": "11:00",
      "title": "Torneo de vóley mixto 3x3",
      "place": "Polideportivo municipal",
      "description": "Bases en cartel aparte.",
      "organicers": [{ "id": 24 }],
      "organizer": "Peña El Atracón"
    }
  ]
}
```

| Campo | Obligatorio | Formato y notas |
|---|---|---|
| `id` | Sí | Texto único. **No lo cambies una vez publicado**: los favoritos de la gente se guardan por id. |
| `day` | Sí | Día de la semana que corresponde a `date`, con mayúscula y tilde: `Lunes`, `Martes`, `Miércoles`, `Jueves`, `Viernes`, `Sábado`, `Domingo`. |
| `date` | Sí | `dd/MM/yyyy`. Es el **día de fiesta**, no el del calendario (ver la regla de la noche). |
| `time` | Sí | `HH:mm` en formato 24 h. |
| `end` | No | Hora de fin, `HH:mm`. Con ella, la actividad sale "En curso" / "Ahora" hasta esa hora; sin ella, durante 30 minutos desde el inicio. Un fin de madrugada es del día siguiente: `"time": "23:30", "end": "02:00"`. |
| `title` | Sí | Nombre de la actividad. |
| `place` | No | Lugar. |
| `description` | No | Texto que se ve al desplegar la ficha. |
| `organicers` | Sí | Lista de organizadores por id: `[{ "id": 24 }, { "id": 3 }]`. Cada id debe existir en `organizations.json`. El id puede ir como número o como texto. |
| `organizer` | No | Nombre en texto. Solo se usa si la actividad no tiene `organicers`. |

**Regla de la noche:** las actividades de 00:00 a 06:59 pertenecen a la noche del día
indicado en `date`. Por ejemplo, una verbena del sábado que empieza a la 01:00 del domingo
se escribe con la fecha del sábado y `"time": "01:00"`. La app ya sabe que en realidad
empieza el día siguiente.

## `organizations.json`: organizaciones

```json
{
  "organizations": [
    {
      "id": "24",
      "name": "Peña El Atracón",
      "type": "PEÑA",
      "address": "Calle Ejemplo 1",
      "year": "1985"
    }
  ]
}
```

| Campo | Obligatorio | Formato y notas |
|---|---|---|
| `id` | Sí | Único y **estable**: las actividades apuntan a él. |
| `name` | Sí | Nombre que se muestra. |
| `type` | Sí | `PEÑA`, `ASOCIACION` o `PUBLICO`. La pantalla de Peñas solo muestra las de tipo `PEÑA`. |
| `address` | No | Dirección. |
| `year` | No | Año de fundación. |

Se pueden añadir campos nuevos (por ejemplo, para mostrar más información de cada peña).
Las versiones de la app que no los conocen simplemente los ignoran.

## Cómo editar

1. Abre el fichero en GitHub y pulsa el lápiz (*Edit*). Funciona también desde el móvil.
2. Cambia lo necesario, revisa comas y comillas, y pulsa *Commit changes*.
3. Si añades una organización nueva y una actividad suya, guarda **primero**
   `organizations.json` y **después** `events.json`.

La app comprueba los dos ficheros antes de usarlos. **No aplica los cambios**, y sigue con
los datos anteriores hasta que se corrijan, si:

- algún fichero no es un JSON correcto (una coma o unas comillas de más o de menos);
- no hay ninguna actividad;
- una actividad u organización no tiene `id` o lo repite;
- una fecha no tiene el formato `dd/MM/yyyy`;
- una actividad apunta en `organicers` a una organización que no existe.

Una hora que no se entiende, un día de la semana que no cuadra con la fecha o una
organización sin nombre no bloquean la actualización.

Cada cambio queda en el historial (*History*), así que cualquier versión anterior se
puede recuperar.
