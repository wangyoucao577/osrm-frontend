FROM debian:buster-slim

RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    curl \
    wget \
    git \
    sed \
    && rm -rf /var/lib/apt/lists/*

# install nvm and nodejs
# https://github.com/nvm-sh/nvm#install--update-script
RUN wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash && \
  export NVM_DIR="$HOME/.nvm" && \
  # This loads nvm
  [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  && \
  # https://github.com/Project-OSRM/osrm-backend/pull/5918
  nvm install node && \
  # nvm install node && \
  node --version && \
  npm --version
# Appending below nvm source string to your ~/.bashrc to let nvm/node/npm available 
#  export NVM_DIR="$HOME/.nvm"
#  [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
#  [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion


# Enables customized options using environment variables
ENV OSRM_BACKEND='http://localhost:5000'
ENV OSRM_CENTER='38.8995,-77.0269'
ENV OSRM_ZOOM='13'
ENV OSRM_LANGUAGE='en'
ENV OSRM_LABEL='Car (fastest)'

# Copy package.json
RUN mkdir -p /src
COPY package.json /src

# Install app dependencies
RUN cd /src && \
    npm install

# Create app directory
COPY . /src
WORKDIR /src

# Run App
EXPOSE 9966
CMD ["npm", "start"]
