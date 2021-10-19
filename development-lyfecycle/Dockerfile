FROM python
RUN pip install gunicorn redis bottle
ADD *.py *.pyc /app/
#ADD requirements.txt /app/
WORKDIR /app
EXPOSE 8080
CMD ["python","/app/th3-server.py"]

