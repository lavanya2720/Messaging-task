**Asynchronous Messaging System with Flask, Celery & RabbitMQ**
This project demonstrates a simple asynchronous messaging system using RabbitMQ as the message broker, Celery as the task queue, and a Flask web application that exposes API endpoints for sending emails and logging timestamps.
The application can be exposed publicly using Ngrok, and can optionally run behind Nginx for production-style deployment.

**Project Overview**
The goal of this system is to showcase how asynchronous background job execution works in real-world applications.
Using Celery + RabbitMQ, the system demonstrates:
•	Sending emails asynchronously
•	Logging time via Celery tasks
•	Processing messages in the background
•	Running a Flask API endpoint
•	Exposing APIs externally using Ngrok
•	Managing environment variables securely
•	Optionally using Nginx as a reverse proxy

**Project Structure**
messaging-system/
│
├── app/
│   ├── celery_app.py      # Celery configuration & tasks
│   ├── main.py            # Flask application
│
├── logs/
│   └── app.log            # Log file generated at runtime
│
├── venv/                  # Python virtual environment
├── .env                   # Environment variables
├── start_all.sh           # Script to start the system
└── README.md

**Step 1** — Create Project Directories
mkdir messaging-system
cd messaging-system
mkdir app logs

**Step 2** — Create a Python Virtual Environment
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip

**Step 3**— Install Required Dependencies
pip install flask celery requests python-dotenv
pip install celery[redis]
pip install fastapi uvicorn

**Step 4** — Install & Run RabbitMQ
Option A — Using Docker (Recommended)
docker run -d --name rabbitmq \-p 5672:5672 -p 15672:15672 \rabbitmq:3-management
Management UI → http://localhost:15672

**Step 5** — Create Celery App 
Contains Celery configuration and tasks like sending emails or logging time.

**Step 6** — Create Flask App 
This Flask API exposes endpoints such as:
GET /action?sendmail=youremail@example.com
GET /action?logtime=true

**Step 7** — Create Environment Variables (.env)
EMAIL_USER=your@gmail.com
EMAIL_PASS=your_app_password

**Step 8**— Run 
1.Activate Virtual Environment
source venv/bin/activate
2.Run Celery Worker
celery -A app.celery_app.celery_app worker --loglevel=info
3.Run Flask Application
python app/main.py
4.Start Ngrok
ngrok http 5000
<img width="1920" height="1080" alt="MT 1" src="https://github.com/user-attachments/assets/803c1881-082e-4126-8c7b-fbc18e67a885" />
<img width="1806" height="241" alt="MT2" src="https://github.com/user-attachments/assets/b6e980af-5948-4e5d-abef-5605f666860f" />
<img width="1920" height="1080" alt="MT3" src="https://github.com/user-attachments/assets/fa6af724-9394-496a-b72c-3bd0ae4a4009" />
<img width="1920" height="1080" alt="MT4" src="https://github.com/user-attachments/assets/4f1d9d2b-9faf-4a9e-adb1-13ad7d4da2ec" />

**Testing the System**
Send an email:
http://localhost:5000/action?sendmail=example@gmail.com
Log the current time:
http://localhost:5000/action?logtime=true
<img width="1920" height="1080" alt="MT5" src="https://github.com/user-attachments/assets/8c1608b7-5388-4e25-b1c0-ad24b6d89aa7" />

 
**Conclusion**
This project successfully walked through building a messaging system using Flask, Celery, RabbitMQ, and Ngrok, with optional Nginx. 
we have learned to send emails asynchronously using Celery workers, run RabbitMQ for message brokering, 
expose the local app publicly via Ngrok, manage environment variables securely with .env, and improve deployment by configuring Nginx as a reverse proxy. 
Along the way, you debugged installation, routing, and port issues—gaining practical real-world experience.
