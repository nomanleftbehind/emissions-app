# Emissions App

The aim of this project is to create a functional web app integrated with database and server for tracking and quantifiying greenhouse gas emissions.

## Technology

### Server
- [Rust](https://www.rust-lang.org/) programming language
- [Async-graphql](https://async-graphql.github.io/async-graphql/en/index.html) server integration with [Actix](https://actix.rs/) web framework for Rust
- [Diesel](https://diesel.rs/) ORM to interact with PostgreSQL database

### Database
- [PostgreSQL](https://www.postgresql.org/) object-relational database

### Client
- [Svelte](https://svelte.dev/) web framework (not implemented yet)


I primarily started this project to learn Rust in practice. With that goal in mind, this documentation is written in a way to guide complete beginners through technology stack integration and towards successful compilation of the program.

Big shout-out to [philipdaquin](https://github.com/philipdaquin/Twitter-Clone-WASM) and [open-msupply](https://github.com/openmsupply/open-msupply) without whom this process would have taken a lot longer.

## Setup

### Install Rust and Cargo
Follow the instructions on official [Rust](https://www.rust-lang.org/learn/get-started) website to install the language.

### Install PostgreSQL

Download and install [PostgreSQL](https://www.postgresql.org/download/). You will be asked to set up a password for superuser called "postgres" and port number at the end of the installation.

Run `psql --port=5432 -U=postgres`. Make sure the port number is the same as the one you chose during the installation process.

You will be prompted to enter superuser password.

Run
`CREATE DATABASE emissions;` and `CREATE DATABASE emissions_test;`.

### Install Diesel CLI
Make sure you have PostgreSQL in your Environment Variables Path. Example: `C:\Program Files\PostgreSQL\14\lib` and `C:\Program Files\PostgreSQL\14\bin`.

Run `cargo install diesel_cli --no-default-features --features postgres` command in your terminal.

It's possible you will run into an error while installing. If that happens, follow official [Diesel](https://diesel.rs/guides/getting-started) guide on how to resolve it.

### Setup Diesel
We need to tell Diesel where to find our database. We do this by setting the DATABASE_URL environment variable.

Rename `users/.env.example` file to `users/.env`. Inside, replace the word 'password' of DATABASE_URL with earlier defined superuser password.

The general form for a PostgreSQL connection URI is `postgresql://[user[:password]@][host][:port][/dbname]`

Navigate to `users` folder with `cd users`. Populate your database by running `diesel migration run`. It executes `up.sql` commands located in `users/migrations` folder.

### Build binary and run locally
Navigate back to project root with `cd ..`. Compile program by running `cargo run`.

### Potential errors during build
- If you are compiling on Windows machine you might run into an error with 'argonautica' package as it requires `libclang.dll`, which is part of LLVM. Download [LLVM](https://github.com/llvm/llvm-project/releases/tag/llvmorg-14.0.0). Click `LLVM-14.0.0-win64.exe` or `LLVM-14.0.0-win32.exe`, depending on your system. During installation make sure you select to add LLVM to your path. Compilation should be succesful after installing it.

- You might run into `error: failed to run custom build command for rdkafka-sys`. Installing the latest version of [CMake](https://cmake.org/download/) should solve that.

Open http://localhost:8081/graphiql. It opens a GraphQL IDE for better development workflows, context-aware autocompletion & error highlighting.