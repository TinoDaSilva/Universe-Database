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

--
-- PostgreSQL database dump
--

-- Dumped from database version 12.17 (Ubuntu 12.17-1.pgdg22.04+1)
-- Dumped by pg_dump version 12.17 (Ubuntu 12.17-1.pgdg22.04+1)

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

DROP DATABASE universe;
--
-- Name: universe; Type: DATABASE; Schema: -; Owner: freecodecamp
--

CREATE DATABASE universe WITH TEMPLATE = template0 ENCODING = 'UTF8' LC_COLLATE = 'C.UTF-8' LC_CTYPE = 'C.UTF-8';


ALTER DATABASE universe OWNER TO freecodecamp;

\connect universe

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

SET default_tablespace = '';

SET default_table_access_method = heap;

--
-- Name: asteroid; Type: TABLE; Schema: public; Owner: freecodecamp
--

CREATE TABLE public.asteroid (
    asteroid_id integer NOT NULL,
    name character varying(100) NOT NULL,
    diameter numeric(10,2) NOT NULL,
    mass numeric(30,2) NOT NULL,
    planet_id integer
);


ALTER TABLE public.asteroid OWNER TO freecodecamp;

--
-- Name: asteriod_asteroid_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
--

CREATE SEQUENCE public.asteriod_asteroid_id_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE public.asteriod_asteroid_id_seq OWNER TO freecodecamp;

--
-- Name: asteriod_asteroid_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
--

ALTER SEQUENCE public.asteriod_asteroid_id_seq OWNED BY public.asteroid.asteroid_id;


--
-- Name: galaxy; Type: TABLE; Schema: public; Owner: freecodecamp
--

CREATE TABLE public.galaxy (
    galaxy_id integer NOT NULL,
    name character varying(250),
    description text,
    age_in_millions_of_years integer NOT NULL,
    has_life boolean
);


ALTER TABLE public.galaxy OWNER TO freecodecamp;

--
-- Name: galaxy_galaxy_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
--

CREATE SEQUENCE public.galaxy_galaxy_id_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE public.galaxy_galaxy_id_seq OWNER TO freecodecamp;

--
-- Name: galaxy_galaxy_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
--

ALTER SEQUENCE public.galaxy_galaxy_id_seq OWNED BY public.galaxy.galaxy_id;


--
-- Name: moon; Type: TABLE; Schema: public; Owner: freecodecamp
--

CREATE TABLE public.moon (
    moon_id integer NOT NULL,
    name character varying(250),
    planet_id integer,
    age_in_millions_of_years integer NOT NULL,
    distance_from_earth numeric(10,2)
);


ALTER TABLE public.moon OWNER TO freecodecamp;

--
-- Name: moon_mood_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
--

CREATE SEQUENCE public.moon_mood_id_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE public.moon_mood_id_seq OWNER TO freecodecamp;

--
-- Name: moon_mood_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
--

ALTER SEQUENCE public.moon_mood_id_seq OWNED BY public.moon.moon_id;


--
-- Name: planet; Type: TABLE; Schema: public; Owner: freecodecamp
--

CREATE TABLE public.planet (
    planet_id integer NOT NULL,
    name character varying(250),
    star_id integer,
    has_life boolean,
    age_in_millions_of_years integer NOT NULL
);


ALTER TABLE public.planet OWNER TO freecodecamp;

--
-- Name: planet_planet_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
--

CREATE SEQUENCE public.planet_planet_id_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE public.planet_planet_id_seq OWNER TO freecodecamp;

--
-- Name: planet_planet_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
--

ALTER SEQUENCE public.planet_planet_id_seq OWNED BY public.planet.planet_id;


--
-- Name: star; Type: TABLE; Schema: public; Owner: freecodecamp
--

CREATE TABLE public.star (
    star_id integer NOT NULL,
    name character varying(250),
    galaxy_id integer,
    is_sepherical boolean,
    age_in_millions_of_years numeric(10,5) NOT NULL
);


ALTER TABLE public.star OWNER TO freecodecamp;

--
-- Name: star_star_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
--

CREATE SEQUENCE public.star_star_id_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE public.star_star_id_seq OWNER TO freecodecamp;

--
-- Name: star_star_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
--

ALTER SEQUENCE public.star_star_id_seq OWNED BY public.star.star_id;


--
-- Name: asteroid asteroid_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.asteroid ALTER COLUMN asteroid_id SET DEFAULT nextval('public.asteriod_asteroid_id_seq'::regclass);


--
-- Name: galaxy galaxy_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.galaxy ALTER COLUMN galaxy_id SET DEFAULT nextval('public.galaxy_galaxy_id_seq'::regclass);


--
-- Name: moon moon_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.moon ALTER COLUMN moon_id SET DEFAULT nextval('public.moon_mood_id_seq'::regclass);


--
-- Name: planet planet_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.planet ALTER COLUMN planet_id SET DEFAULT nextval('public.planet_planet_id_seq'::regclass);


--
-- Name: star star_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.star ALTER COLUMN star_id SET DEFAULT nextval('public.star_star_id_seq'::regclass);


--
-- Data for Name: asteroid; Type: TABLE DATA; Schema: public; Owner: freecodecamp
--

INSERT INTO public.asteroid VALUES (1, 'Ceres', 939.40, 93800000000000000.00, 1);
INSERT INTO public.asteroid VALUES (2, 'Pallas', 512.00, 21100000000000000.00, 1);
INSERT INTO public.asteroid VALUES (3, 'Vesta', 525.40, 25900000000000000.00, 2);
INSERT INTO public.asteroid VALUES (4, 'Hygiea', 434.00, 8670000000000000.00, 2);
INSERT INTO public.asteroid VALUES (5, 'Eros', 16.84, 669000000000000.00, 3);
INSERT INTO public.asteroid VALUES (6, 'Gaspra', 18.20, 250000000000000.00, 4);
INSERT INTO public.asteroid VALUES (7, 'Ida', 31.40, 420000000000000.00, 4);
INSERT INTO public.asteroid VALUES (8, 'Bennu', 0.49, 73300000000.00, 5);
INSERT INTO public.asteroid VALUES (9, 'Itokawa', 0.54, 35100000000.00, 6);
INSERT INTO public.asteroid VALUES (10, 'Psyche', 226.00, 24100000000000000.00, 7);
INSERT INTO public.asteroid VALUES (11, 'Eunomia', 255.00, 31200000000000000.00, 8);
INSERT INTO public.asteroid VALUES (12, 'Juno', 233.90, 26700000000000000.00, 9);
INSERT INTO public.asteroid VALUES (13, 'Davida', 326.00, 30000000000000000.00, 10);
INSERT INTO public.asteroid VALUES (14, 'Interamnia', 306.00, 38000000000000000.00, 11);
INSERT INTO public.asteroid VALUES (15, 'Metis', 190.00, 3600000000000000.00, 11);
INSERT INTO public.asteroid VALUES (16, 'Amphitrite', 212.00, 11800000000000000.00, 12);
INSERT INTO public.asteroid VALUES (17, 'Hebe', 185.00, 12800000000000000.00, 12);
INSERT INTO public.asteroid VALUES (18, 'Iris', 200.00, 11900000000000000.00, 12);
INSERT INTO public.asteroid VALUES (19, 'Flora', 140.00, 4160000000000000.00, 10);
INSERT INTO public.asteroid VALUES (20, 'Psyche', 226.00, 24100000000000000.00, 6);


--
-- Data for Name: galaxy; Type: TABLE DATA; Schema: public; Owner: freecodecamp
--

INSERT INTO public.galaxy VALUES (1, 'Milky Way', 'Our home galaxy', 13600, true);
INSERT INTO public.galaxy VALUES (2, 'Andromeda', 'Nearest spiral galaxy', 10000, false);
INSERT INTO public.galaxy VALUES (3, 'Triangulum', 'Third largest in our group', 9500, false);
INSERT INTO public.galaxy VALUES (4, 'Whirlpool', 'Famous for its spiral structure', 3000, false);
INSERT INTO public.galaxy VALUES (5, 'Sombrero', 'A galaxy with a bright nucleus', 8900, false);
INSERT INTO public.galaxy VALUES (6, 'Messier 87', 'A giant elliptical galaxy', 13000, false);


--
-- Data for Name: moon; Type: TABLE DATA; Schema: public; Owner: freecodecamp
--

INSERT INTO public.moon VALUES (1, 'Moon', 1, 4500, 384400.00);
INSERT INTO public.moon VALUES (2, 'Phobos', 2, 4500, 9376.00);
INSERT INTO public.moon VALUES (3, 'Deimos', 2, 4500, 23463.00);
INSERT INTO public.moon VALUES (4, 'Europa', 3, 4500, 628.30);
INSERT INTO public.moon VALUES (5, 'Ganymede', 3, 4500, 1070.40);
INSERT INTO public.moon VALUES (6, 'Callisto', 4, 4500, 1882.00);
INSERT INTO public.moon VALUES (7, 'Io', 4, 4500, 621.30);
INSERT INTO public.moon VALUES (8, 'Titan', 5, 4500, 1221870.00);
INSERT INTO public.moon VALUES (9, 'Enceladus', 5, 4500, 1270.40);
INSERT INTO public.moon VALUES (10, 'Mimas', 6, 4500, 1850.00);
INSERT INTO public.moon VALUES (11, 'Triton', 7, 4500, 354759.00);
INSERT INTO public.moon VALUES (12, 'Charon', 8, 4500, 1960.00);
INSERT INTO public.moon VALUES (13, 'Oberon', 9, 4500, 582600.00);
INSERT INTO public.moon VALUES (14, 'Miranda', 9, 4500, 129390.00);
INSERT INTO public.moon VALUES (15, 'Ariel', 10, 4500, 190000.00);
INSERT INTO public.moon VALUES (16, 'Umbriel', 10, 4500, 265970.00);
INSERT INTO public.moon VALUES (17, 'Titania', 11, 4500, 435910.00);
INSERT INTO public.moon VALUES (18, 'Rhea', 11, 4500, 527040.00);
INSERT INTO public.moon VALUES (19, 'Iapetus', 12, 4500, 356080.00);
INSERT INTO public.moon VALUES (20, 'Dione', 12, 4500, 377410.00);


--
-- Data for Name: planet; Type: TABLE DATA; Schema: public; Owner: freecodecamp
--

INSERT INTO public.planet VALUES (1, 'Earth', 1, true, 4500);
INSERT INTO public.planet VALUES (2, 'Mars', 1, false, 4500);
INSERT INTO public.planet VALUES (3, 'Proxima Centauri b', 2, false, 4500);
INSERT INTO public.planet VALUES (4, 'Kepler-22b', 3, false, 4500);
INSERT INTO public.planet VALUES (5, 'HD 209458 b', 3, false, 4600);
INSERT INTO public.planet VALUES (6, 'Gliese 581g', 4, false, 4800);
INSERT INTO public.planet VALUES (7, 'Tau Ceti e', 4, false, 4900);
INSERT INTO public.planet VALUES (8, 'TRAPPIST-1d', 5, false, 4500);
INSERT INTO public.planet VALUES (9, '55 Cancri e', 5, false, 4100);
INSERT INTO public.planet VALUES (10, 'WASP-12b', 6, false, 3500);
INSERT INTO public.planet VALUES (11, 'HD 189733 b', 6, false, 3600);
INSERT INTO public.planet VALUES (12, 'GJ 1214 b', 6, false, 3700);


--
-- Data for Name: star; Type: TABLE DATA; Schema: public; Owner: freecodecamp
--

INSERT INTO public.star VALUES (1, 'Sun', 1, true, 4600.12345);
INSERT INTO public.star VALUES (2, 'Alpha Centauri', 2, true, 5500.54321);
INSERT INTO public.star VALUES (3, 'Betelgeuse', 3, false, 8000.98765);
INSERT INTO public.star VALUES (4, 'Sirius', 1, true, 3000.56789);
INSERT INTO public.star VALUES (5, 'Rigel', 4, true, 8700.12345);
INSERT INTO public.star VALUES (6, 'Vega', 5, false, 4500.67890);


--
-- Name: asteriod_asteroid_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
--

SELECT pg_catalog.setval('public.asteriod_asteroid_id_seq', 20, true);


--
-- Name: galaxy_galaxy_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
--

SELECT pg_catalog.setval('public.galaxy_galaxy_id_seq', 6, true);


--
-- Name: moon_mood_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
--

SELECT pg_catalog.setval('public.moon_mood_id_seq', 20, true);


--
-- Name: planet_planet_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
--

SELECT pg_catalog.setval('public.planet_planet_id_seq', 12, true);


--
-- Name: star_star_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
--

SELECT pg_catalog.setval('public.star_star_id_seq', 6, true);


--
-- Name: asteroid asteriod_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.asteroid
    ADD CONSTRAINT asteriod_pkey PRIMARY KEY (asteroid_id);


--
-- Name: asteroid asteroid_id_unique; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.asteroid
    ADD CONSTRAINT asteroid_id_unique UNIQUE (asteroid_id);


--
-- Name: galaxy galaxy_name; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.galaxy
    ADD CONSTRAINT galaxy_name UNIQUE (name);


--
-- Name: galaxy galaxy_name_unique; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.galaxy
    ADD CONSTRAINT galaxy_name_unique UNIQUE (galaxy_id, name);


--
-- Name: galaxy galaxy_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.galaxy
    ADD CONSTRAINT galaxy_pkey PRIMARY KEY (galaxy_id);


--
-- Name: moon moon_name; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.moon
    ADD CONSTRAINT moon_name UNIQUE (name);


--
-- Name: moon moon_name_unique; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.moon
    ADD CONSTRAINT moon_name_unique UNIQUE (moon_id, name);


--
-- Name: moon moon_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.moon
    ADD CONSTRAINT moon_pkey PRIMARY KEY (moon_id);


--
-- Name: planet planet_name; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.planet
    ADD CONSTRAINT planet_name UNIQUE (name);


--
-- Name: planet planet_name_unique; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.planet
    ADD CONSTRAINT planet_name_unique UNIQUE (planet_id, name);


--
-- Name: planet planet_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.planet
    ADD CONSTRAINT planet_pkey PRIMARY KEY (planet_id);


--
-- Name: star star_name; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.star
    ADD CONSTRAINT star_name UNIQUE (name);


--
-- Name: star star_name_unique; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.star
    ADD CONSTRAINT star_name_unique UNIQUE (star_id, name);


--
-- Name: star star_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.star
    ADD CONSTRAINT star_pkey PRIMARY KEY (star_id);


--
-- Name: star fk_galaxy; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.star
    ADD CONSTRAINT fk_galaxy FOREIGN KEY (galaxy_id) REFERENCES public.galaxy(galaxy_id);


--
-- Name: moon fk_planet; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.moon
    ADD CONSTRAINT fk_planet FOREIGN KEY (planet_id) REFERENCES public.planet(planet_id);


--
-- Name: asteroid fk_planet; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.asteroid
    ADD CONSTRAINT fk_planet FOREIGN KEY (planet_id) REFERENCES public.planet(planet_id) ON DELETE SET NULL;


--
-- Name: planet fk_star; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
--

ALTER TABLE ONLY public.planet
    ADD CONSTRAINT fk_star FOREIGN KEY (star_id) REFERENCES public.star(star_id);


--
-- PostgreSQL database dump complete
--


