# Basic Web Server in Golang

This repository contains a simple web server implementation using Go (Golang). The server responds with a html pages message for every request.

## Prerequisites

Before you begin, ensure you have met the following requirements:
- You have installed [Go](https://golang.org/doc/install) (at least version 1.16).
- You have a working internet connection.

## Installation

1. Clone the repository:

   ```bash
   git clone (https://github.com/Cybersayak/WebServer1stApp.git)

Sure! Here's a README for your Web Server project that renders HTML pages:

---

## Project Structure

```
.
├── main.go
└── static
    ├── form.html
    └── index.html
```

## Files

### `main.go`

This is the entry point of the application. It sets up the HTTP server and routes.

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

func formHandler(w http.ResponseWriter, r *http.Request) {
	if err := r.ParseForm(); err != nil {
		fmt.Fprintf(w, "ParseForm() err: %v", err)
	}
	fmt.Fprint(w, "POST request successful")
	name := r.FormValue("name")
	address := r.FormValue("address")
	email := r.FormValue("email")
	fmt.Fprintf(w, "Name = %s\n", name)
	fmt.Fprintf(w, "Address = %s\n", address)
	fmt.Fprintf(w, "Email = %s\n", email)
}

func helloHandler(w http.ResponseWriter, r *http.Request) {
	if r.URL.Path != "/hello" {
		http.Error(w, "404 not found", http.StatusNotFound)
		return
	}
	if r.Method != "GET" {
		http.Error(w, "Method not allowed", http.StatusNotFound)
		return
	}
	fmt.Fprint(w, "Hello Commanders")
}

func main() {
	fileServer := http.FileServer(http.Dir("./static"))
	http.Handle("/", fileServer)
	http.HandleFunc("/form", formHandler)
	http.HandleFunc("/hello", helloHandler)
	fmt.Printf("Starting server on port 8080\n")
	if err := http.ListenAndServe(":8080", nil); err != nil {
		log.Fatal(err)
	}
}

```

### `static/form.html`

This is the HTML template for the home page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Static Site in Golang</title>
</head>
<body>
    </form>
    <form action="/form" method="post">
      <label for="name">Name:</label><br>
      <input type="text" id="name" name="name"><br>
      <label for="address">Address:</label><br>
      <input type="text" id="address" name="address"><br>
      <label for="emailaddress">Email:</label><br>
      <input type="email" id="email" name="email"><br><br>
        
      <input type="submit" value="Submit">
    </form> 
</body>
</html>
```

### `static/index.html`

This is the HTML template for the about page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>About Page</title>
</head>
<body>
    <h1>Welcome to the About Page</h1>
</body>
</html>
```

## Running the Project

1. Ensure you have Go installed on your machine.
2. Clone the repository or copy the project structure to your local machine.
3. Navigate to the project directory.
4. Run the application using the following command:

```sh
go run main.go
```

5. Open your web browser and navigate to `http://localhost:8000` to see the home page.
6. Navigate to `http://localhost:8000/about` to see the about page.

## Conclusion

This project provides a simple example of how to set up a basic web server in Go with handlers, template rendering, and HTML templates. You can expand this project by adding more routes, templates, and functionality as needed.


---

You can find the project repository [here](https://github.com/Cybersayak/WebServer1stApp).
