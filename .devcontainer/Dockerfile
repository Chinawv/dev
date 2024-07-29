# 使用官方 PyTorch 镜像作为基础镜像
FROM docker.lixd.xyz/pytorch/pytorch:latest

# 更新包列表并安装 OpenSSH 服务器
RUN apt-get update && apt-get install -y openssh-server

# 创建 SSH 运行目录
RUN mkdir /var/run/sshd

# 设置 root 用户的密码为 8848
RUN echo 'root:8848' | chpasswd

# 允许 root 用户通过 SSH 登录
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# 禁用 PAM
RUN sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

# 设置环境变量
ENV NOTVISIBLE="in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# 暴露 SSH 端口
EXPOSE 22

# 启动 SSH 服务并保持容器运行
CMD ["/usr/sbin/sshd", "-D"]