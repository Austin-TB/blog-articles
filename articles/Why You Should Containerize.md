## Dockerizing is the way

Containerizing is the go-to solution for easy cloud deployment. But using it locally has its perks as well. I try to make my projects, work or personal, as structured as possible, as full stack apps with distinct frontend and backend, but a new, subtly annoying issue arose - Starting both the servers in different terminals every time I open it to make changes.

This is where Docker Compose comes to the rescue. It's a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration.

### The `docker-compose.yml` file

The heart of Docker Compose is the `docker-compose.yml` file. This file defines the services, networks, and volumes for your application. Let's imagine a simple full-stack application with a Node.js backend and a React frontend.

Here's what a `docker-compose.yml` for that might look like:

```yaml
version: '3.8'
services:
  backend:
    build: ./backend
    ports:
      - "8080:8080"
    volumes:
      - ./backend:/app/backend
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app/frontend
    depends_on:
      - backend
```

In this example, we have two services: `backend` and `frontend`.

- `build`: tells Docker Compose to build the image from the `Dockerfile` in the specified directory.
- `ports`: maps the host machine's port to the container's port.
- `volumes`: mounts the local directory into the container, so any changes you make to your code are reflected inside the container instantly.
- `depends_on`: tells the `frontend` service to start only after the `backend` service has started.

### The Magic Command

Now, instead of two terminals, you just need one. Navigate to your project root and run:

```bash
docker-compose up
```

And just like that, both your frontend and backend servers are running. To stop them, simply press `Ctrl+C` or run:

```bash
docker-compose down
```

This simple workflow solves my annoyance and brings some other cool benefits.

### More Than Just Convenience

Using Docker and Docker Compose for local development isn't just about avoiding multiple terminals.

- **Consistency:** Your development environment is now defined in code. Anyone on your team can get the exact same setup by running one command. No more "it works on my machine" problems.
- **Onboarding:** New developers can get up and running in minutes. They just need to have Docker installed, clone the repo, and run `docker-compose up`.
- **Mirroring Production:** You can use a similar Docker setup in production, which reduces the chances of bugs appearing in production that you didn't see in development.

## Conclusion

So, while containerizing is fantastic for cloud deployments, don't overlook its power for local development. It streamlines your workflow, ensures consistency, and makes collaboration a breeze. That "subtly annoying issue" of managing multiple terminals was just the tip of the iceberg. Adopting Docker for local development was one of the best productivity boosts I've had.