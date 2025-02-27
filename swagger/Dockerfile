FROM swaggerapi/swagger-ui

# swagger.yaml をイメージ内にコピー
COPY swagger.yaml /swagger.yaml

# Swagger UI が参照するファイルパスを環境変数で指定
ENV SWAGGER_JSON=/swagger.yaml
