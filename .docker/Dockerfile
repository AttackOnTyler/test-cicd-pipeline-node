# Stage 1:Build Stage
FROM node:hydrogen-bookworm AS NodeBuild

# Install git
RUN apt-git update && \
    apt-git install -y git

# Download and install Neovim AppImage
RUN curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage && \
    chmod u+x nvim.appimage && \
    ./nvim.appimage --appimage-extract

# Set the working directory
WORKDIR /app

# Clone the app branch into the working directory
RUN git clone --single-branch --branch app https://github.com/AttackOnTyler/test-cicd-pipeline-node.git .

# Set environment to production
ENV NODE_ENV=production

# Install producion dependencies
RUN npm ci --production

# Stage 2: Final Stage
FROM node:hydrogen-bookworm-slim

# Copy the Neovim configuration from the local machine
COPY --chown=node:node ~/.config/nvim ~/.config/nvim

# Copy the built app files from the NodeBuild Stage
COPY --from=NodeBuild /app /app

# Copy Neovim from the NodeBuild Stage
COPY --from=NodeBuild /squashfs-root /

# Expose Neovim globally
RUN ln -s /AppRun /usr/bin/nvim

USER node

WORKDIR /app
