FROM python
RUN useradd -m -d /app appuser
USER appuser
RUN pip install gunicorn redis bottle
ADD *.py *.pyc /app/
#ADD requirements.txt /app/
WORKDIR /app
EXPOSE 8080
CMD ["python","/app/th3-server.py"]

