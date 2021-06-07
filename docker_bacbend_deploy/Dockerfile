FROM nvidia/cuda:11.2.2-devel-ubuntu20.04

# 安装Python、Pipe
RUN apt update
RUN apt install python3
RUN pip3 install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
RUN pip3 install torch==1.8.1+cu111 torchvision==0.9.1+cu111 torchaudio===0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
#编译Nginx
RUN apt install git
RUN apt-get install openssl libssl-dev libpcre3 libpcre3-dev zlib1g-dev
RUN apt-get install build-essential
RUN git clone https://github.com/winshining/nginx-http-flv-module.git
RUN wget http://nginx.org/download/nginx-1.8.0.tar.gz
RUN tar -zxvf nginx-1.17.9.tar.gz
RUN cd nginx-1.17.9
RUN ./configure --add-module=/home/nginx-http-flv-module/
RUN make && make install
COPY nginx/nginx.conf /usr/local/nginx/conf

#
COPY frontend /var/www/html
COPY backend /uar/local

COPY ./startup.sh /usr/local/

CMD [/usr/local/startup.sh]