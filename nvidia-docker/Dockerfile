# NVIDIA & CentOS7
FROM nvidia/cuda:10.1-cudnn7-runtime-centos7

# ホームディレクトリ(/root)に移動
WORKDIR /root

# 必要なパッケージをインストール
RUN yum -y update && \
	yum -y install readline-devel zlib-devel bzip2-devel sqlite-devel openssl-devel \
    libXext.x86_64 libSM.x86_64 libXrender.x86_64 gcc gcc-c++ libffi-devel python-devel git

# ロケーション設定(日本語ロケールを設定)
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"

# python3系をインストール
RUN yum install -y https://repo.ius.io/ius-release-el7.rpm && \
	yum install -y python36u python36u-devel python36u-libs python36u-pip

# requirements.txtに記載されたパッケージをインストール
ADD requirements.txt /root
RUN echo `pwd` && \
	ls -al && \
	pip3.6 install --upgrade pip && \
	pip3.6 install -r requirements.txt && \
	rm -rf requirements.txt

WORKDIR /work