# Database Study: Redis vs PostGreSQL
This project is a study on the Redis DataBase Management System (DBMS) and another DBMS, PostGreSQL.  
The goal of this study is to shed light on the common points and the differences between the two above DBMS'.  
The database used in the study is the [animal-crossing database](https://www.kaggle.com/jessicali9530/animal-crossing-new-horizons-nookplaza-dataset) on Kaggle.

## Table Of Content.
* **0** [**Organization of the repository** ](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#0-organization-of-the-repository-toc)
* **1** [**Prerequisites.**                 ](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#1-prerequisites-toc)
* **2** [**Import the database...**         ](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#2-import-the-database-toc)
  - **2.1** [**... into PostGreSQL.**          ](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#21--into-postgresql-toc)
  - **2.2** [**... into Redis.**               ](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#22--into-redis-toc)
* **3** [**Inspect the tables manually.**   ](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#3-inspect-the-tables-manually-toc)

## 0. Organization of the repository [[toc](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#table-of-content)]

The repository is organized as follows:  
📦 ***animal-crossing-db-study***  
┣ 📂 [`tables`]  -- *all the tables from **Animal Crossing New Horizons,** from Kaggle.*  
┃ ┣ 📜 [`accessories.csv`]  
┃ ┣ 📜 [`achievements.csv`]  
┃ ┣ ...  
┃ ┗ 📜 [`wallpaper.csv`]  
┣ 📂 [`scripts`]  
┃ ┣ 📂 [`imports`]  
┃ ┃ ┣ 📜 [`redis_import_main.py`]  -- *a python script that generates a `.redis` file or sends tables to a `redis` server.*  
┃ ┃ ┣ 📜 [`cact4p.sql`]  -- *a `.sql` script that creates and loads all the tables from [`tables`].*  
┃ ┣ 📜 ...  
┃ ┗ 📜 [`analysis.py`]  
┣ 📜 LICENCE  
┣ 📜 README.md  
┗ 📜 [`cact4p`]  -- *a bash wrapper to use [`cact4p.sql`] more easily.*  
┗ 📜 [`seecsv`]  -- *a bash tool to manually look at the tables in `.csv` files.*  
┗ 📜 [`relations.md`]  -- *a summary of the dataset and the relations between the tables.*

## 1. Prerequisites. [[toc](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#table-of-content)]
Install PostGreSQL: [tutorial](https://supaerodatascience.github.io/OBD/0_2_postgres.html#postgresql-installation)  
Install Redis: [tutorial](https://redis.io/)
```bash
pip install redis
```

## 2. Import the database... [[toc](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#table-of-content)]
### 2.1. ... into PostGreSQL. [[toc](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#table-of-content)]

Run the following commands to create a new data base and automatically fill the tables:  
```bash
createdb animal-crossing
```
and then
```bash
./cact4p tables
```

### 2.2. ... into Redis. [[toc](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#table-of-content)]

After installing redis server, and redis-py on your computer. And making sure the redis server is running. Execute the python file to generate a redis script.  
i.e. in one terminal, or in one `tmux`-like tool session:
```bash
redis-server
```
and in a another one:
```bash
python3 scripts/imports/redis_import_main.py tables
```
Use `python3 scripts/imports/redis_import_main.py -h` to learn more about the use of the python script.

## 3. Inspect the tables manually. [[toc](https://github.com/AntoineStevan/animal-crossing-db-study/tree/main/#table-of-content)]
If you want to inspect the tables in [`tables`], it can be quite tideous in the terminal without the proper tool.  
This is why we introduce [`seecsv`], a simple tool to see any `.csv` table inside the terminal.  
*Might not work perfectly with large tables, e.g. with pretty long strings*, but it can give a good idea of what is inside a given table.  
To use it, simply run the following: 
```bash
./seecsv /path/to/table.csv
```

[`tables`]: tables
[`accessories.csv`]: tables/accessories.csv
[`achievements.csv`]: tables/achievements.csv
[`wallpaper.csv`]: tables/wallpaper.csv
[`scripts`]: scripts
[`imports`]: scripts/imports
[`redis_import_main.py`]: scripts/imports/redis_import_main.py
[`import_db.redis`]: scripts/imports/import_db.redis
[`cact4p.sql`]: scripts/imports/cact4p.sql
[`cact4p`]: scripts/imports/cact4p
[`analysis.py`]: scripts/analysis.py
[`relations.md`]: relations.md
[`seecsv`]: seecsv
