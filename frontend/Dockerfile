# Set the baseImage to use for subsequent instructions.
FROM python:3.9-alpine
# If given, Python won’t try to write .pyc files on the import of source modules.
ENV PYTHONDONTWRITEBYTECODE 1
# Force the stdout and stderr streams to be unbuffered. This option has no effect on the stdin stream.
ENV PYTHONUNBUFFERED 1
# assign working dir
WORKDIR /src
# copy all files
COPY ./ ./
# list files and directories
RUN ls -la && sleep 20
# install packages
RUN pip install -r frontend/requirements.txt

CMD ["python", "frontend/app.py"]
