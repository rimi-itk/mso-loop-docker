# MSO Loop

```sh
docker-compose up --detach
docker-compose run --rm drush --root=/app make --working-copy https://raw.githubusercontent.com/itk-mso/Loop/master/drupal.make /app/web

cat <<'EOF' > web/sites/default/settings.php
<?php
$databases['default']['default'] = [
  'database' => 'db',
  'username' => 'db',
  'password' => 'db',
  'host' => 'mariadb',
  'port' => '',
  'driver' => 'mysql',
  'prefix' => '',
];

echo http://0.0.0.0:$(docker-compose port reverse-proxy 80 | cut -d: -f2)
echo http://mso-loop.docker.localhost:$(docker-compose port reverse-proxy 80 | cut -d: -f2)
```

## Running `drush`

```sh
docker-compose run --rm drush --root=/app/web --uri="http://mso-loop.docker.localhost:$(docker-compose port reverse-proxy 80 | cut -d: -f2)"
```
