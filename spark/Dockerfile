FROM jupyter/pyspark-notebook:latest

ENV SPARK_MODE=master
ENV SPARK_MASTER_PORT=7077

WORKDIR /home/jovyan/work

EXPOSE 8888

ENV JUPYTER_TOKEN=""
CMD start-notebook.sh --NotebookApp.token=''