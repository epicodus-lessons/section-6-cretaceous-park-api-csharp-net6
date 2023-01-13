## What Is This?

This is an example repo corresponding to multiple lessons within the LearnHowToProgram.com walkthrough on creating an ASP.NET Core API in [Section 6: Building an API](https://www.learnhowtoprogram.com/c-and-net/building-an-api). Later we create [an ASP.NET Core MVC app](https://github.com/epicodus-lessons/section-6-cretaceous-park-client-csharp-net6).

This project is called the "Cretaceous Park API", while the client is called the "Cretaceous Park Client".

There are multiple branches in this repo that are described more below.

Finally, this project was scaffolded using [`dotnet new`](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-new).

## How To Run This Project

### Install Tools

Install the tools that are introduced in [this series of lessons on LearnHowToProgram.com](https://www.learnhowtoprogram.com/c-and-net/getting-started-with-c).

If you have not already, install the `dotnet-ef` tool by running the following command in your terminal:

```
dotnet tool install --global dotnet-ef --version 6.0.0
```

### Set Up and Run Project

1. Clone this repo.
2. Open the terminal and navigate to this project's production directory called "CretaceousApi".
3. Within the production directory "CretaceousApi", create two new files: `appsettings.json` and `appsettings.Development.json`.
4. Within `appsettings.json`, put in the following code. Make sure to replacing the `uid` and `pwd` values in the MySQL database connection string with your own username and password for MySQL. For the LearnHowToProgram.com lessons, we always assume the `uid` is `root` and the `pwd` is `epicodus`.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Port=3306;database=cretaceous_api;uid=root;pwd=epicodus;"
  }
}
```

5. Within `appsettings.Development.json`, add the following code:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Trace",
      "Microsoft.AspNetCore": "Information",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  }
}
```

6. Create the database using the migrations in the Cretaceous Park API project. Open your shell (e.g., Terminal or GitBash) to the production directory "CretaceousApi", and run `dotnet ef database update`. You may need to run this command for each of the branches in this repo. 
    - To optionally create a migration, run the command `dotnet ef migrations add MigrationName` where `MigrationName` is your custom name for the migration in UpperCamelCase. To learn more about migrations, visit the LHTP lesson [Code First Development and Migrations](https://www.learnhowtoprogram.com/c-and-net-part-time/many-to-many-relationships/code-first-development-and-migrations).
7. Within the production directory "CretaceousApi", run `dotnet watch run --launch-profile "CretaceousApi-Production"` in the command line to start the project in production mode with a watcher. 
8. To optionally further build out this project in development mode, start the project with `dotnet watch run` in the production directory "CretaceousApi".
9. Use your program of choice to make API calls. In your API calls, use the domain _http://localhost:5000_. Keep reading to learn about all of the available endpoints.

## Testing the API Endpoints

You are welcome to test this API via [Postman](https://www.postman.com/), [curl](https://curl.se/), or [the ASP.NET Core MVC frontend "Cretaceous Park Client"](https://github.com/epicodus-lessons/section-6-cretaceous-park-api-csharp-net6) create to work with this API. 

If you want to use the Cretaceous Park Client, an ASP.NET Core MVC application, follow the setup instructions in the README of [this repo](https://github.com/epicodus-lessons/section-6-cretaceous-park-api-csharp-net6). 

### Available Endpoints

```
GET http://localhost:5000/api/animals/
GET http://localhost:5000/api/animals/{id}
POST http://localhost:5000/api/animals/
PUT http://localhost:5000/api/animals/{id}
DELETE http://localhost:5000/api/animals/{id}
```

Note: `{id}` is a variable and it should be replaced with the id number of the animal you want to GET, PUT, or DELETE.

#### Optional Query String Parameters for GET Request

GET requests to `http://localhost:5000/api/animals/` can optionally include query strings to filter or search animals.

| Parameter   | Type        |  Required    | Description |
| ----------- | ----------- | -----------  | ----------- |
| species     | String      | not required | Returns animals with a matching species value |
| name        | String      | not required | Returns animals with a matching name value |
| minimumAge  | Number      | not required | Returns animals that have an age value that is greater than or equal to the specified minimumAge value |

The following query will return all animals with a species value of "Dinosaur":

```
GET http://localhost:5000/api/animals?species=dinosaur
```

The following query will return all animals with the name "Matilda":

```
GET http://localhost:5000/api/animals?name=matilda
```

The following query will return all animals with an age of 10 or older:

```
GET http://localhost:5000/api/animals?minimumAge=10
```

You can include multiple query strings by separating them with an `&`:

```
GET http://localhost:5000/api/animals?species=dinosaur&minimumAge=10
```

#### Additional Requirements for POST Request

When making a POST request to `http://localhost:5000/api/animals/`, you need to include a **body**. Here's an example body in JSON:

```json
{
  "species": "Tyrannosaurus Rex",
  "name": "Elizabeth",
  "age": 8
}
```

#### Additional Requirements for PUT Request

When making a PUT request to `http://localhost:5000/api/animals/{id}`, you need to include a **body** that includes the animal's `animalId` property. Here's an example body in JSON:

```json
{
  "animalId": 1,
  "species": "Tyrannosaurus Rex",
  "name": "Lizzy",
  "age": 9
}
```

And here's the PUT request we would send the previous body to:

```
http://localhost:5000/api/animals/1
```

Notice that the value of `animalId` needs to match the id number in the URL. In this example, they are both 1.

## Available Branches

**1_setup_and_seeding**: This branch includes the code we added after working through the following lessons:

- https://www.learnhowtoprogram.com/c-and-net/building-an-api/scaffolding-a-net-application-with-dotnet-new
- https://www.learnhowtoprogram.com/c-and-net/building-an-api/exploring-the-dotnet-new-web-api-template
- https://www.learnhowtoprogram.com/c-and-net/building-an-api/adding-a-model-and-database
- https://www.learnhowtoprogram.com/c-and-net/building-an-api/seeding-the-database

**2_crud_functionality**: This branch includes the code we added after working through the following lessons:

- https://www.learnhowtoprogram.com/c-and-net/building-an-api/api-create-and-read
- https://www.learnhowtoprogram.com/c-and-net/building-an-api/api-update-and-delete

**3_query_strings**: This branch includes the code we added after working through the following lesson:

- https://www.learnhowtoprogram.com/c-and-net/building-an-api/adding-parameters-to-a-get-request-to-support-query-strings

**There are other lessons in this series, but the rest are not implemented in this example repo:**

- https://www.learnhowtoprogram.com/c-and-net/building-an-api/adding-api-model-validation
- https://www.learnhowtoprogram.com/c-and-net/building-an-api/scaffolding-api-controllers
- https://www.learnhowtoprogram.com/c-and-net/building-an-api/further-exploration-with-apis
