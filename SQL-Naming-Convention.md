En el siguiente documento detallamos el estándar que usamos para modelar las base de datos relacionales.

## Idioma

Todo será en idioma inglés, tanto el nombre de las entidades como de los atributos.


```
CREATE TABLE IF NOT EXISTS `docs` (
  `id` int(6) unsigned NOT NULL,
  `rev` int(3) unsigned NOT NULL,
  `content` varchar(200) NOT NULL,
  `created_at` datetime NOT NULL,
  `updated_at` datetime NOT NULL,
  PRIMARY KEY (`id`,`rev`)
) DEFAULT CHARSET=utf8;
```

## Entidades

Se usarán el nombre en singular con minúsculas con guión bajo.

## Atributos

Se usarán minúsculas con guión bajo.

## Campos por defecto

Se usarán los campos *created_at* y *updated_at* en todas las tablas.

### Fuentes

[http://leshazlewood.com/software-engineering/sql-style-guide/](http://leshazlewood.com/software-engineering/sql-style-guide/)