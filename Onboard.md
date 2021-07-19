# Mimum setup

## Running hydra with postgres

`docker-compose -f quickstart.yml -f quickstart-postgres.yml up --build`

## Running hydra client

`docker-compose -f quickstart.yml exec hydra hydra clients create --endpoint http://127.0.0.1:4445/ --id my-client --secret secret -g client_credentials`

### Creating token, Client Credentials Grant

`docker-compose -f quickstart.yml exec hydra hydra token client --endpoint http://127.0.0.1:4444/ --client-id my-client    --client-secret secret`

Test the token

`docker-compose -f quickstart.yml exec hydra hydra token introspect --endpoint http://127.0.0.1:4445/ l_U0_q1xNWMVt9sKpaapY-FleO24OPAaeCM-Q_Cy21g.UmC4XNJErJ3-9Csx_W7aqvjQyHL6R4YzK7xgNo98C2U`

### Creating authcode, Authcode Grant

`docker-compose -f quickstart.yml exec hydra hydra clients create --endpoint http://127.0.0.1:4445 --id auth-code-client --secret secret --grant-types authorization_code,refresh_token --response-types code,id_token --scope openid,offline --callbacks http://127.0.0.1:5555/callback`

Run example web application to test manual grant

`docker-compose -f quickstart.yml exec hydra hydra token user --client-id auth-code-client --client-secret secret --endpoint http://127.0.0.1:4444/ --port 5555 --scope openid,offline`
