# Selenium E-Commerce Automation

Framework de automatizacion de pruebas para [SauceDemo](https://www.saucedemo.com/) utilizando Selenium WebDriver con Java y el patron Page Object Model (POM).

## Tecnologias

![Java](https://img.shields.io/badge/Java_11-ED8B00?style=flat&logo=openjdk&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium_4.18-43B02A?style=flat&logo=selenium&logoColor=white)
![TestNG](https://img.shields.io/badge/TestNG_7.9-FF7300?style=flat&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=flat&logo=apachemaven&logoColor=white)
![ExtentReports](https://img.shields.io/badge/ExtentReports_5.1-00897B?style=flat&logoColor=white)

## Estructura del proyecto

```
src/
├── main/java/com/shopzone/pages/
│   ├── BasePage.java              # Clase base con operaciones comunes
│   ├── LoginPage.java             # Interacciones de login
│   ├── ProductsPage.java          # Catalogo y ordenamiento
│   ├── CartPage.java              # Carrito de compras
│   └── CheckoutPage.java          # Proceso de pago
└── test/java/com/shopzone/
    ├── base/BaseTest.java         # Setup y teardown
    └── tests/
        ├── LoginTest.java         # 5 tests de autenticacion
        ├── ProductsTest.java      # 7 tests de productos
        ├── CartTest.java          # 4 tests de carrito
        └── CheckoutTest.java      # 5 tests de checkout
```

## Cobertura de tests

| Suite | Tests | Escenarios |
|-------|-------|------------|
| Login | 5 | Login valido, credenciales invalidas, campos vacios, usuario bloqueado |
| Products | 7 | Carga de productos, agregar/remover del carrito, ordenamiento por precio y nombre |
| Cart | 4 | Carrito vacio, agregar productos, remover items, navegacion |
| Checkout | 5 | Flujo completo, validaciones de campos, checkout con multiples productos |
| **Total** | **21** | |

## Requisitos previos

- Java 11+
- Maven 3+
- Google Chrome

## Como ejecutar

```bash
# Ejecutar todos los tests
mvn test

# Modo headless (sin navegador visible)
mvn test -Dheadless=true

# Ejecutar una suite especifica
mvn test -Dtest=LoginTest

# Ejecutar con TestNG suite
mvn test -DsuiteXmlFile=testng.xml
```

## Arquitectura

El framework implementa el patron **Page Object Model (POM)**:

- **BasePage**: Clase abstracta con metodos reutilizables (`click`, `type`, `getText`, `isDisplayed`) y esperas explicitas con `WebDriverWait`
- **Page Objects**: Cada pagina encapsula sus locators (`@FindBy`) y acciones
- **Tests**: Heredan de `BaseTest` que maneja el ciclo de vida del WebDriver
- **Ejecucion paralela**: Configurada en `testng.xml` con 2 threads a nivel de clase
