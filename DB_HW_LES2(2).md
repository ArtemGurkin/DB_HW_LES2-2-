create table if not exists Genre (
Genre_ID SERIAL primary key,
Genre_name VARCHAR(60) unique not null
);

create table if not exists Artist (
Artist_ID SERIAL primary key,
Artist_name VARCHAR(60) unique not null
);

create table if not exists Album (
Album_ID SERIAL primary key,
Album_name VARCHAR(60) not null,
Album_year DATE not null
);

create table if not exists Collection (
Collection_ID SERIAL primary key,
Collection_name VARCHAR(60) not null,
Collection_year DATE not null
);

create table Track (
Track_ID SERIAL primary key,
Track_name VARCHAR(60) unique not null,
Track_duration INTEGER not null,
Album_ID INTEGER references Album(Album_ID)
);

create table Collection_Track (
Collection_ID INTEGER references Collection(Collection_ID),
Track_ID INTEGER references Track(Track_ID),
constraint CT primary key (Collection_ID, Track_ID)
);

create table if not exists Artist+Genre (
Artist_ID INTEGER references Artist(Artist_ID),
Genre_ID INTEGER references Genre(Genre_ID),
constraint AG primary key (Artist_ID, Genre_ID)
);

create table if not exists Album+Artist (
Album_ID INTEGER references Album(Album_ID),
Artist_ID INTEGER references Artist(Artist_ID),
constraint AA primary key (Artist_ID, Album_ID)
);