# Sistema de Gestión de una Liga Infantil de Fútbol

## 1. Introducción

El presente proyecto tiene como finalidad desarrollar un sistema de
información para la gestión y administración de una liga infantil de
fútbol mediante una aplicación web que permita organizar y consultar la
información relacionada con los equipos participantes, jugadores,
categorías, partidos, sedes y árbitros.

La organización de una liga deportiva requiere llevar un control
adecuado de los equipos inscritos, sus integrantes, las categorías
correspondientes y la programación de los encuentros. Cuando esta
información se administra de manera manual o mediante diferentes medios,
pueden presentarse problemas como duplicidad de datos, pérdida de
información y dificultades para consultar los resultados.

Por esta razón, se propone el diseño de una base de datos que permita
almacenar y relacionar toda la información necesaria para el
funcionamiento de la liga. El sistema contempla el registro de
categorías, equipos y jugadores, así como la administración de partidos,
asignación de árbitros, sedes, alineaciones y estadísticas individuales
de los jugadores.

Con este proyecto se busca facilitar la administración de la liga
infantil de fútbol, mejorar la organización de los encuentros deportivos
y proporcionar un medio de consulta eficiente, confiable y ordenado para
los usuarios.

------------------------------------------------------------------------

## 2. Casos de uso (UML)

### 2.1 Actores del sistema

-   **Administrador de la liga:** Responsable de administrar la
    información general del sistema, registrar categorías, equipos,
    jugadores y programar los partidos.
-   **Entrenador:** Puede consultar la información de su equipo y sus
    jugadores, así como revisar los partidos programados y las
    alineaciones.
-   **Árbitro:** Participa en los encuentros deportivos asignados y
    proporciona la información correspondiente a los resultados.
-   **Usuario / Consultor:** Puede consultar información general de la
    liga, como equipos participantes, partidos, fechas, sedes y
    resultados.

### 2.2 Descripción de los casos de uso

  -----------------------------------------------------------------------
  Caso de uso             Descripción             Actor principal
  ----------------------- ----------------------- -----------------------
  Gestionar categorías    Registrar, consultar,   Administrador
                          modificar y eliminar    
                          categorías de la liga.  

  Gestionar equipos       Registrar equipos,      Administrador
                          asignar entrenadores y  
                          relacionarlos con una   
                          categoría.              

  Gestionar jugadores     Registrar jugadores,    Administrador
                          asignarlos a equipos y  
                          administrar sus datos.  

  Gestionar sedes         Registrar y consultar   Administrador
                          los lugares donde se    
                          realizarán los          
                          partidos.               

  Gestionar árbitros      Registrar y consultar   Administrador
                          los árbitros            
                          disponibles para los    
                          encuentros.             

  Programar partidos      Establecer fecha, hora, Administrador
                          sede, equipo local y    
                          equipo visitante.       

  Registrar alineaciones  Seleccionar los         Administrador /
                          jugadores que           Entrenador
                          participarán en un      
                          partido e indicar si    
                          son titulares.          

  Registrar resultados    Registrar los goles del Administrador / Árbitro
                          equipo local y          
                          visitante.              

  Registrar estadísticas  Registrar goles,        Administrador / Árbitro
                          asistencias y tarjetas  
                          de cada jugador por     
                          partido.                

  Consultar partidos      Visualizar los          Todos los usuarios
                          encuentros programados  
                          y sus resultados.       

  Consultar equipos y     Consultar los equipos   Todos los usuarios
  jugadores               participantes y sus     
                          integrantes.            

  Consultar estadísticas  Consultar las           Todos los usuarios
                          estadísticas            
                          individuales y          
                          acumuladas de los       
                          jugadores.              
  -----------------------------------------------------------------------

### 2.3 Diagrama de casos de uso

``` mermaid
flowchart TB
    A["Administrador de la liga"]
    E["Entrenador"]
    R["Árbitro"]
    U["Usuario / Consultor"]

    subgraph S["Sistema de Gestión de Liga Infantil de Fútbol"]
        UC1(["Gestionar categorías"])
        UC2(["Gestionar equipos"])
        UC3(["Gestionar jugadores"])
        UC4(["Gestionar sedes"])
        UC5(["Gestionar árbitros"])
        UC6(["Programar partidos"])
        UC7(["Registrar alineaciones"])
        UC8(["Registrar resultados"])
        UC9(["Registrar estadísticas"])
        UC10(["Consultar partidos"])
        UC11(["Consultar equipos y jugadores"])
        UC12(["Consultar estadísticas"])
    end

    A --- UC1
    A --- UC2
    A --- UC3
    A --- UC4
    A --- UC5
    A --- UC6
    A --- UC7
    A --- UC8
    A --- UC9

    E --- UC10
    E --- UC11
    E --- UC7
    E --- UC12

    R --- UC8
    R --- UC9

    U --- UC10
    U --- UC11
    U --- UC12
```

------------------------------------------------------------------------

## 3. Modelo entidad-relación

### 3.1 Descripción de las entidades

El modelo entidad-relación está compuesto por **ocho entidades
principales** que permiten representar la información necesaria para
administrar la liga infantil de fútbol.

**1. Categoría**

  Atributo       Tipo de dato   Clave
  -------------- -------------- -------
  id_categoria   INT            PK
  nombre         VARCHAR(100)   
  edades         VARCHAR(50)    

**2. Equipo**

  Atributo       Tipo de dato   Clave
  -------------- -------------- -------
  id_equipo      INT            PK
  nombre         VARCHAR(120)   
  tecnico        VARCHAR(120)   
  categoria_id   INT            FK

**3. Jugadores**

  Atributo     Tipo de dato   Clave
  ------------ -------------- -------
  id_jugador   INT            PK
  nombre       VARCHAR(150)   
  edad         INT            
  numero       INT            
  posicion     VARCHAR(50)    
  id_equipo    INT            FK

**4. Sede**

  Atributo    Tipo de dato   Clave
  ----------- -------------- -------
  id_sede     INT            PK
  nombre      VARCHAR(120)   
  direccion   VARCHAR(250)   

**5. Árbitro**

  Atributo     Tipo de dato   Clave
  ------------ -------------- -------
  id_arbitro   INT            PK
  nombre       VARCHAR(150)   
  licencia     VARCHAR(80)    

**6. Alineación**

  Atributo        Tipo de dato   Clave
  --------------- -------------- -------
  id_alineacion   INT            PK
  id_partido      INT            FK
  id_jugador      INT            FK
  titular         BOOLEAN        

**7. Partido**

  Atributo           Tipo de dato   Clave
  ------------------ -------------- -------
  id_partido         INT            PK
  fecha              DATE           
  hora               TIME           
  id_sede            INT            FK
  gol_visitante      INT            
  id_arbitro         INT            FK
  gol_local          INT            
  equipo_local       INT            FK
  equipo_visitante   INT            FK

**8. Estadísticas del jugador**

  Atributo             Tipo de dato   Clave
  -------------------- -------------- -------
  id_estadistica       INT            PK
  id_jugador           INT            FK
  id_partido           INT            FK
  goles                INT            
  tarjetas_amarillas   INT            
  tarjetas_rojas       INT            
  asistencias          INT            

Esta tabla permite registrar el rendimiento individual de cada jugador
en cada partido. Los campos de goles, tarjetas amarillas, tarjetas rojas
y asistencias comienzan en cero y se actualizan conforme se registran
los acontecimientos del encuentro. La combinación de id_jugador e
id_partido debe ser única para evitar registrar dos veces las
estadísticas del mismo jugador en un mismo partido.

### 3.2 Diagrama entidad-relación

``` mermaid
erDiagram
    CATEGORIA ||--o{ EQUIPO : clasifica
    EQUIPO ||--o{ JUGADORES : integra

    EQUIPO ||--o{ PARTIDO : "juega como local"
    EQUIPO ||--o{ PARTIDO : "juega como visitante"

    SEDE ||--o{ PARTIDO : alberga
    ARBITRO ||--o{ PARTIDO : dirige

    PARTIDO ||--o{ ALINEACION : contiene
    JUGADORES ||--o{ ALINEACION : participa

    JUGADORES ||--o{ ESTADISTICAS_JUGADOR : registra
    PARTIDO ||--o{ ESTADISTICAS_JUGADOR : genera

    CATEGORIA {
        int id_categoria PK
        string nombre
        string edades
    }

    EQUIPO {
        int id_equipo PK
        string nombre
        string tecnico
        int categoria_id FK
    }

    JUGADORES {
        int id_jugador PK
        string nombre
        int edad
        int numero
        string posicion
        int id_equipo FK
    }

    SEDE {
        int id_sede PK
        string nombre
        string direccion
    }

    ARBITRO {
        int id_arbitro PK
        string nombre
        string licencia
    }

    ALINEACION {
        int id_alineacion PK
        int id_partido FK
        int id_jugador FK
        boolean titular
    }

    PARTIDO {
        int id_partido PK
        date fecha
        time hora
        int id_sede FK
        int gol_visitante
        int id_arbitro FK
        int gol_local
        int equipo_local FK
        int equipo_visitante FK
    }

    ESTADISTICAS_JUGADOR {
        int id_estadistica PK
        int id_jugador FK
        int id_partido FK
        int goles
        int tarjetas_amarillas
        int tarjetas_rojas
        int asistencias
    }
```

### 3.3 Descripción de las relaciones

-   **Categoría - Equipo (1:N):** Una categoría puede tener varios
    equipos registrados, pero cada equipo pertenece a una sola
    categoría.
-   **Equipo - Jugadores (1:N):** Un equipo puede estar integrado por
    varios jugadores, pero cada jugador pertenece a un equipo.
-   **Equipo - Partido como local (1:N):** Un equipo puede participar en
    diferentes partidos como equipo local.
-   **Equipo - Partido como visitante (1:N):** Un equipo puede
    participar en diferentes partidos como equipo visitante.
-   **Sede - Partido (1:N):** Una sede puede albergar diferentes
    partidos, pero cada partido se realiza en una sola sede.
-   **Árbitro - Partido (1:N):** Un árbitro puede dirigir varios
    partidos, pero cada partido tiene asignado un árbitro.
-   **Partido - Alineación (1:N):** Un partido puede tener varios
    registros de alineación correspondientes a los jugadores
    participantes.
-   **Jugador - Alineación (1:N):** Un jugador puede aparecer en
    diferentes alineaciones a lo largo de distintos partidos.
-   **Jugador - Estadísticas del jugador (1:N):** Un jugador puede tener
    registros estadísticos en diferentes partidos. Cada registro
    pertenece a un solo jugador.
-   **Partido - Estadísticas del jugador (1:N):** Un partido puede
    generar registros estadísticos de varios jugadores. Cada registro
    corresponde a un solo partido.

------------------------------------------------------------------------

## 4. Creación de la base de datos en PostgreSQL

El siguiente código SQL permite crear las ocho tablas del modelo,
establecer sus llaves primarias y foráneas y agregar restricciones para
mantener la integridad de la información.

``` sql
-- Crear la base de datos
CREATE DATABASE "LigaFutbol";

-- Conectarse a LigaFutbol antes de ejecutar
-- las siguientes instrucciones.

-- 1. TABLA CATEGORIA
CREATE TABLE categoria (
    id_categoria INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL UNIQUE,
    edades VARCHAR(50) NOT NULL
);

-- 2. TABLA EQUIPO
CREATE TABLE equipo (
    id_equipo INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nombre VARCHAR(120) NOT NULL,
    tecnico VARCHAR(120) NOT NULL,
    categoria_id INTEGER NOT NULL,
    CONSTRAINT fk_equipo_categoria
        FOREIGN KEY (categoria_id)
        REFERENCES categoria(id_categoria)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,
    CONSTRAINT uq_equipo_categoria
        UNIQUE (nombre, categoria_id)
);

-- 3. TABLA JUGADORES
CREATE TABLE jugadores (
    id_jugador INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nombre VARCHAR(150) NOT NULL,
    edad INTEGER NOT NULL CHECK (edad BETWEEN 3 AND 18),
    numero INTEGER NOT NULL CHECK (numero BETWEEN 0 AND 99),
    posicion VARCHAR(50),
    id_equipo INTEGER NOT NULL,
    CONSTRAINT fk_jugador_equipo
        FOREIGN KEY (id_equipo)
        REFERENCES equipo(id_equipo)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,
    CONSTRAINT uq_numero_equipo
        UNIQUE (id_equipo, numero)
);

-- 4. TABLA SEDE
CREATE TABLE sede (
    id_sede INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nombre VARCHAR(120) NOT NULL UNIQUE,
    direccion VARCHAR(250) NOT NULL
);

-- 5. TABLA ARBITRO
CREATE TABLE arbitro (
    id_arbitro INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nombre VARCHAR(150) NOT NULL,
    licencia VARCHAR(80) NOT NULL UNIQUE
);

-- 6. TABLA PARTIDO
CREATE TABLE partido (
    id_partido INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    fecha DATE NOT NULL,
    hora TIME NOT NULL,
    id_sede INTEGER NOT NULL,
    gol_visitante INTEGER CHECK (gol_visitante >= 0),
    id_arbitro INTEGER NOT NULL,
    gol_local INTEGER CHECK (gol_local >= 0),
    equipo_local INTEGER NOT NULL,
    equipo_visitante INTEGER NOT NULL,

    CONSTRAINT fk_partido_sede
        FOREIGN KEY (id_sede)
        REFERENCES sede(id_sede)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,

    CONSTRAINT fk_partido_arbitro
        FOREIGN KEY (id_arbitro)
        REFERENCES arbitro(id_arbitro)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,

    CONSTRAINT fk_partido_local
        FOREIGN KEY (equipo_local)
        REFERENCES equipo(id_equipo)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,

    CONSTRAINT fk_partido_visitante
        FOREIGN KEY (equipo_visitante)
        REFERENCES equipo(id_equipo)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,

    CONSTRAINT chk_equipos_diferentes
        CHECK (equipo_local <> equipo_visitante)
);

-- 7. TABLA ALINEACION
CREATE TABLE alineacion (
    id_alineacion INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    id_partido INTEGER NOT NULL,
    id_jugador INTEGER NOT NULL,
    titular BOOLEAN NOT NULL DEFAULT FALSE,

    CONSTRAINT fk_alineacion_partido
        FOREIGN KEY (id_partido)
        REFERENCES partido(id_partido)
        ON UPDATE CASCADE
        ON DELETE CASCADE,

    CONSTRAINT fk_alineacion_jugador
        FOREIGN KEY (id_jugador)
        REFERENCES jugadores(id_jugador)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,

    CONSTRAINT uq_jugador_partido
        UNIQUE (id_partido, id_jugador)
);

-- 8. TABLA ESTADISTICAS_JUGADOR
CREATE TABLE estadisticas_jugador (
    id_estadistica INTEGER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    id_jugador INTEGER NOT NULL,
    id_partido INTEGER NOT NULL,
    goles INTEGER NOT NULL DEFAULT 0 CHECK (goles >= 0),
    tarjetas_amarillas INTEGER NOT NULL DEFAULT 0
        CHECK (tarjetas_amarillas >= 0),
    tarjetas_rojas INTEGER NOT NULL DEFAULT 0
        CHECK (tarjetas_rojas >= 0),
    asistencias INTEGER NOT NULL DEFAULT 0
        CHECK (asistencias >= 0),

    CONSTRAINT fk_estadistica_jugador
        FOREIGN KEY (id_jugador)
        REFERENCES jugadores(id_jugador)
        ON UPDATE CASCADE
        ON DELETE RESTRICT,

    CONSTRAINT fk_estadistica_partido
        FOREIGN KEY (id_partido)
        REFERENCES partido(id_partido)
        ON UPDATE CASCADE
        ON DELETE CASCADE,

    CONSTRAINT uq_estadistica_jugador_partido
        UNIQUE (id_jugador, id_partido)
);

-- INDICES PARA APOYAR LAS CONSULTAS
CREATE INDEX idx_equipo_categoria
    ON equipo(categoria_id);

CREATE INDEX idx_jugadores_equipo
    ON jugadores(id_equipo);

CREATE INDEX idx_partido_fecha
    ON partido(fecha);

CREATE INDEX idx_partido_local
    ON partido(equipo_local);

CREATE INDEX idx_partido_visitante
    ON partido(equipo_visitante);

CREATE INDEX idx_alineacion_partido
    ON alineacion(id_partido);

CREATE INDEX idx_alineacion_jugador
    ON alineacion(id_jugador);

CREATE INDEX idx_estadisticas_jugador
    ON estadisticas_jugador(id_jugador);

CREATE INDEX idx_estadisticas_partido
    ON estadisticas_jugador(id_partido);
```

### 4.1 Ejemplo para registrar estadísticas

El siguiente ejemplo muestra cómo registrar las estadísticas de un
jugador en un partido. Los identificadores deben corresponder a
jugadores y partidos que ya existan en la base de datos.

``` sql
INSERT INTO estadisticas_jugador
    (id_jugador, id_partido, goles,
     tarjetas_amarillas, tarjetas_rojas, asistencias)
VALUES
    (1, 1, 2, 0, 0, 1),
    (2, 1, 0, 1, 0, 0),
    (3, 1, 1, 0, 0, 2);
```

### 4.2 Consulta de estadísticas acumuladas por jugador

Esta consulta suma las estadísticas registradas en los distintos
partidos y permite identificar a los jugadores con más goles.

``` sql
SELECT
    j.id_jugador,
    j.nombre AS jugador,
    e.nombre AS equipo,
    COALESCE(SUM(est.goles), 0) AS total_goles,
    COALESCE(SUM(est.tarjetas_amarillas), 0) AS total_amarillas,
    COALESCE(SUM(est.tarjetas_rojas), 0) AS total_rojas,
    COALESCE(SUM(est.asistencias), 0) AS total_asistencias
FROM jugadores j
INNER JOIN equipo e
    ON j.id_equipo = e.id_equipo
LEFT JOIN estadisticas_jugador est
    ON j.id_jugador = est.id_jugador
GROUP BY
    j.id_jugador,
    j.nombre,
    e.nombre
ORDER BY total_goles DESC, j.nombre;
```

