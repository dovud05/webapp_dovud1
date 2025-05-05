webapp_dovud
Final Project – AWS Web App Deployment (EC2, RDS, S3)
This project demonstrates a simple web application hosted on AWS using:
•	Amazon EC2 for backend hosting (Flask)
•	Amazon RDS (PostgreSQL) as the database
•	Amazon S3 for static hosting of the HTML page
________________________________________
🔧 EC2 Setup
•	Created a new EC2 instance (Ubuntu)
•	Configured security group to allow:
o	HTTP (80), HTTPS (443), SSH (22), PostgreSQL (5432), Flask Port (8000)
•	Connected via SSH:
bash
CopyEdit
ssh -i "dovud_key_new.pem" ubuntu@ec2-18-139-30-244.ap-southeast-1.compute.amazonaws.com
________________________________________
🐘 RDS Setup (PostgreSQL)
•	Created an RDS PostgreSQL instance:
o	DB Name: db_dovud
o	Table Name: tbl_dovud_<your_dataset>
•	Connected via psql:
bash
CopyEdit
psql -h https://db-dovud3t.c32geugqgvkj.ap-southeast-1.rds.amazonaws.com
•	Sample schema:
sql
CopyEdit
CREATE TABLE tbl_dovud_data (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    category VARCHAR(100)
);
________________________________________
💻 Flask Backend (app.py)
•	Flask app connects to the RDS instance and provides /add and /delete routes for inserting and deleting data.
Run the app:
bash
CopyEdit
python3 app.py
Access the app at: ec2
http://18.139.30.244:8000
________________________________________
🖼️ S3 Static Hosting
•	Created an S3 bucket named webapp-dovud
•	Uploaded the static file index_dovud.html
•	Enabled static hosting and set index_dovud.html as the entry point
•	Set correct bucket policy for public access
Access the static site here:
http://dovud3t.s3-website-ap-southeast-1.amazonaws.com
________________________________________
📁 File Structure
CopyEdit
webapp_dovud/
├── app.py
├── index_dovud.html
├── requirements.txt
└── README.md
________________________________________
📦 Python Dependencies
Install in EC2:
bash
CopyEdit
sudo apt update
sudo apt install python3 python3-pip postgresql-client -y
pip3 install flask psycopg2-binary

