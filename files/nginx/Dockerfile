FROM nginx:1.12
LABEL maintainer="q408596288@vip.qq.com"

# set timezome(设置时区)
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone