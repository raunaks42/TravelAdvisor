# TravelAdvisor
Helps you figure out the fastest and most efficient ways of getting around the city using public transport

by 
Raunak Sengupta     (PES1201700072)
Aprameya Kulkarni   (PES1201701583)
Dev Bhartra         (PES1201700186)

Execution Procedure:

The commands to create the database are found in the file createstatements.txt in the folder Phase 2.
Data can then be inserted to the database by running the commands containing insert statements found in the insertstatements.txt file, also in the folder Phase 2. Please note that due to the large size of the data being worked with, we have used 'copy' statemnts to import the data which is stored in the csv files, which can be found in the folder - Data. 
Then basic queries can be executed on the data by running the queries found in the file basicquries.txt, which is located in the folder, Phase 2.

Create Statements:

 Database: transport

-- DROP DATABASE transport;

CREATE DATABASE transport
    WITH 
    OWNER = postgres
    ENCODING = 'UTF8'
    LC_COLLATE = 'Kannada_India.utf8'
    LC_CTYPE = 'Kannada_India.utf8'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1;
	
	
	
	
CREATE TABLE public.bookings
(
    bookingid smallint NOT NULL DEFAULT nextval('bookings_bookingid_seq'::regclass),
    userid integer NOT NULL,
    to_stn character varying(50) COLLATE pg_catalog."default",
    from_stn character varying(50) COLLATE pg_catalog."default",
    type character varying(20) COLLATE pg_catalog."default",
    cost smallint,
    CONSTRAINT bookings_pkey PRIMARY KEY (bookingid),
    CONSTRAINT bookings_userid_key UNIQUE (userid)

)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.bookings
    OWNER to postgres;
	
	
	
	
	
	
CREATE TABLE public.bus_routes
(
)

WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.bus_routes
    OWNER to postgres;
	
	
	
	
	
	
CREATE TABLE public.buses
(
    busno character varying(20) COLLATE pg_catalog."default" NOT NULL DEFAULT nextval('buses_busno_seq'::regclass),
    dep_stn character varying(50) COLLATE pg_catalog."default" NOT NULL,
    des_stn character varying(50) COLLATE pg_catalog."default" NOT NULL,
    total_stops smallint NOT NULL,
    distance numeric NOT NULL,
    j_time numeric NOT NULL,
    type character varying(20) COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT buses_pkey PRIMARY KEY (busno),
    CONSTRAINT buses_total_stops_check CHECK (total_stops > 0),
    CONSTRAINT buses_distance_check CHECK (distance > 0::numeric)
)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.buses
    OWNER to postgres;
	
	
	
	
CREATE TABLE public.metro
(
    dep_stn character varying(20) COLLATE pg_catalog."default",
    des_stn character varying(20) COLLATE pg_catalog."default",
    metro_type character varying(20) COLLATE pg_catalog."default"
)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.metro
    OWNER to postgres;
	
	
	
	
	
CREATE TABLE public.stations
(
    station_name character varying(50) COLLATE pg_catalog."default" NOT NULL,
    station_code character varying(20) COLLATE pg_catalog."default" NOT NULL,
    type character varying(20) COLLATE pg_catalog."default"
)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.stations
    OWNER to postgres;
	
	
	
	
CREATE TABLE public.users
(
    userid integer NOT NULL DEFAULT nextval('users_userid_seq'::regclass),
    buspass character varying(20) COLLATE pg_catalog."default",
    fname character varying(20) COLLATE pg_catalog."default" NOT NULL,
    lname character varying(20) COLLATE pg_catalog."default",
    home_stn character varying(50) COLLATE pg_catalog."default" NOT NULL,
    num_bookings integer,
    metrocard character varying(20) COLLATE pg_catalog."default",
    CONSTRAINT users_pkey PRIMARY KEY (userid)
)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.users
OWNER to postgres;
