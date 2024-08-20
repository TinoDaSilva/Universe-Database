# Universe-Database
This project sets up a PostgreSQL Database for Celestial Bodies. The database schema includes tables for galaxies, stars, planets, moons, and asteroids. Each table captures various attributes that describe these celestial objects, and relationships are established between them using foreign keys.

## **Author**
Tino Da Silva

## Database Schema

The database consists of the following tables:

1. **Galaxy**
    - `galaxy_id`: Primary key.
    - `name`: Name of the galaxy.
    - `age_in_millions_of_years`: Age of the galaxy in millions of years.
    - `diameter_in_light_years`: Diameter of the galaxy in light years.
    - `type`: Type of the galaxy (e.g., Spiral, Elliptical).
  
2. **Star**
    - `star_id`: Primary key.
    - `name`: Name of the star.
    - `galaxy_id`: Foreign key referencing the `galaxy_id` column in the `galaxy` table.
    - `mass_in_solar_masses`: Mass of the star in solar masses.
    - `age_in_millions_of_years`: Age of the star in millions of years.
    - `type`: Type of the star (e.g., Red Dwarf, White Dwarf).

3. **Planet**
    - `planet_id`: Primary key.
    - `name`: Name of the planet.
    - `star_id`: Foreign key referencing the `star_id` column in the `star` table.
    - `has_life`: Boolean indicating if the planet has life.
    - `age_in_millions_of_years`: Age of the planet in millions of years.
  
4. **Moon**
    - `moon_id`: Primary key.
    - `name`: Name of the moon.
    - `planet_id`: Foreign key referencing the `planet_id` column in the `planet` table.
    - `diameter_in_km`: Diameter of the moon in kilometers.
  
5. **Asteroid**
    - `asteroid_id`: Primary key.
    - `name`: Name of the asteroid.
    - `planet_id`: Foreign key referencing the `planet_id` column in the `planet` table.
    - `mass`: Mass of the asteroid (numeric with precision).
    - `composition`: Composition of the asteroid.
