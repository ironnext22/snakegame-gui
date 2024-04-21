FROM python:3.10
LABEL authors="wiktor"

COPY --from=pysnake ./pysnake.py /app
COPY --from=pysnake ./requirements.txt /app
COPY --from=pysnake ./lib /app
COPY --from=pysnake ./tests /app

WORKDIR /app

RUN pip install -r requirements.txt

CMD ["pytest", "-s", "-v"]