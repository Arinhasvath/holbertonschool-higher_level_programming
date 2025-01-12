# Projet Badge
0%
Python - Mappage Objet-Relationnel
 Amateur
 Par : Guillaume
 Poids : 1
 Votre score sera mis à jour à mesure de votre progression.
Description
Avant de commencer...
Assurez-vous que votre serveur MySQL est en version 8.0 -> Comment installer MySQL 8.0 sur Ubuntu 20.04

Contexte
Dans ce projet, vous allez relier deux mondes incroyables : les Bases de Données et Python !

Dans la première partie, vous utiliserez le module MySQLdb pour vous connecter à une base de données MySQL et exécuter vos requêtes SQL.

Dans la deuxième partie, vous utiliserez le module SQLAlchemy (ne me demandez pas comment le prononcer...) un Mappage Objet-Relationnel (ORM).

La plus grande différence est : plus de requêtes SQL ! En effet, le but d'un ORM est d'abstraire le stockage de l'utilisation. Avec un ORM, votre principale préoccupation sera « Que puis-je faire avec mes objets » et non « Comment cet objet est stocké ? où ? quand ? ». Vous n'écrirez aucune requête SQL, seulement du code Python. Dernière chose, votre code ne dépendra plus du type de stockage. Vous pourrez changer votre stockage facilement sans réécrire votre projet entier.

Sans ORM :

conn = MySQLdb.connect(host="localhost", port=3306, user="root", passwd="root", db="my_db", charset="utf8")
cur = conn.cursor()
cur.execute("SELECT * FROM states ORDER BY id ASC") # ICI je dois connaître SQL pour récupérer tous les états de ma base de données
query_rows = cur.fetchall()
for row in query_rows:
    print(row)
cur.close()
conn.close()
Avec un ORM :

engine = create_engine('mysql+mysqldb://{}:{}@localhost/{}'.format("root", "root", "my_db"), pool_pre_ping=True)
Base.metadata.create_all(engine)

session = Session(engine)
for state in session.query(State).order_by(State.id).all(): # ICI : pas de requête SQL, seulement des objets !
    print("{}: {}".format(state.id, state.name))
session.close()
Voyez-vous la différence ? Cool, non ?

La plus grande difficulté avec les ORM est : la syntaxe !

En effet, tous en ont une syntaxe similaire, mais pas toujours. Veuillez lire les tutoriels et ne pas lire toute la documentation avant de commencer, sautez dessus si vous ne comprenez pas quelque chose.

Ressources
Lire ou regarder :

Object-relational mappers
documentation mysqlclient/MySQLdb (veuillez ne pas prêter attention à _mysql)
MySQLdb tutorial
SQLAlchemy tutorial
SQLAlchemy
mysqlclient/MySQLdb
Introduction to SQLAlchemy
Flask SQLAlchemy
10 common stumbling blocks for SQLAlchemy newbies
Python SQLAlchemy Cheatsheet
SQLAlchemy ORM Tutorial for Python Developers (Attention : Ce tutoriel est avec PostgreSQL, mais le concept de SQLAlchemy est le même avec MySQL)
SQLAlchemy Tutorial
Objectifs d'apprentissage
À la fin de ce projet, vous devriez être capable d'expliquer à quiconque, sans l'aide de Google :

Général
Comment se connecter à une base de données MySQL à partir d'un script Python
Comment SELECT des lignes dans une table MySQL à partir d'un script Python
Comment INSERT des lignes dans une table MySQL à partir d'un script Python
Ce que signifie ORM
Comment mapper une classe Python à une table MySQL
Exigences générales
Général
Editeurs autorisés : vi, vim, emacs
Tous vos fichiers seront interprétés/compilés sur Ubuntu 20.04 LTS en utilisant python3 (version 3.8.5)
Vos fichiers seront exécutés avec MySQLdb version 2.0.x
Vos fichiers seront exécutés avec SQLAlchemy version 1.4.x
Tous vos fichiers devraient se terminer par un nouveau ligne
La première ligne de tous vos fichiers devrait être exactement #!/usr/bin/python3
Un fichier README.md, à la racine du dossier du projet, est obligatoire
Votre code devrait utiliser le pycodestyle (version 2.7.*)
Tous vos fichiers doivent être exécutables
La longueur de vos fichiers sera testée en utilisant wc
Tous vos modules devraient avoir une documentation (python3 -c 'print(__import__("my_module").__doc__)')
Toutes vos classes devraient avoir une documentation (python3 -c 'print(__import__("my_module").MyClass.__doc__)')
Toutes vos fonctions (à l'intérieur et à l'extérieur d'une classe) devraient avoir une documentation (python3 -c 'print(__import__("my_module").my_function.__doc__)' et python3 -c 'print(__import__("my_module").MyClass.my_function.__doc__)')
Une documentation n'est pas un seul mot, c'est une vraie phrase expliquant le but du module, de la classe ou de la méthode (la longueur de celle-ci sera vérifiée)
Vous n'êtes pas autorisé à utiliser execute avec sqlalchemy
Plus d'informations
Installer MySQL 8.0 sur Ubuntu 20.04 LTS
$ sudo apt update
$ sudo apt install mysql-server
...
$ mysql --version
mysql  Ver 8.0.25-0ubuntu0.20.04.1 for Linux on x86_64 ((Ubuntu))
$
Se connecter à votre serveur MySQL :

$ sudo mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.25-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
mysql> quit
Bye
$
Installer le module MySQLdb en version 2.0.x
Pour installer MySQLdb, vous devez avoir MySQL installé.

$ sudo apt-get install python3-dev
$ sudo apt-get install libmysqlclient-dev
$ sudo apt-get install zlib1g-dev
$ sudo pip3 install mysqlclient
...
$ python3
>>> import MySQLdb
>>> MySQLdb.version_info 
(2, 0, 3, 'final', 0)
Installer le module SQLAlchemy en version 1.4.x
$ sudo pip3 install SQLAlchemy
...
$ python3
>>> import sqlalchemy
>>> sqlalchemy.__version__ 
'1.4.22'
De plus, vous pouvez avoir ce message d'avertissement :

/usr/local/lib/python3.4/dist-packages/sqlalchemy/engine/default.py:552: Warning: (1681, "'@@SESSION.GTID_EXECUTED' is deprecated and will be re
moved in a future release.")                                                                                                                    
  cursor.execute(statement, parameters)  
Vous pouvez l'ignorer.

Tâches
0. Obtenir tous les états
Obligatoire
Écrire un script qui liste tous les états de la base de données hbtn_0e_0_usa :

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données (aucune validation des arguments nécessaire)
Vous devez utiliser le module MySQLdb (import MySQLdb)
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Les résultats doivent être triés par ordre croissant selon states.id
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 0-select_states.sql
-- Créer la table states dans hbtn_0e_0_usa avec某些 données
CREATE DATABASE IF NOT EXISTS hbtn_0e_0_usa;
USE hbtn_0e_0_usa;
CREATE TABLE IF NOT EXISTS states ( 
    id INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id)
);
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

guillaume@ubuntu:~/$ cat 0-select_states.sql | mysql -uroot -p
Enter password: 
guillaume@ubuntu:~/$ ./0-select_states.py root root hbtn_0e_0_usa
(1, 'California')
(2, 'Arizona')
(3, 'Texas')
(4, 'New York')
(5, 'Nevada')
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 0-select_states.py
  
0/10 pts
1. Filtrer les états
Obligatoire
Écrire un script qui liste tous les états dont le nom commence par N (N majuscule) de la base de données hbtn_0e_0_usa :

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données (aucune validation des arguments nécessaire)
Vous devez utiliser le module MySQLdb (import MySQLdb)
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Les résultats doivent être triés par ordre croissant selon states.id
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 0-select_states.sql
-- Créer la table states dans hbtn_0e_0_usa avec某些 données
CREATE DATABASE IF NOT EXISTS hbtn_0e_0_usa;
USE hbtn_0e_0_usa;
CREATE TABLE IF NOT EXISTS states ( 
    id INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id)
);
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

guillaume@ubuntu:~/$ cat 0-select_states.sql | mysql -uroot -p
Enter password: 
guillaume@ubuntu:~/$ ./1-filter_states.py root root hbtn_0e_0_usa
(4, 'New York')
(5, 'Nevada')
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 1-filter_states.py
  
0/11 pts
2. Filtrer les états par entrée utilisateur
Obligatoire
Écrire un script qui prend en argument et affiche toutes les valeurs dans la table states de hbtn_0e_0_usa où le nom correspond à l'argument.

Votre script doit prendre 4 arguments : nom d'utilisateur mysql, mot de passe mysql, nom de la base de données et nom d'état recherché (aucune validation des arguments nécessaire)
Vous devez utiliser le module MySQLdb (import MySQLdb)
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Vous devez utiliser format pour créer la requête SQL avec l'entrée de l'utilisateur
Les résultats doivent être triés par ordre croissant selon states.id
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 0-select_states.sql
-- Créer la table states dans hbtn_0e_0_usa avec某些 données
CREATE DATABASE IF NOT EXISTS hbtn_0e_0_usa;
USE hbtn_0e_0_usa;
CREATE TABLE IF NOT EXISTS states ( 
    id INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id)
);
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

guillaume@ubuntu:~/$ cat 0-select_states.sql | mysql -uroot -p
Enter password: 
guillaume@ubuntu:~/$ ./2-my_filter_states.py root root hbtn_0e_0_usa 'Arizona'
(2, 'Arizona')
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 2-my_filter_states.py
  
0/13 pts
3. Injection SQL...
Obligatoire
Attendez, vous rappelez la tâche précédente ? Avez-vous testé "Arizona'; TRUNCATE TABLE states ; SELECT * FROM states WHERE name = '" comme une entrée ?

guillaume@ubuntu:~/$ ./2-my_filter_states.py root root hbtn_0e_0_usa "Arizona'; TRUNCATE TABLE states ; SELECT * FROM states WHERE name = '"
(2, 'Arizona')
guillaume@ubuntu:~/$ ./0-select_states.py root root hbtn_0e_0_usa
guillaume@ubuntu:~/$ 
Quoi ? Vide ?

Oui, c'est une injection SQL pour supprimer toutes les enregistrements d'une table…

Une fois de plus, écrire un script qui prend des arguments et affiche toutes les valeurs dans la table states de hbtn_0e_0_usa où le nom correspond à l'argument. Mais cette fois, écrire un qui est safe contre les injections MySQL !

Votre script doit prendre 4 arguments : nom d'utilisateur mysql, mot de passe mysql, nom de la base de données et nom d'état recherché (safe des injections MySQL)
Vous devez utiliser le module MySQLdb (import MySQLdb)
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Utilisez seulement execute() une fois
Les résultats doivent être triés par ordre croissant selon states.id
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 0-select_states.sql
-- Créer la table states dans hbtn_0e_0_usa avec某些 données
CREATE DATABASE IF NOT EXISTS hbtn_0e_0_usa;
USE hbtn_0e_0_usa;
CREATE TABLE IF NOT EXISTS states ( 
    id INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id)
);
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

guillaume@ubuntu:~/$ cat 0-select_states.sql | mysql -uroot -p
Enter password: 
guillaume@ubuntu:~/$ ./3-my_safe_filter_states.py root root hbtn_0e_0_usa 'Arizona'
(2, 'Arizona')
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 3-my_safe_filter_states.py
  
0/11 pts
4. Villes par états
Obligatoire
Écrire un script qui liste toutes les villes de la base de données hbtn_0e_4_usa

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données
Vous devez utiliser le module MySQLdb (import MySQLdb)
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Les résultats doivent être triés par ordre croissant selon cities.id
Utilisez seulement execute() une fois
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 4-cities_by_state.sql
-- Créer la table states dans hbtn_0e_4_usa avec某些 données
CREATE DATABASE IF NOT EXISTS hbtn_0e_4_usa;
USE hbtn_0e_4_usa;
CREATE TABLE IF NOT EXISTS states ( 
    id INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id)
);
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

CREATE TABLE IF NOT EXISTS cities ( 
    id INT NOT NULL AUTO_INCREMENT, 
    state_id INT NOT NULL,
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id),
    FOREIGN KEY(state_id) REFERENCES states(id)
);
INSERT INTO cities (state_id, name) VALUES (1, "San Francisco"), (1, "San Jose"), (1, "Los Angeles"), (1, "Fremont"), (1, "Livermore");
INSERT INTO cities (state_id, name) VALUES (2, "Page"), (2, "Phoenix");
INSERT INTO cities (state_id, name) VALUES (3, "Dallas"), (3, "Houston"), (3, "Austin");
INSERT INTO cities (state_id, name) VALUES (4, "New York");
INSERT INTO cities (state_id, name) VALUES (5, "Las Vegas"), (5, "Reno"), (5, "Henderson"), (5, "Carson City");

guillaume@ubuntu:~/$ cat 4-cities_by_state.sql | mysql -uroot -p
Enter password: 
guillaume@ubuntu:~/$ ./4-cities_by_state.py root root hbtn_0e_4_usa
(1, 'San Francisco', 'California')
(2, 'San Jose', 'California')
(3, 'Los Angeles', 'California')
(4, 'Fremont', 'California')
(5, 'Livermore', 'California')
(6, 'Page', 'Arizona')
(7, 'Phoenix', 'Arizona')
(8, 'Dallas', 'Texas')
(9, 'Houston', 'Texas')
(10, 'Austin', 'Texas')
(11, 'New York', 'New York')
(12, 'Las Vegas', 'Nevada')
(13, 'Reno', 'Nevada')
(14, 'Henderson', 'Nevada')
(15, 'Carson City', 'Nevada')
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 4-cities_by_state.py
  
0/10 pts
5. Toutes les villes par état
Obligatoire
Écrire un script qui prend en argument le nom d'un état et liste toutes les villes de cet état, en utilisant la base de données hbtn_0e_4_usa

Votre script doit prendre 4 arguments : nom d'utilisateur mysql, mot de passe mysql, nom de la base de données et nom d'état (injection SQL free!)
Vous devez utiliser le module MySQLdb (import MySQLdb)
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Les résultats doivent être triés par ordre croissant selon cities.id
Utilisez seulement execute() une fois
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 4-cities_by_state.sql
-- Créer la table states dans hbtn_0e_4_usa avec某些 données
CREATE DATABASE IF NOT EXISTS hbtn_0e_4_usa;
USE hbtn_0e_4_usa;
CREATE TABLE IF NOT EXISTS states ( 
    id INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id)
);
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

CREATE TABLE IF NOT EXISTS cities ( 
    id INT NOT NULL AUTO_INCREMENT, 
    state_id INT NOT NULL,
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id),
    FOREIGN KEY(state_id) REFERENCES states(id)
);
INSERT INTO cities (state_id, name) VALUES (1, "San Francisco"), (1, "San Jose"), (1, "Los Angeles"), (1, "Fremont"), (1, "Livermore");
INSERT INTO cities (state_id, name) VALUES (2, "Page"), (2, "Phoenix");
INSERT INTO cities (state_id, name) VALUES (3, "Dallas"), (3, "Houston"), (3, "Austin");
INSERT INTO cities (state_id, name) VALUES (4, "New York");
INSERT INTO cities (state_id, name) VALUES (5, "Las Vegas"), (5, "Reno"), (5, "Henderson"), (5, "Carson City");

guillaume@ubuntu:~/$ ./5-filter_cities.py root root hbtn_0e_4_usa Texas

guillaume@ubuntu:~/$ cat 4-cities_by_state.sql | mysql -uroot -p
Enter password: 
guillaume@ubuntu:~/$ ./5-filter_cities.py root root hbtn_0e_4_usa Texas
Dallas, Houston, Austin
guillaume@ubuntu:~/$ ./5-filter_cities.py root root hbtn_0e_4_usa Hawaii

guillaume@ubuntu:~/$  
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 5-filter_cities.py
  
0/13 pts
6. Premier modèle d'état
Obligatoire


Écrire un fichier python qui contient la définition de la classe State et une instance Base = declarative_base() :

Classe State :
hérite de Base Conseils
se connecte à la table states de MySQL
attribut de classe id qui représente une colonne d'un entier auto-généré, unique, ne peut pas être null et est une clé primaire
attribut de classe name qui représente une colonne d'une chaîne de 128 caractères et ne peut pas être null
Vous devez utiliser le module SQLAlchemy
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Attention : toutes les classes qui héritent de Base doivent être importées avant d'appeler Base.metadata.create_all(engine)
guillaume@ubuntu:~/$ cat 6-model_state.sql
-- Créer la base de données hbtn_0e_6_usa
CREATE DATABASE IF NOT EXISTS hbtn_0e_6_usa;
USE hbtn_0e_6_usa;
SHOW CREATE TABLE states;

guillaume@ubuntu:~/$ cat 6-model_state.sql | mysql -uroot -p
Enter password: 
ERROR 1146 (42S02) at line 4: Table 'hbtn_0e_6_usa.states' doesn't exist
guillaume@ubuntu:~/$ cat 6-model_state.py
#!/usr/bin/python3
"""Start link class to table in database 
"""
import sys
from model_state import Base, State

from sqlalchemy import (create_engine)

if __name__ == "__main__":
    engine = create_engine('mysql+mysqldb://{}:{}@localhost/{}'.format(sys.argv[1], sys.argv[2], sys.argv[3]), pool_pre_ping=True)
    Base.metadata.create_all(engine)

guillaume@ubuntu:~/$ ./6-model_state.py root root hbtn_0e_6_usa
guillaume@ubuntu:~/$ cat 6-model_state.sql | mysql -uroot -p
Enter password: 
Table   Create Table
states  CREATE TABLE `states` (\n  `id` int(11) NOT NULL AUTO_INCREMENT,\n  `name` varchar(128) NOT NULL,\n  PRIMARY KEY (`id`)\n) ENGINE=InnoDB DEFAULT CHARSET=latin1
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : model_state.py
  
0/10 pts
7. Tous les états via SQLAlchemy
Obligatoire
Écrire un script qui liste tous les objets State de la base de données hbtn_0e_6_usa

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données
Vous devez utiliser le module SQLAlchemy
Vous devez importer State et Base à partir de model_state - from model_state import Base, State
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Les résultats doivent être triés par ordre croissant selon states.id
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 7-model_state_fetch_all.sql
-- Insérer les états
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

guillaume@ubuntu:~/$ cat 7-model_state_fetch_all.sql | mysql -uroot -p hbtn_0e_6_usa
Enter password: 
guillaume@ubuntu:~/$ ./7-model_state_fetch_all.py root root hbtn_0e_6_usa
1: California
2: Arizona
3: Texas
4: New York
5: Nevada
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 7-model_state_fetch_all.py
  
0/10 pts
8. Premier état
Obligatoire
Écrire un script qui affiche le premier objet State de la base de données hbtn_0e_6_usa

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données
Vous devez utiliser le module SQLAlchemy
Vous devez importer State et Base à partir de model_state - from model_state import Base, State
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
L'état affiché doit être le premier en states.id
Vous n'êtes pas autorisé à récupérer tous les états de la base de données avant d'afficher le résultat
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Si la table states est vide, affichez Rien suivi d'un saut de ligne
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ ./8-model_state_fetch_first.py root root hbtn_0e_6_usa
1: California
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 8-model_state_fetch_first.py
  
0/10 pts
9. Contient `a`
Obligatoire
Écrire un script qui liste tous les objets State qui contiennent la lettre a de la base de données hbtn_0e_6_usa

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données
Vous devez utiliser le module SQLAlchemy
Vous devez importer State et Base à partir de model_state - from model_state import Base, State
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Les résultats doivent être triés par ordre croissant selon states.id
Les résultats doivent être affichés comme dans l'exemple ci-dessous
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ ./9-model_state_filter_a.py root root hbtn_0e_6_usa
1: California
2: Arizona
3: Texas
5: Nevada
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 9-model_state_filter_a.py
  
0/12 pts
10. Obtenir un état
Obligatoire
Écrire un script qui affiche l'objet State avec le nom passé en argument de la base de données hbtn_0e_6_usa

Votre script doit prendre 4 arguments : nom d'utilisateur mysql, mot de passe mysql, nom de la base de données et nom d'état à rechercher (injection SQL free)
Vous devez utiliser le module SQLAlchemy
Vous devez importer State et Base à partir de model_state - from model_state import Base, State
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Vous pouvez supposer que vous avez un enregistrement avec le nom d'état à rechercher
Les résultats doivent afficher states.id
Si aucun état n'a le nom recherché, affichez Pas trouvé
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ ./10-model_state_my_get.py root root hbtn_0e_6_usa Texas
3
guillaume@ubuntu:~/$ ./10-model_state_my_get.py root root hbtn_0e_6_usa Illinois
Not found
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 10-model_state_my_get.py
  
0/12 pts
11. Ajouter un nouvel état
Obligatoire
Écrire un script qui ajoute l'objet State "Louisiana" à la base de données hbtn_0e_6_usa

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données
Vous devez utiliser le module SQLAlchemy
Vous devez importer State et Base à partir de model_state - from model_state import Base, State
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Affichez le nouveau states.id après la création
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ ./11-model_state_insert.py root root hbtn_0e_6_usa 
6
guillaume@ubuntu:~/$ ./7-model_state_fetch_all.py root root hbtn_0e_6_usa 
1: California
2: Arizona
3: Texas
4: New York
5: Nevada
6: Louisiana
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 11-model_state_insert.py
  
0/10 pts
12. Mettre à jour un état
Obligatoire
Écrire un script qui change le nom de l'objet State à partir de la base de données hbtn_0e_6_usa

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données
Vous devez utiliser le module SQLAlchemy
Vous devez importer State et Base à partir de model_state - from model_state import Base, State
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Changez le nom de l'État où id = 2 en New Mexico
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ ./12-model_state_update_id_2.py root root hbtn_0e_6_usa 
guillaume@ubuntu:~/$ ./7-model_state_fetch_all.py root root hbtn_0e_6_usa 
1: California
2: New Mexico
3: Texas
4: New York
5: Nevada
6: Louisiana
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : 12-model_state_update_id_2.py
  
0/10 pts
13. Supprimer les états
Obligatoire
Écrire un fichier Python similaire à model_state.py nommé model_city.py qui contient la définition de la classe City.

Classe City :
hérite de Base (importée de model_state)
se connecte à la table MySQL cities
attribut de classe id qui représente une colonne d'un entier auto-généré, unique, ne peut pas être null et est une clé primaire
attribut de classe name qui représente une colonne d'une chaîne de 128 caractères et ne peut pas être null
attribut de classe state_id qui représente une colonne d'un entier, ne peut pas être null et est une clé étrangère vers states.id
Vous devez utiliser le module SQLAlchemy
Ensuite, écrire un script 14-model_city_fetch_by_state.py qui affiche tous les objets City de la base de données hbtn_0e_14_usa :

Votre script doit prendre 3 arguments : nom d'utilisateur mysql, mot de passe mysql et nom de la base de données
Vous devez utiliser le module SQLAlchemy
Vous devez importer State et Base à partir de model_state - from model_state import Base, State
Votre script doit se connecter à un serveur MySQL fonctionnant sur localhost à port 3306
Les résultats doivent être triés par ordre croissant selon cities.id
Les résultats doivent être affichés comme dans l'exemple ci-dessous (<nom d'état> : (<id ville>) <nom ville>)
Votre code ne doit pas être exécuté lorsqu'il est importé
guillaume@ubuntu:~/$ cat 14-model_city_fetch_by_state.sql
-- Créer la base de données hbtn_0e_14_usa, les tables states et cities + certaines données
CREATE DATABASE IF NOT EXISTS hbtn_0e_14_usa;
USE hbtn_0e_14_usa;

CREATE TABLE IF NOT EXISTS states ( 
    id INT NOT NULL AUTO_INCREMENT, 
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id)
);
INSERT INTO states (name) VALUES ("California"), ("Arizona"), ("Texas"), ("New York"), ("Nevada");

CREATE TABLE IF NOT EXISTS cities ( 
    id INT NOT NULL AUTO_INCREMENT, 
    state_id INT NOT NULL,
    name VARCHAR(256) NOT NULL,
    PRIMARY KEY (id),
    FOREIGN KEY(state_id) REFERENCES states(id)
);
INSERT INTO cities (state_id, name) VALUES (1, "San Francisco"), (1, "San Jose"), (1, "Los Angeles"), (1, "Fremont"), (1, "Livermore");
INSERT INTO cities (state_id, name) VALUES (2, "Page"), (2, "Phoenix");
INSERT INTO cities (state_id, name) VALUES (3, "Dallas"), (3, "Houston"), (3, "Austin");
INSERT INTO cities (state_id, name) VALUES (4, "New York");
INSERT INTO cities (state_id, name) VALUES (5, "Las Vegas"), (5, "Reno"), (5, "Henderson"), (5, "Carson City");

guillaume@ubuntu:~/$ cat 14-model_city_fetch_by_state.sql | mysql -uroot -p
Enter password: 
guillaume@ubuntu:~/$ ./14-model_city_fetch_by_state.py root root hbtn_0e_14_usa
California: (1) San Francisco
California: (2) San Jose
California: (3) Los Angeles
California: (4) Fremont
California: (5) Livermore
Arizona: (6) Page
Arizona: (7) Phoenix
Texas: (8) Dallas
Texas: (9) Houston
Texas: (10) Austin
New York: (11) New York
Nevada: (12) Las Vegas
Nevada: (13) Reno
Nevada: (14) Henderson
Nevada: (15) Carson City
guillaume@ubuntu:~/$ 
Aucuns tests de cas nécessaires

Depôt :

GitHub dépôt : holbertonschool-higher_level_programming
Dossier : python-object_relational_mapping
Fichier : model_city.py, 14-model_city_fetch_by_state.py
  
0/10 pts
