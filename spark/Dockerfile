FROM jupyter/all-spark-notebook:b2562c469cdd

WORKDIR /home/jovyan/work

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY notebook notebook

EXPOSE 8888

