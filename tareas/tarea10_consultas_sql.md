
# Tarea 10: consultas SQL

Crear una base de datos llamada cine y una tabla llamada peliculas_nombre. La tabla debe tener las columnas: pelicula_id como llave primaria autoincremental, titulo, director, genero, anio_estreno, duracion_minutos, calificacion y disponible.
```sql
CREATE TABLE peliculas_alejandro (
    pelicula_id INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(50) NOT NULL,
    director VARCHAR(50) NOT NULL,
    genero VARCHAR(50) NOT NULL,
    anio_estreno INT NOT NULL,
    duracion_minutos INT NOT NULL,
    calificacion DECIMAL(3, 1) NOT NULL,
    disponible BOOL NOT NULL
);
```

Insertar por lo menos 10 películas de diferentes géneros y años.
```sql
INSERT INTO peliculas_alejandro (titulo, director, genero, anio_estreno, duracion_minutos, calificacion, disponible) 
VALUES
('Inception', 'Christopher Nolan', 'Ciencia Ficción', 2010, 148, 8.8, TRUE),
('Pulp Fiction', 'Quentin Tarantino', 'Crimen', 1994, 154, 8.9, TRUE),
('The Matrix', 'Lana Wachowski', 'Ciencia Ficción', 1999, 136, 8.7, FALSE),
('Interstellar', 'Christopher Nolan', 'Ciencia Ficción', 2014, 169, 8.6, TRUE),
('Spirited Away', 'Hayao Miyazaki', 'Animación', 2001, 125, 8.6, TRUE),
('The Godfather', 'Francis Ford Coppola', 'Drama', 1972, 175, 9.2, TRUE),
('Parasite', 'Bong Joon Ho', 'Suspenso', 2019, 132, 8.5, FALSE),
('Whiplash', 'Damien Chazelle', 'Drama', 2014, 106, 8.5, TRUE),
('Gladiator', 'Ridley Scott', 'Acción', 2000, 155, 8.5, TRUE),
('The Final Empire', 'Brandon Sanderson', 'Ciencia Ficción', 2017, 164, 10, TRUE);
```
Mostrar todas las películas.
```sql
SELECT * FROM peliculas_alejandro
```
Mostrar solamente el título, género y año de estreno.
```sql
SELECT titulo, genero, anio_estreno FROM peliculas_alejandro
```
Mostrar las películas disponibles.
```sql
SELECT titulo, director, genero, disponible 
FROM peliculas_alejandro 
WHERE disponible = TRUE
```
Buscar las películas de un género específico.
```sql
SELECT titulo, director, genero, calificacion 
FROM peliculas_alejandro
WHERE genero = 'Ciencia Ficción'
```
Mostrar las películas estrenadas después del año 2015.
```sql
SELECT titulo, director, anio_estreno, calificacion 
FROM peliculas_alejandro
WHERE anio_estreno > 2015
```
Mostrar las películas con calificación mayor a 8.
```sql
SELECT titulo, director, genero, calificacion 
FROM peliculas_alejandro
WHERE calificacion > 8
```
Ordenar las películas de la más reciente a la más antigua.
```sql
SELECT titulo, director, genero, calificacion, anio_estreno
FROM peliculas_alejandro
ORDER BY anio_estreno DESC
```
Mostrar la película con mayor calificación.
```sql
SELECT titulo, director, genero, calificacion
FROM peliculas_alejandro
ORDER BY calificacion DESC
LIMIT 1
```
Calcular la duración promedio de las películas.
```sql
SELECT AVG(duracion_minutos) AS 'Duración promedio'
FROM peliculas_alejandro
```
Contar cuántas películas existen por género.
```sql
SELECT genero, COUNT(pelicula_id) AS Peliculas
FROM peliculas_alejandro
GROUP BY genero
```
Buscar películas cuyo título contenga una palabra utilizando LIKE.
```sql
SELECT titulo, director, calificacion, genero
FROM peliculas_alejandro
WHERE titulo like "%the%"
```
Cambiar una película de disponible a no disponible utilizando UPDATE.
```sql
UPDATE peliculas_alejandro
SET disponible = FALSE
WHERE titulo = 'The Final Empire';
```
