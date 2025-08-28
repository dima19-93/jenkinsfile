# jenkinsfile.GPT
Завдання з ** 
Пояснення по блоках

1. pipeline { ... }
Визначає декларативний пайплайн Jenkins.
agent any можна виконувати на будь-якому агенті, де є Linux.

2. stage('Install Apache')
apt-get update — оновлює список пакетів.
apt-get install -y apache2 — ставить Apache (якщо вже стоїть, просто нічого не робить).
systemctl start apache2 — запускає Apache.
systemctl enable apache2 — додає в автозапуск.
systemctl is-active --quiet apache2 — перевіряє, чи сервіс реально працює.
Якщо Apache не запуститься, stage зупиниться з помилкою.

3. stage('Verify Apache Running')
Використовує curl -I http://localhost, щоб отримати тільки заголовки HTTP-відповіді.
Перевіряє, чи є в них 200 OK.
Якщо ні — pipeline впаде.


4. stage('Trigger 404')
Викликає сторінку, якої не існує (/missing-folder/assistent.html).
curl -o /dev/null -s -w "%{http_code}" → повертає тільки HTTP-код (наприклад 404).
Якщо код не дорівнює 404 — pipeline зупиниться з помилкою.

5. post { ... }
always → виконується завжди, незалежно від результату.
success → показує повідомлення, якщо всі stage пройшли.
failure → показує повідомлення, якщо щось впало.
