Link para ver el proyecto [consumiendo Api Clima con JS](https://movie-js-search.netlify.app/).

Subi al repositorio el código sin el js para proteger mi Api key pero lo puedo mostrar en una entrevista.

## Buscador de películas con JavaScript consumiendo API

La aplicación utiliza la API de The Movie Database (TMDb) para buscar películas y mostrar sus detalles.

## Configuración de la API

Obtención de una clave de API registrándote en el sitio web de TMDb. Será la `'API_KEY'` en el código.

    let api_key = 'CLAVE_DE_API'

## Obtención de elementos del DOM

Obtener los elementos HTML necesarios para interactuar con la aplicación. Utilización de `getElementById` para obtener el botón de búsqueda y el campo de entrada de texto.

    document.getElementById('searchButton').addEventListener('click', searchMovies)
    let resultContainer = document.getElementById('results')

## Función de búsqueda de películas

La función `searchMovies` se ejecuta cuando se hace clic en el botón de búsqueda. Obtiene el valor ingresado en el campo de entrada de texto y realiza una solicitud a la API de TMDb para buscar películas que coincidan con el término de búsqueda.

    function searchMovies(){
        resultContainer.innerHTML = 'Cargando...'
        let searchInput = document.getElementById('searchInput').value
        fetch(`${urlBase}?api_key=${api_key}&query=${searchInput}`)
        .then(response => response.json())
        .then(response => displayMovies(response.results))
    }

## Función para mostrar las películas encontradas

La función `displayMovies` se utiliza para mostrar los resultados de la búsqueda de películas. Borra el contenido anterior del contenedor de resultados y luego itera sobre la lista de películas encontradas. Para cada película, crea elementos HTML para mostrar su título, fecha de lanzamiento, descripción y póster.

    function displayMovies(movies){
        resultContainer.innerHTML = ''

        if(movies.length === 0){
            resultContainer.innerHTML= '<p>No se encontraron resultados para tu búsqueda </p>'
            return
        }

        movies.forEach(movie => {
            let movieDiv = document.createElement('div')
            movieDiv.classList.add('movie')

            let title = document.createElement('h2')
            title.textContent = movie.title

            let releaseDate = document.createElement('p')
            releaseDate.textContent = 'La fecha de lanzamiento fue: ' + movie.release_date

            let overview = document.createElement('p')
            overview.textContent = movie.overview

            let posterPath = urlImg + movie.poster_path
            let poster = document.createElement('img')
            poster.src = posterPath

            movieDiv.appendChild(poster)
            movieDiv.appendChild(title)
            movieDiv.appendChild(releaseDate)
            movieDiv.appendChild(overview)

            resultContainer.appendChild(movieDiv)
        })
    }

# Movie-search
