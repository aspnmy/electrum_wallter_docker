# 一致性构建镜像 buildah bud --no-cache -f Dockerfile -t 容器名

FROM docker.io/aspnmy/debian-ssh:python3-s6-overlay-v12.7

#### --构建主服务${S6_OVERLAY_SERVIES}语句-开始
# 更新软件包列表
ADD https://download.electrum.org/4.5.6/Electrum-4.5.6.tar.gz  /tmp_srv
ADD https://download.electrum.org/4.5.6/Electrum-4.5.6.tar.gz.asc /tmp_srv 
RUN gpg --verify /tmp_srv/Electrum-4.5.6.tar.gz.asc && python3 -m pip install --user /tmp_srv/Electrum-4.5.6.tar.gz



# 设置初始root密码
RUN echo 'root:root@#1314' | chpasswd

#### --构建主服务${S6_OVERLAY_SERVIES}语句-结束
# 暴露50002端口
EXPOSE 50002
EXPOSE 622

# 清理缓存减小容器体积
RUN  apt-get autoclean && apt-get clean && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# 设置s6-overla:v${S6_OVERLAY_VERSION}全局的ENTRYPOINT
ENTRYPOINT ["/init"]
# Electrum  钱包默认开机不启动 需要登陆到ssh后手动开启 sshd如未自行启动，可登陆控制台手工启动，部分设备会有此问题
CMD ["/usr/sbin/sshd"]