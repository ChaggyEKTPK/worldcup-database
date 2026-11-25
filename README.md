# ⚽ World Cup Database

Base de datos **PostgreSQL** con estadísticas de Copas del Mundo y consultas en Bash. Proyecto del currículo [Relational Database de freeCodeCamp](https://www.freecodecamp.org/).

## Qué hace

1. `worldcup.sql` — crea la base `worldcup` con las tablas `teams` y `games`, claves foráneas y constraints.
2. `insert_data.sh` — carga `games.csv` en la base, creando los equipos sin duplicados.
3. `queries.sh` — responde 12+ consultas estadísticas: goles totales, promedios, campeones y equipos por ronda.

## Cómo ejecutarlo

Requisitos: PostgreSQL en marcha y un rol llamado `freecodecamp` (así lo espera el harness de freeCodeCamp).

```bash
# 1. Crear la base y las tablas (te pedirá la contraseña de postgres)
psql -U postgres -f worldcup.sql

# 2. Cargar los datos del CSV
chmod +x insert_data.sh queries.sh
./insert_data.sh

# 3. Ejecutar las consultas
./queries.sh
```

## Ejemplo de consulta

```sql
-- Equipo con más victorias
SELECT name
FROM teams
ORDER BY (
  SELECT COUNT(*)
  FROM games
  WHERE games.winner_id = teams.team_id
) DESC
LIMIT 1;
```

## Esquema

| Tabla | Columnas principales |
|---|---|
| `teams` | `team_id` (PK), `name` (UNIQUE, NOT NULL) |
| `games` | `game_id` (PK), `year`, `round`, `winner_id` (FK → teams), `opponent_id` (FK → teams), `winner_goals`, `opponent_goals` |

Las dos referencias de `games` apuntan a la misma tabla `teams`, así que cada partido relaciona dos equipos.

## Validaciones incluidas

- Claves foráneas entre `games` y `teams` para `winner_id` y `opponent_id`.
- Nombres de equipos únicos.
- Inserción idempotente de equipos con `ON CONFLICT (name) DO NOTHING`.
- Salida limpia de `psql` con `-t --no-align`.

## Tecnologías

- PostgreSQL (JOINs, subconsultas, agregaciones)
- Bash + CSV

## Nota sobre `.freeCodeCamp`

La carpeta `.freeCodeCamp/` es el entorno de pruebas oficial de freeCodeCamp. **No es código mío**: la conservo para poder validar el proyecto con el harness original. El esquema, los scripts y las consultas están en la raíz del repositorio.

## Autor

Diego Aguilar · [GitHub](https://github.com/ChaggyEKTPK)
