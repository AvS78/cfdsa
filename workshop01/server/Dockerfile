# what is the base image we are using
FROM node:latest

# define some environment variables

ENV DB_HOST=nwdb  
ENV DB_PORT=3306 
ENV DB_PASSWORD=changeit
ENV DB_USER=root


ENV APP_PORT=3000
ENV APP_ROOT=/app

#create the $APP_ROOT directory and go inside the directory
WORKDIR ${APP_ROOT}

#we are in APP_ROOT i.e. /app. Now Copy my files from notebook into ${APP_ROOT} . represents the current root i.e. /app

ADD main.js .
ADD package-lock.json .
ADD package.json .

# copy the directories now. Note the notation. directory name

ADD public public
ADD views views
ADD config config

# add variables 


# install dependencies. This will use package.json
RUN npm install

#configure health checks

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
        CMD curl -s -f http://localhost:${APP_PORT}/health || exit 1 

#ensure that above command is input before run phase. else it will run dependencies at image run time
#############################################BUILD IS FINISHED#########################################################

################################################BuILD IS FINISHED#######################################################

# what port is the application using
EXPOSE ${APP_PORT}

# how to run the file
ENTRYPOINT [ "node","main.js" ]

################################################RUN IS FINISHED#######################################################

#all env are upper caps and no whitespaces