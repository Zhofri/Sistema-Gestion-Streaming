# Sistema-Gestion-Streaming
package main

import (
    "fmt"
    "log"
    "sistemagestionstreaming/internal/contenido"
    "sistemagestionstreaming/internal/suscripciones"
    "sistemagestionstreaming/internal/usuarios"
    "sistemagestionstreaming/pkg"
    "time"
)

func main() {
    // Canal para manejar usuarios
    usuarioCanal := make(chan *usuarios.Usuario)

    // Mensaje de bienvenida
    fmt.Println("=== Bienvenido al Sistema de Gestión de Streaming ===")

    // Crear un usuario utilizando setters con manejo de errores
    go func() {
        user := &usuarios.Usuario{}
        if err := user.SetNombre("Juan Pérez"); err != nil {
            log.Println("Error al asignar nombre:", err)
        }
        if err := user.SetPassword("abc123"); err != nil {
            log.Println("Error al asignar contraseña:", err)
        }
        if err := user.SetEmail("juan.perez@example.com"); err != nil {
            log.Println("Error al asignar email:", err)
        }
        usuarioCanal <- user // Enviar el usuario al canal
    }()

    // Crear un contenido utilizando setters con manejo de errores
    video := &contenido.Contenido{}
    if err := video.SetTitulo("Documental de Naturaleza"); err != nil {
        log.Println("Error al asignar título:", err)
    }
    if err := video.SetCategoria("Documental"); err != nil {
        log.Println("Error al asignar categoría:", err)
    }
    if err := video.SetDuracion(90); err != nil {
        log.Println("Error al asignar duración:", err)
    }

    // Crear una suscripción utilizando setters con manejo de errores
    sub := &suscripciones.Suscripcion{}
    if err := sub.SetPlan("Premium"); err != nil {
        log.Println("Error al asignar plan:", err)
    }
    if err := sub.SetUsuarioID(1); err != nil {
        log.Println("Error al asignar ID de usuario:", err)
    }

    // Uso de la interfaz para imprimir información de los objetos creados
    var elementos []pkg.InfoPrinter = []pkg.InfoPrinter{video, sub}
    for _, elem := range elementos {
        elem.PrintInfo() // Llama a PrintInfo() de cada objeto
    }

    // Esperar al usuario y procesarlo
    user := <-usuarioCanal // Recibir el usuario procesado
    fmt.Println("Usuario creado:", user.Nombre)

    // Mensaje final de éxito
    fmt.Println("=== Sistema ejecutado exitosamente ===")
}

            log.Println("Error al asignar email:", err)
        }
        usuarioCanal <- user // Enviar el usuario al canal
    }()

    video := &contenido.Contenido{}
    if err := video.SetTitulo("Documental de Naturaleza"); err != nil {
        log.Println("Error al asignar título:", err)
    }
    if err := video.SetCategoria("Documental"); err != nil {
        log.Println("Error al asignar categoría:", err)
    }
    if err := video.SetDuracion(90); err != nil {
        log.Println("Error al asignar duración:", err)
    }

    sub := &suscripciones.Suscripcion{}
    if err := sub.SetPlan("Premium"); err != nil {
        log.Println("Error al asignar plan:", err)
    }
    if err := sub.SetUsuarioID(1); err != nil {
        log.Println("Error al asignar ID de usuario:", err)
    }

    var elementos []pkg.InfoPrinter = []pkg.InfoPrinter{video, sub}
    for _, elem := range elementos {
        elem.PrintInfo()
    }

    // Recibir el usuario creado
    user := <-usuarioCanal
    fmt.Println("Usuario creado:", user.Nombre)

    // Iniciar el servidor web
    api.IniciarServidor()

    fmt.Println("=== Sistema ejecutado exitosamente ===")

