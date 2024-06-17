# Current DevOps Setup

## GitHub Actions

- Used for both the frontend and backend repositories.
- CI: Passes if the code compilation passes correctly (TypeScript to JavaScript).
- CD: Deploys if the CI passes.
    - For backend, it removes the current running backend container and runs the new one with the "restart unless-stopped" option.
    - For frontend, Docker Compose is used because Traefik runs with the frontend container. With every CD, the frontend image tag in the Docker Compose is replaced.

## Dockerfile

- Backend: Follows all the best practices related to image size and security (0 CSV). However, critical environment variables need to be put in the Dockerfile.
- Frontend: Same practices as the backend.


**Current Problems:**

- Only one database is used for development, production, and penetration testing.

- Need separate environments for backend and frontend:
    - Penetration testing environment for isolated testing.
    - Development environment for the frontend with a stable backend (container & database).
    - Production environment.

- Using ngrok to expose the local backend container has limitations in the long term due to request limits for free users.

- Backend experiences downtime due to a single point of failure.

- Lack of a logging and monitoring solution, currently relying on docker logs.

- CI/CD occasionally delivers non-working containers without a check step to ensure correct functionality.

- API testing is needed for all backend endpoints to prevent breaking other endpoint functionality.

- Need an open-source alternative to Postman for team-wide usage.
