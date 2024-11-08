
 Step 1: Prepare the Server
2.Update your system to ensure all packages are up-to-date:
sudo apt update && sudo apt upgrade -y

Step 2: Install Required Software

2.1. Install Python 3.11
Ensure you have Python 3.11 installed, as the Dockerfile uses this version.
sudo apt install python3.11 python3.11-dev python3.11-venv -y

2.2. Install pip
Make sure that pip is installed to manage Python packages:
sudo apt install python3-pip -y

2.3. Install Poetry
Poetry is the package manager for Python dependencies.
curl -sSL https://install.python-poetry.org | python3 -
Poetry ko PATH mein add karna:
.bashrc file ko edit karen:
nano ~/.bashrc
File ke end mein yeh line add karen (agar already add nahi hai):
export PATH="$HOME/.local/bin:$PATH"

Changes ko apply karna:
Ab aapko .bashrc file mein ki gayi changes ko apply karne ke liye bash ko reload karna hoga:
source ~/.bashrc


After installation, verify the version of Poetry:
poetry --version

2.4. Install PostgresSQL
PostgreSQL is required for database management.
sudo apt install postgresql postgresql-contrib -y



After installation, start and enable PostgreSQL:
sudo systemctl start postgresql
sudo systemctl enable postgresql

You can check the status of PostgreSQL with:
sudo systemctl status postgresql




2.5. Install Redis
Redis will be used as the cache management middleware.
sudo apt install redis-server -y

Start and enable Redis:
sudo systemctl start redis
sudo systemctl enable redis
sudo systemctl status redis

Step 3: Set Up Your Application

3.1. Clone the Git Repository
Clone your repo from GitHub:
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
cd attendance-api

3.2. Install Application Dependencies
Use Poetry to install the necessary Python dependencies.
sudo apt install python3-poetry
poetry install
![image](https://github.com/user-attachments/assets/49941af5-fd5a-4747-adfa-fb5a56df5b86)


Update packages


Vi pyproject.toml
packages = [
    {include = "client"},
    {include = "models"},
    {include = "router"},
    {include = "utils"}
]
![image](https://github.com/user-attachments/assets/02185c53-fd3f-4188-91cf-a369a4d426fe)









poetry install
![image](https://github.com/user-attachments/assets/95bd6c9a-0d43-446f-8cc7-b6b47bf3c427)



Failed because psycopg2 ko install karne ke liye libpq-dev package ki zaroorat hoti hai, jo ki PostgreSQL development headers aur libraries ko provide karta hai. Aap ye command run karein:

sudo apt update
sudo apt install libpq-dev

Ab poetry install command dobara run karein:

poetry install
![image](https://github.com/user-attachments/assets/bee4887f-1bda-4249-84df-518dbcabd164)
![image](https://github.com/user-attachments/assets/ad33175d-8f14-47fd-a15c-ab1519c1716e)





























Steps to Install Liquibase
Download Liquibase: Sabse pehle Liquibase ko download karna hoga. Ye command run karein:

sudo snap install liquibase

liquibase --version

make run-migrations
![image](https://github.com/user-attachments/assets/d09ba3b5-2059-4b22-92ef-68045ca1135e)





Change run-migrations

![image](https://github.com/user-attachments/assets/7e44ee66-1390-4c35-b1b8-ddb78332aad6)




13.232.188.111
wget https://jdbc.postgresql.org/download/postgresql-42.5.4.jar -P /home/ubuntu/attendance-api/liquibase_lib/



sudo vi /etc/postgresql/14/main/postgresql.conf

Uncomment listen_addresses
![image](https://github.com/user-attachments/assets/71b2fd63-cd6f-4d77-b4ed-5b6da2b7bd10)


![image](https://github.com/user-attachments/assets/042d590f-51ef-4e77-a794-49098bf14652)









sudo vi /etc/postgresql/14/main/pg_hba.conf

![image](https://github.com/user-attachments/assets/aaae1d42-a4d2-4264-bad6-d4590d7160d0)




Add this line

![image](https://github.com/user-attachments/assets/2bd660f1-130c-4663-b3ce-efd7de8d1d80)



Add classpath
vi liquibase.properties 


classpath=/home/ubuntu/attendance-api/liquibase_lib/postgresql-42.5.4.jar
![image](https://github.com/user-attachments/assets/dd587cb4-3d7a-4f65-927f-0682887a7fc7)




Add host (pub ip)
![image](https://github.com/user-attachments/assets/325366b4-fa67-4410-b6f3-697704fd908d)

sudo netstat -plnt | grep 5432
![image](https://github.com/user-attachments/assets/6355a618-5ba8-4739-bd7e-848940839952)


![image](https://github.com/user-attachments/assets/2cb9fe22-caa2-4577-b3b4-a7bc182f2218)

 




sudo -u postgreS psql

ALTER USER postgres WITH PASSWORD password’ ;


sudo -u postgres psql
CREATE DATABASE attendance_db;
![image](https://github.com/user-attachments/assets/0ccc44c1-c684-463f-8c80-5ef4162fb013)


url=jdbc:postgresql://184.72.203.225:5432/attendance_db

http://3.84.20.150/
 liquibase --changeLogFile=db-changelog.xml update

Face this error
![image](https://github.com/user-attachments/assets/88a4cd1a-5ab2-4b8c-9b79-46129ce54a92)


Add  db-changelog.xml:

vi db-changelog.xml
![image](https://github.com/user-attachments/assets/132b9cc7-e831-4626-bf03-8fd61c3f72c7)

And run again 

liquibase --changeLogFile=db-changelog.xml update
![image](https://github.com/user-attachments/assets/6283df83-1655-40b3-a9c7-97118b3ef9e3)



liquibase --changeLogFile=migration/db-changelog.xml update

Face this error
![image](https://github.com/user-attachments/assets/9ec52682-2ccd-46fc-8c88-4a73aa47d272)


Now  

mv migration/db.changelog-master.xml migration/db-changelog.xml

And run again :
liquibase --changeLogFile=migration/db-changelog.xml update
![image](https://github.com/user-attachments/assets/722130b6-f42a-4de1-abc4-911de0981719)



Run this command:

liquibase --changeLogFile=migration/db-changelog.xml --url=jdbc:postgresql://184.72.203.225:5432/attendance_db --username=postgres --password=password --driver=org.postgresql.Driver update
![image](https://github.com/user-attachments/assets/b67248ac-852f-46ad-8a00-f03a8c9b5519)





make run-migrations
![image](https://github.com/user-attachments/assets/9a0b79d2-caee-4813-bca5-15bb6e6abb0b)



 pip install python-json-logger

 pip install flask
 ![image](https://github.com/user-attachments/assets/1bfd0782-9465-4908-adb9-c8130355b012)

poetry add flasgger

pip install flasgger
![image](https://github.com/user-attachments/assets/08e92cd1-29e8-4b13-9f93-8340423e461a)




 poetry add prometheus_flask_exporter
 
 pip install prometheus_flask_exporter
![image](https://github.com/user-attachments/assets/5fb8685f-9fe4-4c4c-b01e-559029efaaee)


poetry add voluptuous

pip install voluptuous

![image](https://github.com/user-attachments/assets/d7cba79e-0cdf-44a2-9221-fdac3361a2bf)



poetry add psycopg2

pip install psycopg2
![image](https://github.com/user-attachments/assets/28365ba0-8c80-473e-86af-41bda1358401)



poetry add redis

pip install redis
![image](https://github.com/user-attachments/assets/a97e2e10-24b4-484a-8f5f-f233445b07a2)


 poetry add flask-caching
 
 pip install flask-caching

![image](https://github.com/user-attachments/assets/f2603407-b14f-4e1f-a073-54ea6908d8cd)





poetry add peewee

pip install peewee


![image](https://github.com/user-attachments/assets/65543663-7f33-4c75-a0ee-3a578c6ab5ef)





