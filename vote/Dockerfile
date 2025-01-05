FROM python:3.7
ADD . .
RUN pip install -r requirements.txt
EXPOSE 80 
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
