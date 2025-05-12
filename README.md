# universe



CREATE TABLE galaxy (
    galaxy_id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    size_kly INT NOT NULL,
    num_stars_billion INT,
    has_black_hole BOOLEAN NOT NULL,
    description TEXT
);


CREATE TABLE star (
    star_id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    galaxy_id INT REFERENCES galaxy(galaxy_id) NOT NULL,
    mass_solar NUMERIC(5,2) NOT NULL,
    luminosity INT,
    is_binary BOOLEAN NOT NULL
);


CREATE TABLE planet (
    planet_id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    star_id INT REFERENCES star(star_id) NOT NULL,
    distance_au INT NOT NULL,
    mass_earth INT,
    has_life BOOLEAN NOT NULL
);


CREATE TABLE moon (
    moon_id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    planet_id INT REFERENCES planet(planet_id) NOT NULL,
    diameter_km INT NOT NULL,
    has_atmosphere BOOLEAN NOT NULL,
    composition TEXT
);


CREATE TABLE nebula (
    nebula_id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    galaxy_id INT REFERENCES galaxy(galaxy_id) NOT NULL,
    size_ly INT NOT NULL,
    is_emission BOOLEAN NOT NULL,
    description TEXT
);


INSERT INTO galaxy (name, size_kly, num_stars_billion, has_black_hole, description) VALUES
('Milky Way', 100, 200, true, 'Our galaxy'),
('Andromeda', 110, 1000, true, 'Nearest spiral galaxy'),
('Triangulum', 60, 40, false, 'Third-largest in Local Group'),
('Messier 87', 120, 1000, true, 'Elliptical galaxy with supermassive black hole'),
('Sombrero', 50, 100, true, 'Distinctive dust lane'),
('Large Magellanic', 14, 30, false, 'Satellite galaxy of Milky Way');


INSERT INTO star (name, galaxy_id, mass_solar, luminosity, is_binary) VALUES
('Sun', 1, 1.00, 1, false),
('Sirius', 1, 2.02, 25, true),
('Betelgeuse', 1, 15.00, 90000, false),
('Vega', 1, 2.10, 40, false),
('Proxima Centauri', 1, 0.12, 0, true),
('Alpha Andromedae', 2, 3.80, 100, true);


INSERT INTO planet (name, star_id, distance_au, mass_earth, has_life) VALUES
('Earth', 1, 1, 1, true),
('Mars', 1, 2, 0, false),
('Jupiter', 1, 5, 318, false),
('Venus', 1, 1, 1, false),
('Sirius B-1', 2, 3, 2, false),
('Sirius B-2', 2, 4, 3, false),
('Betelgeuse I', 3, 6, 500, false),
('Betelgeuse II', 3, 8, 400, false),
('Vega Prime', 4, 2, 2, false),
('Vega Secundus', 4, 3, 1, false),
('Proxima b', 5, 0, 1, false),
('Alpha And I', 6, 4, 3, false);


INSERT INTO moon (name, planet_id, diameter_km, has_atmosphere, composition) VALUES
('Moon', 1, 3474, false, 'Rocky'),
('Phobos', 2, 22, false, 'Rocky'),
('Deimos', 2, 12, false, 'Rocky'),
('Io', 3, 3643, true, 'Volcanic'),
('Europa', 3, 3122, true, 'Icy'),
('Ganymede', 3, 5268, true, 'Icy'),
('Callisto', 3, 4821, true, 'Icy'),
('Titan', 3, 5150, true, 'Icy/Rocky'),
('Venus I', 4, 1000, false, 'Rocky'),
('Venus II', 4, 800, false, 'Rocky'),
('Sirius B1-M1', 5, 1500, false, 'Rocky'),
('Sirius B1-M2', 5, 1200, false, 'Rocky'),
('Sirius B2-M1', 6, 2000, false, 'Rocky'),
('Betel I-M1', 7, 3000, true, 'Icy'),
('Betel I-M2', 7, 2500, true, 'Icy'),
('Betel II-M1', 8, 2800, true, 'Icy'),
('Vega P-M1', 9, 900, false, 'Rocky'),
('Vega S-M1', 10, 1100, false, 'Rocky'),
('Proxima b-M1', 11, 700, false, 'Rocky'),
('Alpha And I-M1', 12, 1800, true, 'Icy');


INSERT INTO nebula (name, galaxy_id, size_ly, is_emission, description) VALUES
('Orion Nebula', 1, 24, true, 'Star-forming region'),
('Crab Nebula', 1, 11, false, 'Supernova remnant'),
('Eagle Nebula', 1, 70, true, 'Contains Pillars of Creation');
