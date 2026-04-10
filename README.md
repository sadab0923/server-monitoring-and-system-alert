import psutil
import smtplib

# Thresholds
CPU_THRESHOLD = 80
MEM_THRESHOLD = 80
DISK_THRESHOLD = 80

def send_alert(message):
    sender = "your_email@gmail.com"
    receiver = "receiver@gmail.com"
    password = "your_password"

    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.starttls()
    server.login(sender, password)

    subject = "Server Alert!"
    body = f"Subject: {subject}\n\n{message}"

    server.sendmail(sender, receiver, body)
    server.quit()

def monitor():
    cpu = psutil.cpu_percent()
    memory = psutil.virtual_memory().percent
    disk = psutil.disk_usage('/').percent

    if cpu > CPU_THRESHOLD:
        send_alert(f"High CPU Usage: {cpu}%")

    if memory > MEM_THRESHOLD:
        send_alert(f"High Memory Usage: {memory}%")

    if disk > DISK_THRESHOLD:
        send_alert(f"High Disk Usage: {disk}%")

monitor()
