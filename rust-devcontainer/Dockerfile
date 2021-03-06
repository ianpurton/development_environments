# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.148.1/containers/rust/.devcontainer/base.Dockerfile
# figlet with comments | sed -e 's/^/#  /'
FROM mcr.microsoft.com/vscode/devcontainers/rust:1

ARG PULUMI_VERSION=3.0.0

USER vscode

RUN cd ~ \
  #      _                           ____ _     ___ 
  #     / \    _____   _ _ __ ___   / ___| |   |_ _|
  #    / _ \  |_  / | | | '__/ _ \ | |   | |    | | 
  #   / ___ \  / /| |_| | | |  __/ | |___| |___ | | 
  #  /_/   \_\/___|\__,_|_|  \___|  \____|_____|___|
  #  
  && curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash \
  #   _   _           _          _ ____  
  #  | \ | | ___   __| | ___    | / ___| 
  #  |  \| |/ _ \ / _` |/ _ \_  | \___ \ 
  #  | |\  | (_) | (_| |  __/ |_| |___) |
  #  |_| \_|\___/ \__,_|\___|\___/|____/ 
  #
  && curl -sL https://deb.nodesource.com/setup_14.x | sudo bash -\
  && sudo apt-get update -y \
  && sudo apt-get install -y nodejs \
  #   _  __     _           ____ _____ _     
  #  | |/ /   _| |__   ___ / ___|_   _| |    
  #  | ' / | | | '_ \ / _ \ |     | | | |    
  #  | . \ |_| | |_) |  __/ |___  | | | |___ 
  #  |_|\_\__,_|_.__/ \___|\____| |_| |_____|
  # 
  && sudo curl -sSL -o /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
  && sudo chmod +x /usr/local/bin/kubectl \
  #   ____             _             
  #  |  _ \  ___   ___| | _____ _ __ 
  #  | | | |/ _ \ / __| |/ / _ \ '__|
  #  | |_| | (_) | (__|   <  __/ |   
  #  |____/ \___/ \___|_|\_\___|_|   
  #
  && sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common lsb-release \
  && sudo curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | sudo apt-key add - 2>/dev/null \
  && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" \
  && sudo apt-get update \
  && sudo apt-get install -y docker-ce-cli \
  #   ____         ____ _____ _     
  #  |  _ \  ___  / ___|_   _| |    
  #  | | | |/ _ \| |     | | | |    
  #  | |_| | (_) | |___  | | | |___ 
  #  |____/ \___/ \____| |_| |_____|
  #  
  && curl -OL https://github.com/digitalocean/doctl/releases/download/v1.37.0/doctl-1.37.0-linux-amd64.tar.gz \
  && tar xvf doctl-1.37.0-linux-amd64.tar.gz \
  && sudo mv doctl /usr/bin \
  && rm doctl-1.37.0-linux-amd64.tar.gz \
  #   _   _      _           _____ 
  #  | | | | ___| |_ __ ___ |___ / 
  #  | |_| |/ _ \ | '_ ` _ \  |_ \ 
  #  |  _  |  __/ | | | | | |___) |
  #  |_| |_|\___|_|_| |_| |_|____/ 
  # 
  && curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 && sudo chmod 700 get_helm.sh && sudo ./get_helm.sh && rm ./get_helm.sh \
  #   ____  _                _    ____ _     ___ 
  #  |  _ \(_) ___  ___  ___| |  / ___| |   |_ _|
  #  | | | | |/ _ \/ __|/ _ \ | | |   | |    | | 
  #  | |_| | |  __/\__ \  __/ | | |___| |___ | | 
  #  |____/|_|\___||___/\___|_|  \____|_____|___|
  # 
  && cargo install diesel_cli --no-default-features --features postgres \
  #   ____  ____   ___  _     
  #  |  _ \/ ___| / _ \| |    
  #  | |_) \___ \| | | | |    
  #  |  __/ ___) | |_| | |___ 
  #  |_|   |____/ \__\_\_____|
  #  
  && sudo apt-get install -y postgresql postgresql-client libpq-dev \
  #   _  _____      
  #  | |/ / _ \ ___ 
  #  | ' / (_) / __|
  #  | . \\__, \__ \
  #  |_|\_\ /_/|___/
  # 
  && curl -L -s https://github.com/derailed/k9s/releases/download/v0.24.1/k9s_Linux_x86_64.tar.gz | tar xvz -C /tmp && sudo mv /tmp/k9s /usr/bin \
  # adr-tools
  && git clone --depth 1 https://github.com/npryce/adr-tools && sudo mv adr-tools/src/* /usr/bin && rm -rf adr-tools \
  # Stuff needed for cypress
  && sudo apt-get install -y --no-install-recommends libgtk2.0-0 libgtk-3-0 libgbm-dev libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 libxtst6 xauth xvfb \
  #   ____        _                 _ 
  #  |  _ \ _   _| |_   _ _ __ ___ (_)
  #  | |_) | | | | | | | | '_ ` _ \| |
  #  |  __/| |_| | | |_| | | | | | | |
  #  |_|    \__,_|_|\__,_|_| |_| |_|_|
  #  
  && cd ~ && curl -fsSL https://get.pulumi.com | bash -s -- --version $PULUMI_VERSION \
  #   _     _       _                _ 
  #  | |   (_)_ __ | | _____ _ __ __| |
  #  | |   | | '_ \| |/ / _ \ '__/ _` |
  #  | |___| | | | |   <  __/ | | (_| |
  #  |_____|_|_| |_|_|\_\___|_|  \__,_|
  # 
  && cd ~ && curl -sL https://run.linkerd.io/install | sh \
  #   __  __      _____ _       
  #  |  \/  | ___|  ___| |_   _ 
  #  | |\/| |/ __| |_  | | | | |
  #  | |  | | (__|  _| | | |_| |
  #  |_|  |_|\___|_|   |_|\__, |
  #                       |___/ 
  && curl -sL https://github.com/cantino/mcfly/releases/download/v0.5.0/mcfly-v0.5.0-x86_64-unknown-linux-gnu.tar.gz | tar xvz \
  && sudo mv mcfly* /usr/bin \
  && echo "if [[ -r /usr/bin/mcfly.bash ]]; then" >> ~/.bashrc \
  && echo "  source /usr/bin/mcfly.bash" >> ~/.bashrc \
  && echo "fi" >> ~/.bashrc \
  #   __  __ _          
  #  |  \/  (_)___  ___ 
  #  | |\/| | / __|/ __|
  #  | |  | | \__ \ (__ 
  #  |_|  |_|_|___/\___|
  #  
  && sudo apt-get install -y figlet texlive-latex-extra latexmk swaks telnet \
  && cargo install rage \
  && cargo install --force cargo-make \
  && cargo install wasm-bindgen-cli cargo-watch cargo-deny trunk \
  && rustup target add wasm32-unknown-unknown \
  #    ____ _                              ____       _                
  #   / ___| |__  _ __ ___  _ __ ___   ___|  _ \ _ __(_)_   _____ _ __ 
  #  | |   | '_ \| '__/ _ \| '_ ` _ \ / _ \ | | | '__| \ \ / / _ \ '__|
  #  | |___| | | | | | (_) | | | | | |  __/ |_| | |  | |\ V /  __/ |   
  #   \____|_| |_|_|  \___/|_| |_| |_|\___|____/|_|  |_| \_/ \___|_|   
  # 
  # Sanity check with https://gist.github.com/ianpurton/8f2340ef01a2d0bc4efed60b5c157885
  #
  && PLATFORM=linux64 \
  && VERSION=$(curl http://chromedriver.storage.googleapis.com/LATEST_RELEASE) \
  && curl http://chromedriver.storage.googleapis.com/$VERSION/chromedriver_$PLATFORM.zip -LOk \
  && unzip chromedriver_* \
  && sudo mv chromedriver /usr/bin \
  && rm chromedriver_* \
  && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
  && sudo apt install -y ./google-chrome-stable_current_amd64.deb \
  && rm google-chrome* \
  # Clean up
  && sudo apt-get autoremove -y \
  && sudo apt-get clean -y \
  && sudo rm -rf /var/lib/apt/lists/*


RUN echo "alias gst='git status'"  >> ~/.bashrc \ 
    && echo "alias gcm='git checkout master'"  >> ~/.bashrc \  
    && echo "alias c=clear"  >> ~/.bashrc \  
    && echo "alias gp='git push'"  >> ~/.bashrc \  
    && echo "alias gcam='git commit -a -m'"  >> ~/.bashrc \  
    && echo "alias linkerd='~/.linkerd2/bin/linkerd'"  >> ~/.bashrc \  
    && echo "alias gpsup='git push --set-upstream origin $(git_current_branch)'"  >> ~/.bashrc \  
    && echo "alias gcb='git checkout -b'" >> ~/.bashrc \
    && echo "alias gitsetup='git config --global user.name \$NAME && git config --global user.email \$EMAIL && mkdir -p ~/.ssh && cp -u /home/host-ssh/id_rsa ~/.ssh && chmod 600 ~/.ssh/id_rsa && ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub'" >> ~/.bashrc
    
