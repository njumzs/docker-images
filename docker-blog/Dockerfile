FROM ubuntu:14.04
MAINTAINER Zhanshuai Meng (nju.mzs@outlook.com)

#change zh_CN print 
RUN echo "zh_CN.UTF-8 UTF-8" >> /var/lib/locales/supported.d/local && \
    echo "zh_CN.GBK GBK" >> /var/lib/locales/supported.d/local && \ 
    dpkg-reconfigure locales

ENV BLOG_USER="mzsvps" 
ENV BASE_DIR="/home/${BLOG_USER}" 
ENV BLOG_DIR="${BASE_DIR}/sites/blog" 
ENV POST_DIR="${BLOG_DIR}/source/_posts" \
    NODE_DIR="/opt/nodejs"

# install dependent tools
RUN apt-get update && \
    apt-get install -y wget npm git && \
    echo "install wget npm git tools over" && \
    rm -rf /var/lib/apt/lists/*

# install nodejs v0.12.7
RUN wget https://npm.taobao.org/mirrors/node/v0.12.7/node-v0.12.7-linux-x64.tar.gz && \
    tar xvzf node-v0.12.7-linux-x64.tar.gz && \
    echo "node zip get"
RUN rm /bin/sh && ln -s /bin/bash /bin/sh 

ENV NODE_HOME=${NODE_DIR}
ENV PATH=$PATH:$NODE_HOME/bin
ENV NODE_PATH=$NODE_HOME/lib/node_modules

RUN mv node-v0.12.7-linux-x64 /opt/nodejs && \
#    echo "export node compile over" && \
#    echo "export NODE_HOME=${NODE_DIR}" >> /etc/profile && \
#    echo "export PATH=\$PATH:\$NODE_HOME/bin" >> /etc/profile && \
#    echo "export NODE_PATH=\$NODE_HOME/lib/node_modules" >> /etc/profile && \
#    source /etc/profile && \
    echo "install nodejs over"

RUN echo "setup the hexo env" && \
    cd /root/  && \
    npm install hexo-cli -g && \
    hexo init blog && \
    rm -rf blog  && \
    echo "hexo set up over"


EXPOSE 22/tcp 80/tcp 4000/tcp

VOLUME ["/root/blog"]
RUN echo "volume mount over "
COPY start.sh /app/
CMD ["sh","/app/start.sh"]

