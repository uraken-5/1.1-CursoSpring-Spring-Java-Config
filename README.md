# 1.1-CursoSpring-Spring-Java-Config
# Introducción a la Configuración de Spring y la Administración de Beans (Configuración Basada en Java)

Este proyecto presenta una configuración básica de Spring que demuestra la Inversión de Control (IoC) y la Inyección de Dependencias (DI), pero ahora utilizando una **configuración basada en Java** en lugar de un archivo XML. A través de una clase de configuración, definimos nuestros beans y cómo se gestionan dentro del contenedor de Spring.

En este repositorio veremos:
- El concepto de la **Inversión de Control** (IoC)
- **Inyección de Dependencia** (DI)
- Configuración de **beans** utilizando una clase de configuración en Java

## Clases Principales

El proyecto cuenta con tres clases principales:

### Clase `Main`

```java
package com.example.demo;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {

	public static void main(String[] args) {
		ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
		Saludo saludo = context.getBean(Saludo.class);
		saludo.saludoMañanero();
	}
}
```
#### Explicación:

- La clase `Main` actúa como el punto de entrada de la aplicación.
- Utiliza `ApplicationContext`, que es el contenedor IoC de Spring para manejar los beans.
- `AnnotationConfigApplicationContext` es una implementación de `ApplicationContext` que carga la configuración basada en anotaciones desde una clase Java en lugar de un archivo XML.
- Al pasar `AppConfig.class` como parámetro, le indicamos a Spring que use esta clase para la configuración.
- A través de `context.getBean(Saludo.class)`, obtenemos una instancia del bean `Saludo`, definido en `AppConfig`, y luego llamamos a su método `saludoMañanero`.

### Clase AppConfig
```java
package com.example.demo;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {
	
	@Bean
	public Saludo getSaludo() {
		return new Saludo();
	}
	
}
```
#### Explicación:

- La clase `AppConfig` está anotada con `@Configuration`, lo que indica que es una clase de configuración que proporciona definiciones de beans para el contenedor de Spring.
- `@Bean` marca el método `getSaludo` como un bean administrado por Spring, el cual devolverá una instancia de la clase `Saludo`.
- Esta configuración basada en Java reemplaza el archivo XML, permitiendo gestionar los beans directamente en código, lo que facilita la refactorización y la legibilidad.

## Ejecución del Proyecto

Para ejecutar el proyecto:

1. Asegúrate de que la clase `AppConfig` esté en el paquete `com.example.demo`.
2. Ejecuta el método `main` en la clase `Main`.
3. Deberías ver el mensaje `Buenos Dias` en la consola, lo que confirma que Spring ha gestionado exitosamente la creación y administración del bean `Saludo`.

Este es un ejemplo básico que muestra cómo Spring puede manejar beans en una aplicación utilizando una configuración basada en Java, lo que hace que la configuración sea más flexible y mantenible.
