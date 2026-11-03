# E-commerce example (Lab 3)

A small console shop: choose products, then pay. Package `de.haw.hamburg.sel.ex_ecommerce`, main class **`Demo`**.

You work on this code twice in Lab 3:

- **Warm-up (in the lab):** refactor the payment to the **Strategy** pattern
- **Report, task R2:** add a product catalogue with the **Composite** pattern

The tasks are in the Lab 3 sheet.

## Run it

**In an IDE:** open the folder `exercises/ecommerce` (or mark `src` as sources root) and run `Demo`.

**In a terminal** (also Git Bash on Windows), inside `exercises/ecommerce`:

```bash
javac -d out src/de/haw/hamburg/sel/ex_ecommerce/*.java
java -cp out de.haw.hamburg.sel.ex_ecommerce.Demo
```

Type your input line by line when the program asks for it.

## PayPal test accounts

| Email | Password |
|---|---|
| studi@haw.de | Passw0rd |
| prof@haw.de | qwertz |
