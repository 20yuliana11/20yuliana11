- 👋 Hi, I’m @20yuliana11
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
20yuliana11/20yuliana11 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
FROM python:3.8-slim-buster as main
ENV OKTETO=true
ENV GIT_PYTHON_REFRESH=quiet
ENV PIP_NO_CACHE_DIR=1
RUN apt update && apt install libcairo2 git ffmpeg libavcodec-dev libavutil-dev libavformat-dev libswscale-dev libavdevice-dev -y --no-install-recommends
RUN rm -rf /var/lib/apt/lists /var/cache/apt/archives /tmp/*
RUN git clone https://github.com/hikariatama/Hikka /Hikka
WORKDIR /Hikka
RUN pip install --no-warn-script-location --no-cache-dir -r requirements.txt
RUN pip install --no-warn-script-location --no-cache-dir -r optional_requirements.txt
EXPOSE 8080
RUN mkdir /data
CMD ["python3", "-m", "hikka"]
