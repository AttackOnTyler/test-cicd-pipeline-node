# Stage 1:Build Stage
FROM node:hydrogen-bookworm 
# AS NodeBuild

# Install git
RUN apt-get update && \
    apt-get install -y git

# Download and install Neovim AppImage
RUN curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage && \
    chmod u+x nvim.appimage && \
    ./nvim.appimage --appimage-extract && \
    ln -s /squashfs-root/AppRun /usr/bin/nvim && \
    mkdir -p /home/node/.config/nvim

# Set the working directory
WORKDIR /app

# Clone the app branch into the working directory
RUN git clone --single-branch --branch app https://github.com/AttackOnTyler/test-cicd-pipeline-node.git .

# Install producion dependencies
RUN npm install 

# Set environment to production
ENV NODE_ENV=production

# Ensure node user has ownership of the /app directory
RUN chown -R node:node /app

# Set the user to 'node'
USER node

# Stage 2: Final Stage
# FROM node:hydrogen-bookworm-slim

# Copy the Neovim configuration from the local machine
# COPY --from=NodeBuild /home/node/.config/nvim /home/node/.config/nvim

# Copy the built app files from the NodeBuild Stage
# COPY --from=NodeBuild /app /app

# Copy Neovim from the NodeBuild Stage
# COPY --from=NodeBuild /squashfs-root /

# RUN rm -f /usr/bin/nvim

# Expose Neovim globally
# RUN ln -s /AppRun /usr/bin/nvim

# USER node

# WORKDIR /app
