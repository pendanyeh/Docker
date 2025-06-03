# Multi-Stage Docker Build

The main purpose of choosing a golang based application to demonstrate this example is golang is a statically-typed programming language that does not require a runtime in the traditional sense, unlike dynamically-typed languages like Python, Ruby, and JavaScript, which rely on a runtime environment to execute their code, Go compiles directly to machine code, which can then be executed directly by the operating system.

The real advantage of a multi-stage Docker build and distro-less images can be understood through a drastic decrease in image size.

A Multi-Stage Docker Build is a technique in Docker that uses multiple FROM statements within a single Dockerfile. This approach helps you produce smaller and more efficient images by keeping the build environment separate from the runtime environment.

### Why Use It? 
Typically, a Docker image might include all the tools needed to build your application (such as compilers and package managers), even though they're not required when the app runs. This makes the image larger than necessary.

### Multi-stage builds address this by:

- Using one stage to compile or build your app with all necessary tools.
- Copying only the essential files (like binaries or build outputs) into a second, minimal image for running the app.

### Example: Node.js Application

````dockerfile
# Stage 1: Build
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Runtime
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm install --only=production
CMD ["node", "dist/index.js"]
````

### Advantages:

- *** Smaller images:** Only runtime dependencies are included.
- *** Improved security:** Build tools are excluded from the production container.
- *** Faster deployments:** Reduced image size means quicker downloads and startups.
- *** Clear separation:** Build and runtime environments remain distinct.
