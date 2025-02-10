# Starshop

[01. Configurando nuestra App Symfony](#01-configurando-nuestra-app-symfony)

[02. Conociendo nuestro pequeño proyecto](#02-conociendo-nuestro-pequeño-proyecto)

[03. Rutas, controladores y respuestas](#03-rutas-controladores-y-respuestas)

[04. Recetas Flex Mágicas](#04-recetas-flex-mágicas)

[05. Twig y plantillas](#05-twig-y-plantillas)

[06. Herencia de plantillas Twig](#06-herencia-de-plantillas-twig)

[07. Depurando con el Asombroso Perfilador](#07-depurando-con-el-asombroso-perfilador)

[08. Creación de rutas API JSON](#08-creación-de-rutas-api-json)

[09. Los Servicios: La columna vertebral de todo](#09-los-servicios-la-columna-vertebral-de-todo)

[10. Crear tu propio Servicio](#10-crear-tu-propio-servicio)

[11. Rutas más sofisticadas: Requisitos, comodines y más](#11-rutas-más-sofisticadas-requisitos-comodines-y-más)

[12. Generar URLs](#12-generar-urls)

[13. CSS y JavaScript con Asset Mapper](#13-css-y-javascript-con-asset-mapper)

[14. Tailwind CSS](#14-tailwind-css)

[15. Twig Parciales y para bucles](#15-twig-parciales-y-para-bucles)

---

## 01. Configurando nuestra App Symfony

[🔝](#starshop)

### Lo que hace especial a Symfony

### Instalar el binario de Symfony

Creamos el proyecto o lo clonamos de un repositorio de GitHub:

```shell
symfony new starshop

git clone direccion_del_repositorio
```

### Iniciando el Servidor Web symfony

Para ver el proyecto en funcionamiento ejecutamos:

```shell
symfony serve
```

Lo detenemos con `CTRL+C`

## 02. Conociendo nuestro pequeño proyecto

[🔝](#starshop)

### Los 15 archivos de nuestro proyecto

### ¿Dónde está Symfony?

### Ejecuta Composer

Si no tenemos los directorios `/vendor` o `/var`, por ejemplo, porque hemos clonado un proyecto, debemos reconstruirlos.

```shell
composer install
```

### Los 2 directorios que te importan

## 03. Rutas, controladores y respuestas

[🔝](#starshop)

### Creación del controlador

Para hacer más rápido este paso, primero instalamos el asistente que nos ayuda:

```shell
composer require make --dev
```

Lo usamos ejecutando:

```shell
symfony console make:controller
```

Y seguimos los pasos para crear el siguiente controlador.

```shell
src/Controller/MainController.php
```

### Espacios de nombres y directorios

### Crear el método controlador y la ruta

### Controladores y respuestas

## 04. Recetas Flex Mágicas

[🔝](#starshop)

### Alias Flex

### El sistema de recetas

### Instalar PHP CS Fixer

Para instalarlo, ejecuta:

```shell
composer require cs-fixer-shim
```

### Investigando la receta

### Utilizar PHP-CS-Fixer

Ahora que hemos instalado el paquete, vamos a utilizarlo. Para ello, ejecuta:

```shell
php ./vendor/bin/php-cs-fixer fix
```

## 05. Twig y plantillas

[🔝](#starshop)

### Instalación de Twig

```shell
composer require twig
```

### Composer "Paquetes"

### Paquetes Symfony

### La receta Twig

### Renderizar una plantilla

Creamos el archivo `templates/main/homepage.html.twig` con el siguiente contenido.

```html
<h1>
    Starshop: your monopoly-busting option for Starship parts!
</h1>
```

### Pasar datos a una plantilla

Cambiamos el código de nuestro controlador por el siguiente:

```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class MainController extends AbstractController
{
    #[Route('/')]
    public function homepage(): Response
    {
        $starshipCount = 457;

        return $this->render('main/homepage.html.twig', [
            'numberOfStarships' => $starshipCount,
        ]);
    }
}
```

### Renderizar variables

Actualizamos la plantilla:

```twig
<h1>
    Starshop: your monopoly-busting option for Starship parts!
</h1>

<div>
    Browse through {{ numberOfStarships }} starships!
</div>
```

### Etiquetas Twig y la sintaxis "hacer algo"

Volvemos a actualirla:

```twig
<h1>
    Starshop: your monopoly-busting option for Starship parts!
</h1>

<div>
    Browse through {{ numberOfStarships * 10 }} starships!

    {% if numberOfStarships > 400 %}
        <p>
            {# Do you think "shiploads" will pass the legal team? #}
            That's a shiploads of ships!
        </p>
    {% endif %}
</div>
```

### Representación de una matriz asociativa

Actualizamos nuestro controlador:

```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class MainController extends AbstractController
{
    #[Route('/')]
    public function homepage(): Response
    {
        $starshipCount = 457;
        $myShip = [
            'name' => 'USS LeafyCruiser (NCC-0001)',
            'class' => 'Garden',
            'captain' => 'Jean-Luc Pickles',
            'status' => 'under construction',
        ];

        return $this->render('main/homepage.html.twig', [
            'numberOfStarships' => $starshipCount,
            'myShip' => $myShip,
        ]);
    }
}
```

### Funciones y filtros Twig

Actualizamos la plantilla:

```twig
<h1>
    Starshop: your monopoly-busting option for Starship parts!
</h1>

<div>
    Browse through {{ numberOfStarships * 10 }} starships!

    {% if numberOfStarships > 400 %}
        <p>
            {# Do you think "shiploads" will pass the legal team? #}
            That's a shiploads of ships!
        </p>
    {% endif %}
</div>

<div>
    <h2>My Ship</h2>

    <table>
        <tr>
            <th>Name</th>
            <td>{{ myShip.name }}</td>
        </tr>
        <tr>
            <th>Class</th>
            <td>{{ myShip.class }}</td>
        </tr>
        <tr>
            <th>Captain</th>
            <td>{{ myShip.captain|upper|lower|title }}</td>
        </tr>
        <tr>
            <th>Status</th>
            <td>{{ myShip.status }}</td>
        </tr>
    </table>
</div>
```

## 06. Herencia de plantillas Twig

[🔝](#starshop)

### Ampliando el diseño base

```twig
{% extends 'base.html.twig' %}
```

### Reemplazar el título de la página

Actualizamos `templates/main/homepage.html.twig`:

```twig
{% extends 'base.html.twig' %}

{% block title %}Starshop: Beam up some parts!{% endblock %}

{% block body %}
<h1>
    Starshop: your monopoly-busting option for Starship parts!
</h1>

<div>
    Browse through {{ numberOfStarships * 10 }} starships!

    {% if numberOfStarships > 400 %}
        <p>
            {# Do you think "shiploads" will pass the legal team? #}
            That's a shiploads of ships!
        </p>
    {% endif %}
</div>

<div>
    <h2>My Ship</h2>

    <table>
        <tr>
            <th>Name</th>
            <td>{{ myShip.name }}</td>
        </tr>
        <tr>
            <th>Class</th>
            <td>{{ myShip.class }}</td>
        </tr>
        <tr>
            <th>Captain</th>
            <td>{{ myShip.captain|upper|lower|title }}</td>
        </tr>
        <tr>
            <th>Status</th>
            <td>{{ myShip.status }}</td>
        </tr>
    </table>
</div>
{% endblock %}
```

### Sustituir frente a añadir el bloque padre

```twig
{{ parent() }}
```

## 07. Depurando con el Asombroso Perfilador

[🔝](#starshop)

### Instalar las herramientas de depuración

```shell
composer require debug
```

### Hola barra de herramientas de depuración web y perfilador

### ¡Hola bin/console!

```shell
symfony console debug:router
symfony console debug:twig
```

## 08. Creación de rutas API JSON

[🔝](#starshop)

### Creación de la nueva Ruta y Controlador

Creamos el archivo `src/Controller/StarshipApiController.php`.

Cada vez que cree un controlador, extenderé inmediatamente de `AbstractController`.

```php
class StarshipApiController extends AbstractController
{
}
```

### Devolver JSON

Copiamos el siguiente código:

```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class StarshipApiController extends AbstractController
{
    #[Route('/api/starships')]
    public function getCollection(): Response
    {
        $starships = [
            [
                'name' => 'USS LeafyCruiser (NCC-0001)',
                'class' => 'Garden',
                'captain' => 'Jean-Luc Pickles',
                'status' => 'taken over by Q',
            ],
            [
                'name' => 'USS Espresso (NCC-1234-C)',
                'class' => 'Latte',
                'captain' => 'James T. Quick!',
                'status' => 'repaired',
            ],
            [
                'name' => 'USS Wanderlust (NCC-2024-W)',
                'class' => 'Delta Tourist',
                'captain' => 'Kathryn Journeyway',
                'status' => 'under construction',
            ],
        ];

        return $this->json($starships);
    }
}
```

### Añadir una clase modelo

Creamos el archivo `src/Model/Starship.php`.

```php
<?php

namespace App\Model;

class Starship
{
    public function __construct(
        private int $id,
        private string $name,
        private string $class,
        private string $captain,
        private string $status,
    ) {
    }

    public function getId(): int
    {
        return $this->id;
    }

    public function getName(): string
    {
        return $this->name;
    }

    public function getClass(): string
    {
        return $this->class;
    }

    public function getCaptain(): string
    {
        return $this->captain;
    }

    public function getStatus(): string
    {
        return $this->status;
    }
}
```

### Crear los objetos modelo

Actualizamos `src/Controller/StarshipApiController.php`:

```php
<?php

namespace App\Controller;

use App\Model\Starship;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class StarshipApiController extends AbstractController
{
    #[Route('/api/starships')]
    public function getCollection(): Response
    {
        $starships = [
            new Starship(
                1,
                'USS LeafyCruiser (NCC-0001)',
                'Garden',
                'Jean-Luc Pickles',
                'taken over by Q'
            ),
            new Starship(
                2,
                'USS Espresso (NCC-1234-C)',
                'Latte',
                'James T. Quick!',
                'repaired',
            ),
            new Starship(
                3,
                'USS Wanderlust (NCC-2024-W)',
                'Delta Tourist',
                'Kathryn Journeyway',
                'under construction',
            ),
        ];

        return $this->json($starships);
    }
}
```

### Hola Serializador Symfony

```shell
composer require serializer
```

## 09. Los Servicios: La columna vertebral de todo

[🔝](#starshop)

### ¿Qué es un Servicio?

Un servicio es un objeto que hace un trabajo.

### El contenedor y debug:container

A veces también oirás que estos servicios están organizados en un gran objeto llamado "contenedor de servicios". Puedes pensar en el contenedor como en una gigantesca matriz asociativa de objetos de servicio, cada uno con un identificador único. ¿Quieres ver una lista de todos los servicios de nuestra aplicación ahora mismo? Yo también

Busca tu terminal y ejecuta:

```shell
symfony console debug:container
```

### Los bundles proporcionan servicios

¿Recuerdas cuando instalamos `twig`? Añadió un bundle a nuestra aplicación. ¿Y adivinas qué hizo ese bundle? Sí: nos proporcionó nuevos servicios, incluido el servicio `twig`. Los bundles nos dan servicios... y los servicios son herramientas.

### Autocableado

Y aunque hay muchos servicios en esta lista, la gran mayoría son objetos de servicio de bajo nivel que nunca utilizaremos ni nos interesarán. Tampoco nos importará el ID de los servicios la mayoría de las veces.

En su lugar, ejecuta un comando relacionado llamado:

```shell
symfony console debug:autowiring
```

Esto nos muestra todos los servicios que son autocableables, que es la técnica que utilizaremos para obtener servicios. Básicamente, es una lista simplificada de los servicios que es más probable que necesitemos.

### Autoconexión del servicio Logger

La cuestión es: si queremos un *log* (registro) de algo, sólo tenemos que encontrar el servicio que hace ese trabajo. ¡De acuerdo! Vuelve a ejecutar el comando pero busca log:

```shell
symfony console debug:autowiring log
```

```php
class StarshipApiController extends AbstractController
{
// ... line 13
    public function getCollection(LoggerInterface $logger): Response
    {
        dd($logger);
// ... lines 17 - 41
    }
}
```

`dd()` significa "volcar y morir" y viene de Symfony.

El truco que acabamos de hacer -llamado autocableado- funciona exactamente en dos lugares:

* Los métodos de nuestro controlador.
* Y el método `__construct()` de cualquier servicio.

Veremos esta segunda situación en el próximo capítulo.

### Controlar el comportamiento de los servicios

### Utilizar el Logger

Actualizamos el controlador `src/Controller/StarshipApiController.php`:

```php
<?php

namespace App\Controller;

use App\Model\Starship;
use Psr\Log\LoggerInterface;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class StarshipApiController extends AbstractController
{
    #[Route('/api/starships')]
    public function getCollection(LoggerInterface $logger): Response
    {
        $logger->info('Starship collection retrieved');
        $starships = [
            new Starship(
                1,
                'USS LeafyCruiser (NCC-0001)',
                'Garden',
                'Jean-Luc Pickles',
                'taken over by Q'
            ),
            new Starship(
                2,
                'USS Espresso (NCC-1234-C)',
                'Latte',
                'James T. Quick!',
                'repaired',
            ),
            new Starship(
                3,
                'USS Wanderlust (NCC-2024-W)',
                'Delta Tourist',
                'Kathryn Journeyway',
                'under construction',
            ),
        ];

        return $this->json($starships);
    }
}
```

### Ver el Perfilador de una petición API

Para acceder al perfilador de esta petición, cambia la URL a `/_profiler`.

## 10. Crear tu propio Servicio

[🔝](#starshop)

### Crear la clase de servicio

Creamos el archivo `src/Repository/StarshipRepository.php`.

```php
<?php

namespace App\Repository;

use App\Model\Starship;
use Psr\Log\LoggerInterface;

class StarshipRepository
{
    public function findAll(): array
    {
        return [
            new Starship(
                1,
                'USS LeafyCruiser (NCC-0001)',
                'Garden',
                'Jean-Luc Pickles',
                'taken over by Q'
            ),
            new Starship(
                2,
                'USS Espresso (NCC-1234-C)',
                'Latte',
                'James T. Quick!',
                'repaired',
            ),
            new Starship(
                3,
                'USS Wanderlust (NCC-2024-W)',
                'Delta Tourist',
                'Kathryn Journeyway',
                'under construction',
            ),
        ];
    }
}
```

### Autocableado del nuevo servicio

Sólo con crear esta clase, ya está disponible para autocableado.

Actualizamos el controlador `src/Controller/StarshipApiController.php`:

```php
<?php

namespace App\Controller;

use App\Repository\StarshipRepository;
use Psr\Log\LoggerInterface;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class StarshipApiController extends AbstractController
{
    #[Route('/api/starships')]
    public function getCollection(LoggerInterface $logger, StarshipRepository $repository): Response
    {
        $logger->info('Starship collection retrieved');
        $starships = $repository->findAll();

        return $this->json($starships);
    }
}
```

### Autocableado del Constructor

¿Qué pasaría si, desde dentro de `StarshipRepository`, necesitáramos acceder a otro servicio que nos ayudara a hacer nuestro trabajo? Intentemos autocablear de nuevo el servicio logger.

Añade un nuevo `public function __construct()` y realiza el autocableado allí.

```php
class StarshipRepository
{
    public function __construct(private LoggerInterface $logger)
    {
    }
    public function findAll(): array
    {
        $this->logger->info('Starship collection retrieved');
// ... lines 17 - 40
    }
}
```

Si queremos obtener un servicio -como el logger, una conexión a una base de datos, lo que sea-, ésta es la forma correcta de utilizar el autocableado: añadir un método `__construct` dentro de otro servicio. El truco que vimos antes -en el que añadimos el argumento a un método normal- sí, eso es especial y **sólo funciona para los métodos del controlador**. Es una comodidad adicional que se añadió al sistema. Es una gran característica, pero la forma del constructor... así es como funciona realmente el autocableado.

**Si estás en un método controlador, añade el argumento al método.**

### Utilizar el Servicio en otra Página

### Imprimiendo objetos en Twig

Actualizamos `src/Controller/MainController.php`:

```php
<?php

namespace App\Controller;

use App\Repository\StarshipRepository;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

class MainController extends AbstractController
{
    #[Route('/')]
    public function homepage(StarshipRepository $starshipRepository): Response
    {
        $ships = $starshipRepository->findAll();
        $myShip = $ships[array_rand($ships)];

        return $this->render('main/homepage.html.twig', [
            'myShip' => $myShip,
            'ships' => $ships,
        ]);
    }
}
```

Actualizamos `templates/main/homepage.html.twig`:

```twig
{% extends 'base.html.twig' %}

{% block title %}Starshop: Beam up some parts!{% endblock %}

{% block body %}
<h1>
    Starshop: your monopoly-busting option for Starship parts!
</h1>

<div>
    Browse through {{ ships|length * 10 }} starships!

    {% if ships|length > 2 %}
        <p>
            {# Do you think "shiploads" will pass the legal team? #}
            That's a shiploads of ships!
        </p>
    {% endif %}
</div>

<div>
    <h2>My Ship</h2>

    <table>
        <tr>
            <th>Name</th>
            <td>{{ myShip.name }}</td>
        </tr>
        <tr>
            <th>Class</th>
            <td>{{ myShip.class }}</td>
        </tr>
        <tr>
            <th>Captain</th>
            <td>{{ myShip.captain|upper|lower|title }}</td>
        </tr>
        <tr>
            <th>Status</th>
            <td>{{ myShip.status }}</td>
        </tr>
    </table>
</div>
{% endblock %}
```

## 11. Rutas más sofisticadas: Requisitos, comodines y más

[🔝](#starshop)

### Restringir el comodín a un número

```php
class StarshipApiController extends AbstractController
{
// ... lines 12 - 19
    #[Route('/api/starships/{id<\d+>}')]
    public function get(int $id): Response
    {
        dd($id);
    }
}
```

### Restringir el método HTTP de la ruta

```php
class StarshipApiController extends AbstractController
{
    #[Route('/api/starships', methods: ['GET'])]
    public function getCollection(StarshipRepository $repository): Response
// ... lines 14 - 19
    #[Route('/api/starships/{id<\d+>}', methods: ['GET'])]
    public function get(int $id): Response
// ... lines 22 - 24
}
```

### Poner un prefijo a cada URL de ruta

```php
#[Route('/api/starships')]
class StarshipApiController extends AbstractController
{
    #[Route('', methods: ['GET'])]
    public function getCollection(StarshipRepository $repository): Response
// ... lines 15 - 20
    #[Route('/{id<\d+>}', methods: ['GET'])]
    public function get(int $id): Response
// ... lines 23 - 25
}
```

### Finalizando la nueva ruta API

### Activar una página 404

```php
public function get(int $id, StarshipRepository $repository): Response
{
    $starship = $repository->find($id);
    if (!$starship) {
        throw $this->createNotFoundException('Starship not found');
    }
    return $this->json($starship);
}
```

## 12. Generar URLs

[🔝](#starshop)

### Crear la página Mostrar

### Crear la plantilla

Creamos el archivo `templates/starship/show.html.twig`.

### Enlazar entre páginas

```php
class StarshipController extends AbstractController
{
    #[Route('/starships/{id<\d+>}', name: 'app_starship_show')]
    public function show(int $id, StarshipRepository $repository): Response
// ... lines 14 - 23
}
```

El nombre podría ser cualquier cosa, pero ésta es la convención que yo sigo: **app** porque es una ruta que estoy creando en mi aplicación, y luego el nombre de la clase del **controlador** y el nombre del **método**.

Nombrar una ruta nos permite generar una URL hacia ella. Para generar la URL, diré `{{ path() }}` y le pasaré el nombre de la ruta.

## 13. CSS y JavaScript con Asset Mapper

[🔝](#starshop)

¿Qué pasa con las imágenes, CSS y JavaScript? ¿Cómo funciona eso en Symfony?

### Las cosas públicas son... Público

En primer lugar, el directorio `public/` se conoce como la raíz de tu documento. Cualquier cosa dentro de `public/` es accesible para tu usuario final. Todo lo que no esté en `public/` no es accesible.

Así que si quieres crear un archivo CSS o un archivo de imagen o cualquier otra cosa, la vida puede ser tan simple como ponerlo en `public/`. Ahora puedo ir a su ruta y vemos el archivo.

### Hola Mapeador de Activos

Symfony tiene un gran componente llamado `Asset Mapper` que nos permite hacer efectivamente lo mismo, poner archivos en `public/`.

```shell
composer require symfony/asset-mapper
```

### Los 2 superpoderes de Asset Mapper

La receta nos ha proporcionado un nuevo directorio `assets/` con un archivo `app.js` y otro `styles/app.css`.

Asset Mapper tiene dos grandes superpoderes:

1. El primero es que nos ayuda a cargar CSS y JavaScript.
2. Cualquier archivo que pongamos en el directorio `assets/` estará disponible públicamente. Es como si el directorio  `assets/` viviera físicamente dentro de `public/`. Esto es útil porque, sobre la marcha, **Asset Mapper añade el versionado de activos**.

### Listado de activos y ruta lógica

```shell
symfony console debug:asset
```

Creamos el directorio `assets/images/`.

### Representación de una imagen

```twig
<html>
// ... lines 3 - 13
    <body>
        <img src="{{ asset('images/starshop-logo.png') }}" alt="Starshop Logo">
        {% block body %}{% endblock %}
    </body>
</html>
```

Necesitamos instalar el paquete para que funcione:

```shell
composer require symfony/asset
```

### Versionado automático de activos

## 14. Tailwind CSS

[🔝](#starshop)

¿Qué pasa con el CSS? Eres libre de añadir el CSS que quieras a `app/styles/app.css`. Ese archivo ya está cargado en la página.

¿Quieres utilizar CSS de `Bootstrap`? Consulta la documentación de Asset Mapper sobre cómo hacerlo.

### Hola Tailwind

```shell
composer require symfonycasts/tailwind-bundle
```

Para este paquete, la receta no hace nada más que activar el nuevo bundle. Para poner en marcha Tailwind, una vez en tu proyecto, ejecuta:

```shell
symfony console tailwind:init
```

Esto hace tres cosas.

1. Descarga un binario de Tailwind en segundo plano, algo en lo que nunca tendrás que pensar.
2. Crea un archivo `tailwind.config.js` en la raíz de nuestro proyecto. Esto indica a Tailwind dónde tiene que buscar en nuestro proyecto las clases CSS de Tailwind.
3. Actualiza nuestro `app.css` para añadir tres líneas. Estas serán sustituidas por el código real de Tailwind, en segundo plano, por el binario.

### Ejecutar Tailwind

Por último, hay que compilar Tailwind, así que tenemos que ejecutar un comando para hacerlo:

```shell
symfony console tailwind:build -w
```

### Ver Tailwind en acción

```twig
{% block body %}
<h1 class="text-2xl">
    Starshop: your monopoly-busting option for Starship parts!
</h1>
// ... lines 9 - 46
{% endblock %}
```

### Ejecutar automáticamente Tailwind con el binario symfony

```yaml
# .symfony.local.yaml
workers:
    tailwind:
        cmd: ['symfony', 'console', 'tailwind:build', '--watch']
```

### Copiar en plantillas estilizadas

El archivo `templates/base.html.twig`.

```twig
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Welcome!{% endblock %}</title>
        <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 128 128%22><text y=%221.2em%22 font-size=%2296%22>⚫️</text></svg>">
        {% block stylesheets %}
        {% endblock %}

        {% block javascripts %}
{% block importmap %}{{ importmap('app') }}{% endblock %}
        {% endblock %}
    </head>
    <body class="text-white" style="background: radial-gradient(102.21% 102.21% at 50% 28.75%, #00121C 42.62%, #013954 100%);">
        <div class="flex flex-col justify-between min-h-screen relative">
            <div>
                <header class="h-[114px] shrink-0 flex flex-col sm:flex-row items-center sm:justify-between py-4 sm:py-0 px-6 border-b border-white/20 shadow-md">
                    <a href="#">
                        <img class="h-[42px]" src="{{ asset('images/starshop-logo.png') }}" alt="starshop logo">
                    </a>
                    <nav class="flex space-x-4 font-semibold">
                        <a class="hover:text-amber-400 pt-2" href="#">
                            Home
                        </a>
                        <a class="hover:text-amber-400  pt-2" href="#">
                            About
                        </a>
                        <a class="hover:text-amber-400 pt-2" href="#">
                            Contact
                        </a>
                        <a class="rounded-[60px] py-2 px-5 bg-white/10 hover:bg-white/20" href="#">
                            Get Started
                        </a>
                    </nav>
                </header>
                {% block body %}{% endblock %}
            </div>
            <div class="p-5 bg-white/5 mt-3 text-center">
                Made with ❤️ by <a class="text-[#0086C4]" href="https://symfonycasts.com">SymfonyCasts</a>
            </div>
        </div>
    </body>
</html>
```

El `homepage.html.twig`.

```twig
{% extends 'base.html.twig' %}

{% block title %}Starshop: Beam up some parts!{% endblock %}

{% block body %}
    <main class="flex flex-col lg:flex-row">
        <aside
            class="pb-8 lg:pb-0 lg:w-[411px] shrink-0 lg:block lg:min-h-screen text-white transition-all overflow-hidden px-8 border-b lg:border-b-0 lg:border-r border-white/20"
        >
            <div class="flex justify-between mt-11 mb-7">
                <h2 class="text-[32px] font-semibold">My Ship Status</h2>
                <button>
                    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 448 512"><!--!Font Awesome Pro 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2024 Fonticons, Inc.--><path fill="#fff" d="M384 96c0-17.7 14.3-32 32-32s32 14.3 32 32V416c0 17.7-14.3 32-32 32s-32-14.3-32-32V96zM9.4 278.6c-12.5-12.5-12.5-32.8 0-45.3l128-128c12.5-12.5 32.8-12.5 45.3 0s12.5 32.8 0 45.3L109.3 224 288 224c17.7 0 32 14.3 32 32s-14.3 32-32 32l-178.7 0 73.4 73.4c12.5 12.5 12.5 32.8 0 45.3s-32.8 12.5-45.3 0l-128-128z"/></svg>
                </button>
            </div>

            <div>
                <div class="flex flex-col space-y-1.5">
                    <div class="rounded-2xl py-1 px-3 flex justify-center w-32 items-center" style="background: rgba(255, 184, 0, .1);">
                        <div class="rounded-full h-2 w-2 bg-amber-400 blur-[1px] mr-2"></div>
                        <p class="uppercase text-xs">in progress</p>
                    </div>
                    <h3 class="tracking-tight text-[22px] font-semibold">
                        <a class="hover:underline" href="{{ path('app_starship_show', {
                            id: myShip.id
                        }) }}">{{ myShip.name }}</a>
                    </h3>
                </div>
                <div class="flex mt-4">
                    <div class="border-r border-white/20 pr-8">
                        <p class="text-slate-400 text-xs">Captain</p>
                        <p class="text-xl">{{ myShip.captain }}</p>
                    </div>

                    <div class="pl-8">
                        <p class="text-slate-400 text-xs">Class</p>
                        <p class="text-xl">{{ myShip.class }}</p>
                    </div>
                </div>
            </div>
        </aside>

        <div class="px-12 pt-10 w-full">
            <h1 class="text-4xl font-semibold mb-8">
                Ship Repair Queue
            </h1>

            <div class="space-y-5">
                <!-- start ship item -->
                    <div class="bg-[#16202A] rounded-2xl pl-5 py-5 pr-11 flex flex-col min-[1174px]:flex-row min-[1174px]:justify-between">
                        <div class="flex justify-center min-[1174px]:justify-start">
                            <img class="h-[83px] w-[84px]" src="/images/status-in-progress.png" alt="Status: in progress">
                            <div class="ml-5">
                                <div class="rounded-2xl py-1 px-3 flex justify-center w-32 items-center bg-amber-400/10">
                                    <div class="rounded-full h-2 w-2 bg-amber-400 blur-[1px] mr-2"></div>
                                    <p class="uppercase text-xs text-nowrap">in progress</p>
                                </div>
                                <h4 class="text-[22px] pt-1 font-semibold">
                                    <a
                                        class="hover:text-slate-200"
                                        href="#"
                                    >USS LeafyCruiser</a>
                                </h4>
                            </div>
                        </div>
                        <div class="flex justify-center min-[1174px]:justify-start mt-2 min-[1174px]:mt-0 shrink-0">
                            <div class="border-r border-white/20 pr-8">
                                <p class="text-slate-400 text-xs">Captain</p>
                                <p class="text-xl">Jean-Luc Pickles</p>
                            </div>

                            <div class="pl-8 w-[100px]">
                                <p class="text-slate-400 text-xs">Class</p>
                                <p class="text-xl">Garden</p>
                            </div>
                        </div>
                    </div>
                <!-- end ship item -->
            </div>

            <p class="text-lg mt-5 text-center md:text-left">
                Looking for your next galactic ride?
                <a href="#" class="underline font-semibold">Browse the {{ ships|length * 10 }} starships for sale!</a>
            </p>
        </div>
    </main>
{% endblock %}
```

y finalmente `show.html.twig`.

```twig
{% extends 'base.html.twig' %}

{% block title %}{{ ship.name }}{% endblock %}

{% block body %}
<div class="my-4 px-8">
    <a class="bg-white hover:bg-gray-200 rounded-xl p-2 text-black" href="#">
        <svg class="inline text-black" xmlns="http://www.w3.org/2000/svg" height="16" width="14" viewBox="0 0 448 512"><!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#000" d="M9.4 233.4c-12.5 12.5-12.5 32.8 0 45.3l160 160c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L109.2 288 416 288c17.7 0 32-14.3 32-32s-14.3-32-32-32l-306.7 0L214.6 118.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0l-160 160z"/></svg>
        Back
    </a>
</div>
<div class="md:flex justify-center space-x-3 mt-5 px-4 lg:px-8">
    <div class="flex justify-center">
        <img class="max-h-[300px] md:max-h-[500px]" src="{{ asset('images/purple-rocket.png') }}" alt="purple ship launching">
    </div>
    <div class="space-y-5">
        <div class="mt-8 max-w-xl mx-auto">
            <div class="px-8 pt-8">
                <div class="rounded-2xl py-1 px-3 flex justify-center w-32 items-center bg-amber-400/10">
                    <div class="rounded-full h-2 w-2 bg-amber-400 blur-[1px] mr-2"></div>
                    <p class="uppercase text-xs">{{ ship.status }}</p>
                </div>

                <h1 class="text-[32px] font-semibold border-b border-white/10 pb-5 mb-5">
                    {{ ship.name }}
                </h1>
                <h4 class="text-xs text-slate-300 font-semibold mt-2 uppercase">Spaceship Captain</h4>
                <p class="text-[22px] font-semibold">{{ ship.captain }}</p>

                <h4 class="text-xs text-slate-300 font-semibold mt-2 uppercase">Class</h4>
                <p class="text-[22px] font-semibold">{{ ship.class }}</p>

                <h4 class="text-xs text-slate-300 font-semibold mt-2 uppercase">Ship Status</h4>
                <p class="text-[22px] font-semibold">30,000 lys to next service</p>
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

   Si copias los archivos (en lugar del contenido de los archivos), puede que el sistema de caché de Symfony no note el cambio y no veas el nuevo diseño. Si eso ocurre, borra la caché ejecutando:

   ```shell
   symfony console cache:clear.
   ```

## 15. Twig Parciales y para bucles

[🔝](#starshop)

### Organizar en una Plantilla Parcial

En la parte superior de `homepage.html.twig`, este largo elemento `<aside>` es la barra lateral. Está bien que este código viva en `homepage.html.twig`... ¡pero ocupa mucho espacio! ¿Y si queremos reutilizar esta barra lateral en otra página?

Copia este código, y en el directorio `main/` -aunque esto puede ir en cualquier sitio- añade un nuevo archivo llamado `_shipStatusAside.html.twig`. Pega dentro.

De vuelta en `homepage.html.twig`, borra eso, y luego inclúyelo con `{{` - sintaxis decir algo - `include()` y el nombre de la plantilla: `main/_shipStatusAside.html.twig`.

```twig
{% block body %}
    <main class="flex flex-col lg:flex-row">
        {{ include('main/_shipStatusAside.html.twig') }}
// ... lines 8 - 51
    </main>
{% endblock %}
```

### Haciendo un bucle sobre las naves en Twig

```twig
<div class="space-y-5">
    {% for ship in ships %}
// ... lines 16 - 43
    {% endfor %}
</div>
```
