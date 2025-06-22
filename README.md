# Delcii Urbane-Desktop

Delicii Urbane este o aplicație desktop dezvoltată cu **Java** și **JavaFX**, stilizată cu **CSS**, având ca scop oferirea unei platforme interactive pentru utilizatori pentru a descoperi și comanda delicii culinare urbane.

---

## Funcționalități

* **Interfață Grafică Intuitivă**: Construită cu JavaFX, oferind o experiență de utilizare plăcută.
* **Stilare Personalizată**: Design modern și atractiv folosind CSS.
* **Autentificare Utilizatori**: Funcționalități complete de înregistrare și login.
* **Afișare Meniu**: Vizualizarea preparatelor disponibile din baza de date.
* **Formular de Contact**: Posibilitatea de a trimite mesaje către administrație.
* **Plasare Comenzi**: Sistem de comandă pentru preparatele culinare.
* **Gestionare Cont**: (Funcționalitate menționată, dar necesită implementare completă)
* **Integrare cu Baza de Date MySQL**: Stocarea și preluarea informațiilor despre produse, utilizatori, mesaje de contact și comenzi.

---

## Tehnologii Utilizate

* **Java**
* **JavaFX**
* **CSS**
* **MySQL** (prin conectorul JDBC)

---

## Cerințe de Sistem

* **JDK 19** sau o versiune ulterioară
* **JavaFX SDK**
* **MySQL Server** (recomandat **XAMPP** pentru mediu local)
* Un IDE compatibil cu Java (ex: **IntelliJ IDEA**, Eclipse)

---

## Instalare și Configurare

### 1. Descarcă Proiectul

Clonează acest depozit Git în sistemul tău local:

```sh
git clone https://github.com/username/delicii-urbane.git
cd delicii-urbane
```

### 2. Configurează MySQL (cu XAMPP)

Aplicația folosește o bază de date MySQL. Recomandăm utilizarea **XAMPP** pentru o configurare ușoară a serverului local.

1. **Instalează și Pornește XAMPP**:
    * Descarcă și instalează XAMPP de pe [apachefriends.org](https://www.apachefriends.org/).
    * Pornește **XAMPP Control Panel** și apasă `Start` pentru modulele **Apache** și **MySQL**.

2. **Creează Baza de Date**:
    * Accesează **phpMyAdmin** din XAMPP Control Panel (butonul `Admin` de lângă MySQL).
    * În phpMyAdmin, apasă pe `New` în panoul din stânga.
    * Introdu `meniurestaurant` ca nume pentru baza de date și apasă `Create`.

3. **Creează Tabelele Necesare**:
    * Selectează baza de date `meniurestaurant` din lista din stânga în phpMyAdmin.
    * Accesează tab-ul **`SQL`** din partea de sus.
    * Copiază și rulează următorul script SQL pentru a crea toate tabelele necesare:

```sql
USE meniurestaurant;

-- Tabelul `meniu` (pentru preparatele culinare)
CREATE TABLE IF NOT EXISTS meniu (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Price DECIMAL(10, 2) NOT NULL,
    Quantity VARCHAR(50)
);

-- Tabelul `users` (pentru înregistrare și autentificare)
CREATE TABLE IF NOT EXISTS users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    name VARCHAR(255),
    email VARCHAR(255),
    phoneNumber VARCHAR(20)
);

-- Tabelul `contact` (pentru mesajele din formularul de contact)
CREATE TABLE IF NOT EXISTS contact (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Nume VARCHAR(255),
    Prenume VARCHAR(255),
    Email VARCHAR(255),
    Contact TEXT
);

-- Tabelul `comenzi` (pentru comenzile plasate)
CREATE TABLE IF NOT EXISTS comenzi (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Nume VARCHAR(255),
    NumarTelefon VARCHAR(20),
    Adresa VARCHAR(255),
    Comanda TEXT,
    OrderDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 3. Configurează Conexiunea la Baza de Date în Aplicația Java

Asigură-te că fișierul `DBConnector.java` (din pachetul `service`) are setările corecte pentru conexiunea la baza de date locală (XAMPP).

**Exemplu `DBConnector.java`:**

```java
package service;

public class DBConnector {
    public static final String JDBC_URL = "jdbc:mysql://localhost:3306/meniurestaurant";
    public static final String USER = "root";
    public static final String PASSWORD = ""; // Parola implicită pentru XAMPP root este goală

    // ... restul codului pentru gestionarea conexiunii ...
}
```

*Notă: Dacă ai setat o parolă pentru utilizatorul `root` în MySQL-ul din XAMPP, asigură-te că o actualizezi și în `PASSWORD`.*

### 4. Configurează CSS și Resurse

Fișierele CSS pentru stilizarea aplicației (`BeforeLoginCSS.css`) și imaginile (`images/`) sunt incluse în directorul `src/main/resources/`. Asigură-te că aceste fișiere se află în calea de resurse a proiectului.

---

## Utilizare

1. **Rulează Aplicația**  
   În IDE-ul tău, navighează la clasa principală a aplicației (`src/main/java/com/example/restaurantproject/Main.java`) și rulează aplicația.

2. **Navigarea prin Aplicație**:
    * **Ecranul Principal**: După pornire, vei vedea opțiuni de "Intră în cont!" sau "Înregistrează-te!".
    * **Login/Register**: Creează un cont nou sau loghează-te cu unul existent.
    * **Meniul Principal (după login)**: De aici poți accesa meniul complet, gestiona contul (viitor) sau plasa o comandă.
    * **Vizualizare Meniu**: Vei vedea o listă detaliată a preparatelor din baza de date.
    * **Contact**: Poți trimite mesaje prin formularul de contact.
    * **Comandă**: Formular pentru a plasa o nouă comandă.

---

## Structura Proiectului

```
src/
├── main/
│   ├── java/
│   │   └── com/example/restaurantproject/
│   │       └── Main.java
│   ├── java/model/
│   │   ├── Meal.java
│   │   ├── User.java
│   │   └── Spacer.java
│   ├── java/service/
│   │   ├── DBConnector.java
│   │   └── UserManager.java
│   └── resources/
│       ├── css/
│       │   └── BeforeLoginCSS.css
│       ├── images/
│       └── Anton-Regular.ttf
```

---

## Contact

Pentru orice întrebări sau sugestii, vă rugăm să contactați echipa de dezvoltare la [radustefan.gr@icloud.com](mailto:radustefan.gr@icloud.com).
