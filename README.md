@startuml

package "Sistema" {
    class Aplicacion {
        +buscarPelicula()
        +verDetalles(pelicula: Pelicula)
        +agregarAFavoritos(pelicula: Pelicula)
        +calificarPelicula(pelicula: Pelicula, calificacion: int)
        +comentarPelicula(pelicula: Pelicula, comentario: Comentario)
        +compartirValoraciones(pelicula: Pelicula)
        +añadirAmigo(usuario: Usuario)
        +compartirPeliculasFavoritas(usuario: Usuario)
    }
}

package "Entorno" {
    class Usuario {
        +iniciarSesion()
        +cerrarSesion()
    }

    class Pelicula {
        -titulo: String
        -año: int
        -genero: String
        -director: String
        -sinopsis: String
        -calificacionPromedio: double
        +getInformacion()
        +getCalificacionPromedio()
    }

    class ListaFavoritos {
        -peliculasFavoritas: List<Pelicula>
        +agregarPelicula()
        +eliminarPelicula()
    }

    class Comentario {
        -texto: String
        -fecha: Date
        +getComentario()
        +getFecha()
    }

    class Plataforma {
        -nombre: String
        -tipo: String
        +getInformacion()
    }
}

package "Interfaz" {
    class BuscadorPeliculas {
        +buscarPelicula()
    }

    class DetallesPelicula {
        +verDetalles()
        +hacerComentario(comentario: Comentario)
    }
}

Aplicacion "1" *-- "1..1" BuscadorPeliculas: usa
Aplicacion "1" *-- "1..1" DetallesPelicula: usa
Aplicacion "1" -- "1..*" Usuario: interactúa con
Aplicacion "1" -- "1..*" Pelicula: interactúa con
Aplicacion "1" *-- "1..*" ListaFavoritos: gestiona
Aplicacion "1" *-- "1..*" Comentario: crea
Aplicacion "1" *-- "1..*" Plataforma: utiliza

Usuario "1" *-- "1" ListaFavoritos: tiene
Usuario "1" *-- "0..*" Comentario: escribe

Pelicula "1" *-- "0..*" Comentario: tiene

Interfaz "1" *-- "1" Usuario: muestra
Interfaz "1" *-- "1" Pelicula: muestra

@enduml
