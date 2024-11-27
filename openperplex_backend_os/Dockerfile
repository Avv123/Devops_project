FROM python:3.12-slim

WORKDIR /workspace
ENV HOME=/workspace

ADD . /workspace

RUN chown -R 42420:42420 /workspace

# Install dependencies using apk and then Python packages
RUN pip install -r requirements.txt

EXPOSE 4000

ENTRYPOINT ["uvicorn"]

CMD ["main:app", "--host", "0.0.0.0", "--port", "4000"]


# this docker image work for OVH CLOUD AI DEPLOY
