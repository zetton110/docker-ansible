# Amazon EC2
FROM amazonlinux:latest

# OpenSSHサーバをインストールする
RUN yum -y install openssh-server

# SSHサーバのホストキーを作成
RUN ssh-keygen -A

# ルートログインを許可する
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config

# パスワード認証を有効にする
RUN sed -ri 's/^#?PasswordAuthentication\s+.*/PasswordAuthentication yes/' /etc/ssh/sshd_config

# 空のパスワードを許可する（テスト目的でのみ）
RUN sed -ri 's/^#?PermitEmptyPasswords\s+.*/PermitEmptyPasswords yes/' /etc/ssh/sshd_config


RUN sed -ri 's/^#?PubkeyAuthentication\s+.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config

# ルートのパスワードを "root" に設定
RUN echo "root:root" | chpasswd

EXPOSE 22

# SSHサーバを起動
CMD ["/usr/sbin/sshd", "-D"]
