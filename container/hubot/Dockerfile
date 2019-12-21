FROM node

RUN npm install -g yo generator-hubot
RUN npm list -g yo generator-hubot
RUN useradd bot
RUN mkdir /home/bot && chown -R bot:bot /home/bot

WORKDIR /home/bot

ADD ./run.sh .
RUN chmod +x ./run.sh
RUN printenv | awk '{print "export " $1}' > /root/env.sh

USER bot

RUN yo hubot --owner "someone" --name "bot" --description "Slack Hubot on Docker" --adapter "slack" 
# RUN yo hubot --owner=${HUBOT_OWNER} --name=${HUBOT_NAME} --description=${HUBOT_DESCRIPTION} --adapter "slack" 

CMD ["sh", "./run.sh"]

