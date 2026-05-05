## Sistema de Autenticación con Spring Security 6

Programación Web — Unidad 9: Seguridad en Aplicaciones Web
Universidad de Santander (UDES) — Ingeniería de Sistemas 2026

## Descripción

Aplicación web desarrollada con Spring Boot y Spring Security 6 que implementa un sistema completo de autenticación y autorización. Incluye registro de usuarios con contraseñas encriptadas mediante BCrypt, inicio de sesión personalizado, y control de acceso basado en roles (ADMIN y USER). Los usuarios se almacenan en MySQL y la autenticación se realiza mediante un UserDetailsService personalizado.

## Estructura del proyecto
``
estudiantes/
├── src/main/java/com/universidad/estudiantes/
│   ├── config/
│   │   └── SecurityConfig.java
│   ├── model/
│   │   └── Usuario.java
│   ├── repository/
│   │   └── UsuarioRepository.java
│   ├── service/
│   │   ├── UsuarioService.java
│   │   └── UsuarioDetailsService.java
│   └── controller/
│       └── AuthController.java
├── src/main/resources/
│   ├── application.properties
│   └── templates/
│       ├── auth/
│       │   ├── login.html
│       │   └── registro.html
│       ├── admin/
│       │   └── panel.html
│       └── dashboard.html
└── pom.xml
``
## Prerrequisitos

Java JDK 17 o superior
Apache Maven 3.8+
IntelliJ IDEA
MySQL 8+
Navegador web

## Configuración de MySQL

Crear la base de datos antes de ejecutar:

CREATE DATABASE estudiantes_db;

Seleccionar la base de datos:

USE estudiantes_db;

Configurar en application.properties:

spring.datasource.url=jdbc:mysql://localhost:3306/estudiantes_db
spring.datasource.username=root
spring.datasource.password=tu_password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
Ejecución del proyecto

Ejecutar en la terminal:

mvn spring-boot:run

Abrir en navegador:

http://localhost:8080/login
Usuarios de prueba

Usuario normal (crear desde la aplicación):
Email: usuario@correo.com

Contraseña: 123456

Usuario administrador (insertar manualmente en MySQL):
```
INSERT INTO usuarios (nombre, email, contrasenia, rol, activo)
VALUES (
'Administrador',
'admin@universidad.edu',
'$2a$12$TU_HASH_GENERADO',
'ROLE_ADMIN',
1
);
```

Credenciales para login ADMIN:
Email: admin@universidad.edu

Contraseña: admin123

Nota: la contraseña en base de datos debe estar encriptada con BCrypt, no en texto plano.

## Funcionalidades implementadas

Registro de usuarios con validaciones
Contraseñas encriptadas con BCrypt
Login personalizado con Spring Security
Autenticación desde base de datos (MySQL)
Autorización basada en roles
Acceso restringido a /admin solo para ADMIN
Acceso a /dashboard para usuarios autenticados
Logout con invalidación de sesión

## Pruebas realizadas

Registro de usuario y almacenamiento de contraseña como hash BCrypt
Inicio de sesión exitoso con usuario registrado
Acceso a /dashboard después de autenticación
Intento de acceso a /admin con usuario USER devuelve error 403
Acceso a /admin con usuario ADMIN permitido
Logout redirige correctamente a /login?logout

## Capturas de pantalla requeridas

Formulario de login
<img width="585" height="345" alt="image" src="https://github.com/user-attachments/assets/34d10d6b-e3c3-403d-a6dc-38a4bf2c279a" />


Dashboard de usuario ADMIN
<img width="638" height="357" alt="image" src="https://github.com/user-attachments/assets/98612652-67f6-4113-ac6d-8b9fa64fb648" />

<img width="506" height="276" alt="image" src="https://github.com/user-attachments/assets/eb9e003b-11c1-4062-b2cf-a8d3ac605751" />



Acceso denegado 403 al intentar entrar a /admin con usuario USER
<img width="653" height="253" alt="image" src="https://github.com/user-attachments/assets/7aab1c3a-27cb-4258-b881-343be8fbe515" />

Contraseña encriptada en MySQL (hash BCrypt)
<img width="1132" height="154" alt="image" src="https://github.com/user-attachments/assets/a1d11d27-454c-4e9f-bab2-9b999a78fccd" />
