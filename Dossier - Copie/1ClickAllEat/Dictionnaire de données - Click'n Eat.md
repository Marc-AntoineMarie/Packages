| Table       | Champ            | Type     | Taille | Description                      | Contrainte         |
| ----------- | ---------------- | -------- | ------ | -------------------------------- | ------------------ |
| USERS       | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | name             | VARCHAR  | 255    | Nom de l'utilisateur             | NOT NULL           |
|             | email            | VARCHAR  | 255    | Adresse email                    | UNIQUE, NOT NULL   |
|             | password         | VARCHAR  | 255    | Mot de passe hashé               | NOT NULL           |
|             | role             | ENUM     | -      | Role (admin,restaurateur,client) | NOT NULL           |
| RESTAURANTS | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | name             | VARCHAR  | 255    | Nom du restaurant                | NOT NULL           |
|             | description      | TEXT     | -      | Description                      | NULL               |
|             | address          | VARCHAR  | 255    | Adresse                          | NOT NULL           |
|             | phone            | VARCHAR  | 20     | Téléphone                        | NOT NULL           |
|             | opening_hours    | JSON     | -      | Horaires d'ouverture             | NOT NULL           |
|             | avg_rating       | DECIMAL  | (3,2)  | Note moyenne                     | DEFAULT 0          |
|             | ratings_count    | INTEGER  | -      | Nombre d'avis                    | DEFAULT 0          |
| TABLES      | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | number           | INTEGER  | -      | Numéro de la table               | NOT NULL           |
|             | capacity         | INTEGER  | -      | Capacité en personnes            | NOT NULL           |
| RESERVATION | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | reservation_time | DATETIME | -      | Date et heure                    | NOT NULL           |
|             | guests_count     | INTEGER  | -      | Nombre de convives               | NOT NULL           |
|             | status           | VARCHAR  | 20     | État de la réservation           | NOT NULL           |
|             | notes            | TEXT     | -      | Notes spéciales                  | NULL               |
| CATEGORIES  | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | name             | VARCHAR  | 255    | Nom de la catégorie              | NOT NULL           |
|             | description      | TEXT     | -      | Description                      | NULL               |
| ITEMS       | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | name             | VARCHAR  | 255    | Nom du plat                      | NOT NULL           |
|             | description      | TEXT     | -      | Description                      | NULL               |
|             | price            | DECIMAL  | (10,2) | Prix                             | NOT NULL           |
| RATINGS     | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | rating           | INTEGER  | -      | Note (1-5)                       | NOT NULL           |
|             | comment          | TEXT     | -      | Commentaire                      | NULL               |
| CART_ITEMS  | id               | BIGINT   | -      | Identifiant unique               | PK, Auto_increment |
|             | guests_count     | INTEGER  | -      | Nombre de convives               | NOT NULL           |
|             | reservation_time | DATETIME | -      | Date et heure                    | NOT NULL           |
|             | notes            | TEXT     | -      | Notes spéciales                  | NULL               |
|             | total_price      | DECIMAL  | (10,2) | Prix total                       | NOT NULL           |
|             | selected_items   | JSON     | -      | Items sélectionnés               | NULL               |
