# MyBlog

**MyBlog** is a web application for sharing .NET knowledge, built with a modern tech stack and Clean Architecture principles. The project serves as a personal blog platform to publish articles, categorize content, and engage with readers through comments. It also demonstrates best practices in .NET development, making it a showcase for learning and professional branding.

## Features
- Create, read, update, and delete blog posts with categories and comments.
- User management for authors and commenters.
- Clean Architecture with CQRS (Command Query Responsibility Segregation) for scalability and maintainability.
- Code-first approach using Entity Framework Core for MySQL.
- RESTful API backend with ASP.NET Core.
- Frontend built with ReactJS (Vite) for a responsive user interface (in progress).
- Containerized deployment with Docker (optional).

## Tech Stack
- **Backend**: ASP.NET Core 8.0, Entity Framework Core, MediatR (CQRS)
- **Database**: MySQL (supports Aiven for MySQL for cloud deployment)
- **Frontend**: ReactJS (Vite) with Tailwind CSS (planned)
- **Other**: Docker, Swagger (API documentation)

## Project Structure
The project follows **Clean Architecture** with three main layers, ensuring separation of concerns and testability:

```
my-blog
├── src
│   ├── MyBlog.Domain           # Entities, interfaces, and core business logic
│   ├── MyBlog.Application      # Use cases, CQRS commands/queries, DTOs
│   ├── MyBlog.Infrastructure   # EF Core, repositories, external services
│   ├── MyBlog.Api             # API controllers, ASP.NET Core configuration
│   └── MyBlog.Web             # ReactJS frontend (planned)
├── tests
│   ├── MyBlog.Domain.Tests
│   ├── MyBlog.Application.Tests
│   └── MyBlog.Api.Tests
└── docker-compose.yml          # Docker configuration for deployment
```

### Layers
1. **Domain**: Contains entities (`User`, `Post`, `Category`, `Comment`) and repository interfaces. No dependencies on other layers.
2. **Application**: Implements business logic using CQRS with MediatR. Contains commands (e.g., `CreatePostCommand`) and queries (e.g., `GetPostByIdQuery`).
3. **Infrastructure**: Implements EF Core `DbContext`, repositories, and database access. Connects to MySQL.
4. **Api**: Exposes RESTful endpoints using ASP.NET Core controllers. Integrates with Application and Infrastructure layers.

## Getting Started

### Prerequisites
- [.NET SDK 8.0](https://dotnet.microsoft.com/download)
- [MySQL 8.0](https://dev.mysql.com/downloads/) or Aiven for MySQL
- [Node.js 18+](https://nodejs.org/) (for frontend, when implemented)
- [Docker](https://www.docker.com/) (optional, for containerized deployment)
- [Git](https://git-scm.com/)

### Installation
1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/my-blog.git
   cd my-blog
   ```

2. **Set up MySQL**:
   - Install MySQL locally or use Aiven for MySQL (see [Aiven Migration Guide](https://aiven.io/docs/products/mysql/howto/migrate-db-to-aiven-via-console)).
   - Update the connection string in `src/MyBlog.Api/appsettings.json`:
     ```json
     "ConnectionStrings": {
       "DefaultConnection": "Server=localhost;Port=3306;Database=blog_dotnet;User=root;Password=your_password;"
     }
     ```

3. **Restore dependencies**:
   ```bash
   cd src/MyBlog.Api
   dotnet restore
   ```

4. **Apply database migrations**:
   ```bash
   cd ../MyBlog.Infrastructure
   dotnet ef migrations add InitialCreate -s ../MyBlog.Api
   dotnet ef database update -s ../MyBlog.Api
   ```

5. **Run the API**:
   ```bash
   cd ../MyBlog.Api
   dotnet run
   ```
   - Access the API at `https://localhost:5001/swagger` for Swagger documentation.

6. **Frontend (coming soon)**:
   - The ReactJS frontend will be located in `src/MyBlog.Web`. Instructions will be updated once implemented.

### Docker (Optional)
To run the application with Docker:
1. Ensure Docker and Docker Compose are installed.
2. Update `docker-compose.yml` with your MySQL credentials.
3. Run:
   ```bash
   docker-compose up --build
   ```

## API Endpoints
- `GET /api/posts/{id}`: Retrieve a post by ID.
- `POST /api/posts`: Create a new post.
- More endpoints (for users, categories, comments) will be added.

## Contributing
Contributions are welcome! Please follow these steps:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

## Roadmap
- Implement ReactJS frontend with Vite and Tailwind CSS.
- Add authentication (JWT) for user management.
- Support post tags and search functionality.
- Integrate with Aiven for MySQL for cloud deployment.
- Write unit tests for Domain and Application layers.
- Publish blog posts about the development process.

## License
This project is licensed under the [MIT License](LICENSE).

## Contact
- Author: Doan Tuan Khai (Dre Kai)
- Email: khai.lumberjack@gmail.com
- Blog: [Your Blog URL, if available]

Feel free to reach out for feedback, questions, or collaboration opportunities!
