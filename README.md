# ⚽ World Cup Database

Base de datos **PostgreSQL** con estadísticas de la Copa Mundial y consultas en Bash. Proyecto del currículo [Relational Database de freeCodeCamp](https://www.freecodecamp.org/).

## Qué hace

1. `worldcup.sql` — crea el esquema: tablas `teams`, `games` con claves foráneas y constraints (`NOT NULL`, `UNIQUE`)
2. `insert_data.sh` — inserta los datos de `games.csv` en la base de datos
3. `queries.sh` — responde 12+ consultas estadísticas (goles promedio por equipo, partidas ganadas, años con el máximo de goles, etc.)

## Ejemplo de consulta

```bash
# Equipo con más victorias
SELECT name FROM teams
ORDER BY (SELECT COUNT(*) FROM games WHERE games.winner_id = teams.team_id) DESC;
```

## Validaciones incluidas

- Claves foráneas entre `games` ↔ `teams` para ambas referencias (`winner_id`, `opponent_id`)
- Nombres de equipos únicos
- Silencia `psql` con `-t --no-align` para salida limpia

## Tecnologías

- PostgreSQL (JOINs, subconsultas, funciones de agregación)
- Bash + CSV
