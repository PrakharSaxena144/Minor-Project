# Minor-Project

```markdown
# FastAPI Tutorial Summary and Quick Notes

This document combines the summary and quick notes from both parts of the FastAPI Python web framework tutorial. The tutorial focuses on building a **CRUD** (Create, Read, Update, Delete) inventory application backend, migrating from an in-memory list to a **PostgreSQL** database using **SQLAlchemy**, and finally connecting to a **React** front-end.

***

## 🚀 Part 1: Introduction, Setup, and Initial CRUD (In-Memory)

The tutorial introduces **FastAPI** as a high-performance, easy-to-use web framework for Python, often compared to Django and Flask.

### ⚙️ Environment Setup

| Concept | Description | Command/Tool |
| :--- | :--- | :--- |
| **Prerequisites** | Knowledge of **Python** and basic web application concepts. | Python 3.12/3.13, VS Code (or other IDE) |
| **Virtual Environment** | Essential for isolating project dependencies. | `python -m venv <name>` then activate. |
| **Core Packages** | FastAPI framework and Uvicorn ASGI server. | `pip install fastapi uvicorn` |
| **Server Command** | Runs the application with auto-reload. | `uvicorn main:app --reload` |
| **API Docs** | FastAPI automatically provides interactive documentation via **Swagger UI**. | `http://localhost:8000/docs` |

---

### 🧱 Data Structure and Pydantic

**Pydantic** is used to define data schemas, ensuring data validation and easy conversion to/from JSON.

| Concept | Description | Example |
| :--- | :--- | :--- |
| **Data Models** | Define class that inherits from `BaseModel`. | `from pydantic import BaseModel` <br> `class Product(BaseModel): id: int; name: str` |
| **FastAPI Integration** | Pydantic models are used as type hints in endpoint functions, automatically validating the request body. | `def add_product(product: Product): ...` |

---

### 🎯 Initial CRUD Operations (In-Memory List)

Initial operations are performed on a simple Python list of Pydantic `Product` objects.

| HTTP Method | FastAPI Decorator | Path/URL | Key Logic |
| :--- | :--- | :--- | :--- |
| **GET All** | `@app.get("/products")` | Returns the entire global list. | `return products` |
| **GET by ID** | `@app.get("/product/{id}")` | **Dynamic Path:** Uses curly braces `{id}`. | Iterates list to find product by ID. |
| **POST (Create)** | `@app.post("/product")` | Accepts a new `Product` object. | Uses Python's list method `products.append(product)`. |
| **PUT (Update)** | `@app.put("/product/{id}")` | Requires ID and new data. | Iterates list, finds index, replaces: `products[i] = product`. |
| **DELETE** | `@app.delete("/product/{id}")` | Requires ID. | Iterates list, finds index, deletes: `del products[i]`. |

***

## 🌐 Part 2: Database Migration, Dependency Injection, and Full-Stack Connection

The application is refactored to use a **PostgreSQL** database via **SQLAlchemy** for persistent storage.

### 💾 Database Integration with SQLAlchemy

**SQLAlchemy** acts as the ORM, allowing developers to interact with the database using Python objects instead of raw SQL.

| Concept | Code/Action | Purpose |
| :--- | :--- | :--- |
| **Packages** | `pip install sqlalchemy psycopg2` | ORM and PostgreSQL driver installation. |
| **DB Engine** | `create_engine(<DB_URL>)` | Manages the database connection and dialect (e.g., PostgreSQL). |
| **DB Session** | `sessionmaker(..., bind=engine)` | Creates the object used to perform transactions (`.query()`, `.add()`, `.commit()`, `.close()`). |
| **SQLAlchemy Model** | Class inherits from `Base`, attributes use `Column(type, constraints)`. | Maps the Python object structure to a SQL table schema. |
| **Transaction** | `db.add()`, `db.delete()`, then **`db.commit()`** | **Crucial step**—must be called to persist changes to the database. |
| **Model Conversion** | `database_models.Product(**product.model_dump())` | Converts the **Pydantic** model object (for FastAPI) to the **SQLAlchemy** model object (for the DB). |

---

### 💉 Dependency Injection for DB Sessions

**Dependency Injection** simplifies resource management by providing necessary resources (like a database session) to functions, handling cleanup automatically.

| Concept | Description | Code Snippet |
| :--- | :--- | :--- |
| **`get_db()`** | A function that creates a DB session, uses **`yield db`**, and ensures **`db.close()`** in a `finally` block. | `def get_db(): try: yield db_session; finally: db_session.close()` |
| **Injection** | Used as a parameter with `Depends()` in the endpoint function. | `db: Session = Depends(get_db)` |

---

### 🔄 CRUD with SQLAlchemy

Endpoint functions now use the injected `db` object and SQLAlchemy ORM methods.

| Operation | SQLAlchemy ORM Method |
| :--- | :--- |
| **Read All** | `db.query(Product).all()` |
| **Read by ID** | `db.query(Product).filter(Product.id == id).first()` |
| **Create** | Convert Pydantic model, `db.add(db_product)`, `db.commit()` |
| **Update** | Fetch product, update fields (e.g., `db_product.name = new_name`), `db.commit()` |
| **Delete** | Fetch product, `db.delete(db_product)`, `db.commit()` |

---

### 🔗 Full-Stack Connection (CORS)

Connecting the React front-end (Port 3000) to the FastAPI backend (Port 8000) requires explicit permission due to security policies.

| Issue | Description | Fix (Middleware) |
| :--- | :--- | :--- |
| **CORS Error** | **Cross-Origin Resource Sharing** security prevents the front-end from accessing the API on a different port. | `from fastapi.middleware.cors import CORSMiddleware` |
| **CORS Configuration** | Allows requests from the front-end URL for all HTTP methods. | `app.add_middleware(CORSMiddleware, allow_origins=["http://localhost:3000"], allow_methods=["*"])` |
```
