# Module 05 — REST APIs, Validation, and Error Handling

# Resource-Oriented Design

Prefer:

```text
POST   /orders
GET    /orders/{id}
GET    /orders
PATCH  /orders/{id}
DELETE /orders/{id}
```

Avoid RPC-style endpoints unless the operation truly represents a command that does not map naturally to CRUD.

Sometimes an action endpoint is reasonable:

```text
POST /orders/{id}/cancel
```

---

# HTTP Methods

## GET
Read. Should not mutate business state.

## POST
Create or submit a command.

## PUT
Replace a resource representation.

## PATCH
Partially modify.

## DELETE
Remove.

---

# Useful Status Codes

| Code | Meaning |
|---|---|
| 200 | successful request |
| 201 | created |
| 204 | success, no body |
| 400 | malformed/invalid request |
| 401 | unauthenticated |
| 403 | authenticated but forbidden |
| 404 | resource not found |
| 409 | state conflict |
| 422 | semantically invalid request |
| 429 | rate limited |
| 500 | unexpected server failure |

---

# Validation

```java
public record CreateUserRequest(
    @NotBlank String name,
    @Email String email
) {}
```

Controller:

```java
@PostMapping
public ResponseEntity<UserResponse> create(
        @Valid @RequestBody CreateUserRequest request) {
    ...
}
```

Keep structural validation separate from deeper business rules.

---

# Global Error Handling

```java
@RestControllerAdvice
public class ApiExceptionHandler {

    @ExceptionHandler(OrderNotFoundException.class)
    ResponseEntity<ProblemDetail> handle(OrderNotFoundException ex) {
        var problem = ProblemDetail.forStatus(HttpStatus.NOT_FOUND);
        problem.setDetail(ex.getMessage());
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(problem);
    }
}
```

---

# Pagination

For large lists, avoid returning everything.

Use:

- page + size
- cursor pagination
- stable sort

Cursor pagination is often better for large changing datasets.

---

# API Compatibility

Avoid casually breaking:

- field names
- enum values
- semantics
- required fields

Additive API changes are usually easier for clients.

---

# DTO Mapping

Do not expose JPA entities directly.

Map explicitly or use a mapping library if it stays understandable.

---

# Lab

Build:

```text
POST /orders
GET /orders/{id}
GET /orders?page=0&size=20
POST /orders/{id}/cancel
```

Add:

- validation
- Problem Details
- 404
- 409 on illegal order state
- request correlation ID

---

# Interview Questions

1. PUT vs PATCH?
2. 401 vs 403?
3. 400 vs 422?
4. Why pagination?
5. Offset vs cursor pagination?
6. Why not expose entities?
7. What is API versioning?
8. What makes an HTTP operation idempotent?
